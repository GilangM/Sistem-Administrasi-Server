### **Administration System Practical Final Project Report**

Gilang Maulana (1202190011) & Dinda Tresna Teja Nirwana (1202190050)

1. ##### Buat LXC baru yang terdiri dari :

- 6 Instance LXC ubuntu 20.04 PHP 7.4

```markdown
sudo lxc-create -n lxc_php7_1 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_2 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_3 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_5 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php7_6 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no validate --server images.linuxcontainers.org
```

- 2 Instance LXC debian 10 PHP 5.6

```markdown
sudo lxc-create -n lxc_php5_1 -t download -- --dist debian --release buster --arch amd64 --force-cache --no validate --server images.linuxcontainers.org

sudo lxc-create -n lxc_php5_2 -t download -- --dist debian --release buster --arch amd64 --force-cache --no validate --server images.linuxcontainers.org
```

- 1 instance LXC debian 10 mariadb server

```markdown
sudo lxc-create -n lxc_mariadb -t download -- --dist debian --release buster --arch amd64 --force-cache --no validate --server images.linuxcontainers.org
```

2. **Setting sites-available pada VM menggunakan nama kelompok05.fpsas dan symlink ke sites-enabled**

``` 
 upstream laravel {
        least_conn;
        server lxc_php7_1.dev;
        server lxc_php7_4_laravel.dev;
        server lxc_php7_6_laravel.dev;
        server lxc_php7_2_laravel.dev;
  }
  upstream yii {
        server lxc_php7_2_yii.dev weight=2;
        server lxc_php7_1_yii.dev weight=3;
        server lxc_php7_4_yii.dev weight=4;
        server lxc_php7_5_yii.dev weight=1;
        server lxc_php7_6_yii.dev weight=6;
   }
  upstream ci {
        server lxc_php5_1.dev;
        server lxc_php5_2.dev;
  }
  upstream wp {
        ip_hash;
        server lxc_php7_3_wp.dev;
        server lxc_php7_2.dev;
        server lxc_php7_4_wp.dev;
        server lxc_php7_5_wp.dev;
  }

  server {
          listen 80;
          listen [::]:80;

          server_name kelompok5.fpsas;

          root /var/www/html;
          index index.html;

          location /app {
		                kelompok05.fpsas                  Modified
                  rewrite /app/?(.*)$ /$1 break;
                  #proxy_pass http://lxc_php5_1.dev;
                  proxy_pass http://ci;
          }

          location /product {
                  rewrite /product/?(.*)$ /$1 break;
                  #proxy_pass http://lxc_php7_6_yii.dev;
                  proxy_pass http://yii;
          }

          location /phpmyadmin {
                  rewrite /phpmyadmin/?(.*)$ /$1 break;
                  proxy_pass http://lxc_db_server.dev;
          }

          location / {
                  #rewrite /php7/?(.*)$ /$1 break;
                  #proxy_pass http://lxc_php7_1.dev;
                  proxy_pass http://laravel;
          }

  }

  server {
         listen 80;

         server_name news.kelompok5.fpsas;

         root /var/www/html;
         index index.html;

         location / {
                  #rewrite /php7/?(.*)$ /$1 break;
                  #proxy_pass http://lxc_php7_3_wp.dev;
                  proxy_pass http://wp;
	}
}
```

4. **Daftarkan semua LXC pada /etc/hosts di VM**

```
127.0.0.1 localhost
127.0.1.1 sas02
127.0.1.1 kelompok5.fpsas news.kelompok5.fpsas

# The following lines are desirable for IPv6 capable hosts
::1     ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters

#laravel
10.0.3.101  lxc_php7_1L.dev
10.0.3.102  laravel_2.dev
10.0.3.104  laravel_3.dev
10.0.3.106  laravel_4.dev

#yii
10.0.3.101  yii.dev
10.0.3.102  lxc_php7_2Y.dev
10.0.3.104  yii_2.dev
10.0.3.105  yii_3.dev
10.0.3.106  yii_4.dev

#wp
10.0.3.103  wordpress.dev
10.0.3.102  wordpress_1.dev
10.0.3.104  wordpress_2.dev
10.0.3.105  wordpress_3.dev

#ci
10.0.3.111  lxc_php5_1.dev
10.0.3.112  lxc_php5_2.dev

#db
10.0.3.200  lxc_db_server.dev
```

5. **Deploy website menggunakan ansible :**

- Setting hosts ansible

  ![setting host ansible](https://user-images.githubusercontent.com/26424175/152106073-858e0603-e142-4e11-8a74-2d361197b318.PNG)ve.PNG)

  ```
  [database]
  lxc_db_server ansible_host=lxc_db_server.dev ansible_ssh_user=root ansible_>
  
  [php5]
  lxc_php5_1 ansible_host=lxc_php5_1.dev ansible_ssh_user=root ansible_become>
  lxc_php5_2 ansible_host=lxc_php5_2.dev ansible_ssh_user=root ansible_become>
  
  [laravel]
  lxc_php7_1 ansible_host=lxc_php7_1L.dev ansible_ssh_user=root ansible_becom>
  lxc_php7_2 ansible_host=lxc_php7_2.dev ansible_ssh_user=root ansible_become>
  lxc_php7_4 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become>
  lxc_php7_6 ansible_host=lxc_php7_6.dev ansible_ssh_user=root ansible_become>
  
  [wordpress]
  lxc_php7_2 ansible_host=lxc_php7_2.dev ansible_ssh_user=root ansible_become>
  lxc_php7_3 ansible_host=lxc_php7_3.dev ansible_ssh_user=root ansible_become>
  lxc_php7_4 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become>
  lxc_php7_5 ansible_host=lxc_php7_5.dev ansible_ssh_user=root ansible_become>
  
  [yii]
  lxc_php7_1 ansible_host=lxc_php7_1.dev ansible_ssh_user=root ansible_become>
  lxc_php7_2 ansible_host=lxc_php7_2Y.dev ansible_ssh_user=root ansible_becom>
  lxc_php7_4 ansible_host=lxc_php7_4.dev ansible_ssh_user=root ansible_become>
  lxc_php7_5 ansible_host=lxc_php7_5.dev ansible_ssh_user=root ansible_become>
  lxc_php7_6 ansible_host=lxc_php7_6.dev ansible_ssh_user=root ansible_become>
  ```

  

#### Install Mariadb

Masukkan perintah nano install-mariadb.yml

```
- hosts: database
  vars:
    username: 'admin'
    password: 'admin'
    domain: 'lxc_db_server.dev'
  roles:
    - db
    - pma
```

#### Roles db

/ansible/tubes/roles/db/handlers

```
---
- name: restart mysql
  become: yes
  become_user: root
  become_method: su
  action: service name=mysql state=restarted
```

/ansible/tubes/roles/db/tasks

```
---
- name: delete apt chache
  become: yes
  become_user: root
  become_method: su
  command: rm -vf /var/lib/apt/lists/*

- name: install mariadb
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
   - python
   - mariadb-server
   - python-mysqldb
   - python-pymysql

- name: Stop MySQL
  service: name=mysqld state=stopped

- name: set environment variables
  shell: systemctl set-environment MYSQLD_OPTS="--skip-grant-tables"

- name: Start MySQL
  service: name=mysqld state=started

- name: sql query
  command:  mysql -u root --execute="UPDATE mysql.user SET authentication_s>
- name: sql query flush
  command:  mysql -u root --execute="FLUSH PRIVILEGES"

- name: Stop MySQL
  service: name=mysqld state=stopped
- name: unset environment variables
  shell: systemctl unset-environment MYSQLD_OPTS

- name: Start MySQL
  service: name=mysqld state=started

- name: Create user for mysql
  command:  mysql -u root --execute="CREATE USER IF NOT EXISTS '{{ username>

- name: GRANT ALL PRIVILEGES to user {{username}}
  command:  mysql -u root --execute="GRANT ALL PRIVILEGES ON * . * TO '{{ u>

- name: Create user for remote mysql
  command:  mysql -u root --execute="CREATE USER IF NOT EXISTS '{{ username>

- name: GRANT ALL PRIVILEGES to remote user {{username}}
  command:  mysql -u root --execute="GRANT ALL PRIVILEGES ON * . * TO '{{ u>

- name: sql query flush
  command:  mysql -u root --execute="FLUSH PRIVILEGES"

- name: Create DB laravel
  command:  mysql -u root --execute="CREATE DATABASE IF NOT EXISTS `laravel>

- name: Create DB wordpress
  command:  mysql -u root --execute="CREATE DATABASE IF NOT EXISTS `wordpre>

- name: Create DB yii
  command:  mysql -u root --execute="CREATE DATABASE IF NOT EXISTS `yii`;"

- name: Create DB codeigniter
  command:  mysql -u root --execute="CREATE DATABASE IF NOT EXISTS `ci`;"

- name: Copy .my.cnf file with root password credentials
  template:
    src=templates/my.cnf
	 dest=/etc/mysql/mariadb.conf.d/50-server.cnf
  notify: restart mysql
```

/ansible/tubes/roles/db/templates

```
#
# These groups are read by MariaDB server.
# Use it for options that only the server (but not clients) should see
#
# See the examples of server my.cnf files in /usr/share/mysql/
#

# this is read by the standalone daemon and embedded servers
[server]

# this is only for the mysqld standalone daemon
[mysqld]

#
# * Basic Settings
#
user            = mysql
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
port            = 3306
basedir         = /usr
datadir         = /var/lib/mysql
tmpdir          = /tmp
lc-messages-dir = /usr/share/mysql
skip-external-locking

# Instead of skip-networking the default is now to listen only on
# localhost which is more compatible and is not less secure.
bind-address            = 0.0.0.0

#
# * Fine Tuning
#
key_buffer_size         = 16M
max_allowed_packet      = 16M
thread_stack            = 192K
thread_cache_size       = 8
# This replaces the startup script and checks MyISAM tables if needed
# the first time they are touched
myisam_recover_options  = BACKUP
#max_connections        = 100
#table_cache            = 64
#thread_concurrency     = 10

#
# * Query Cache Configuration
#
query_cache_limit       = 1M
query_cache_size        = 16M

#
# * Logging and Replication
#
# Both location gets rotated by the cronjob.
# Be aware that this log type is a performance killer.
# As of 5.1 you can enable the log at runtime!
#general_log_file        = /var/log/mysql/mysql.log
#general_log             = 1
#
# Error log - should be very few entries.
#
log_error = /var/log/mysql/error.log
#
# Enable the slow query log to see queries with especially long duration
#slow_query_log_file    = /var/log/mysql/mariadb-slow.log
#long_query_time = 10
#log_slow_rate_limit    = 1000
#log_slow_verbosity     = query_plan
#log-queries-not-using-indexes
#
# The following can be used as easy to replay backup logs or for replication.
# note: if you are setting up a replication slave, see README.Debian about
#       other settings you may need to change.
#server-id              = 1
#log_bin                        = /var/log/mysql/mysql-bin.log
expire_logs_days        = 10
max_binlog_size   = 100M
#binlog_do_db           = include_database_name
#binlog_ignore_db       = exclude_database_name

#
# * InnoDB
#
# InnoDB is enabled by default with a 10MB datafile in /var/lib/mysql/.
# Read the manual for more InnoDB related options. There are many!

#
# * Security Features
#
# Read the manual, too, if you want chroot!
# chroot = /var/lib/mysql/
#
# For generating SSL certificates you can use for example the GUI tool "tinyca".
#
# ssl-ca=/etc/mysql/cacert.pem
# ssl-cert=/etc/mysql/server-cert.pem
# ssl-key=/etc/mysql/server-key.pem
#
# Accept only connections using the latest and most secure TLS protocol version.
# ..when MariaDB is compiled with OpenSSL:
# ssl-cipher=TLSv1.2
# ..when MariaDB is compiled with YaSSL (default in Debian):
# ssl=on

#
# * Character sets
#
# MySQL/MariaDB default is Latin1, but in Debian we rather default to the full
# utf8 4-byte character set. See also client.cnf
#
character-set-server  = utf8mb4
collation-server      = utf8mb4_general_ci

#
# * Unix socket authentication plugin is built-in since 10.0.22-6
#
# Needed so the root database user can authenticate without a password but
# only when running as the unix root user.
#
# Also available for other users if required.
# See https://mariadb.com/kb/en/unix_socket-authentication-plugin/

# this is only for embedded server
[embedded]

# This group is only read by MariaDB servers, not by MySQL.
# If you use the same .cnf file for MySQL and MariaDB,
# you can put MariaDB-only options here
[mariadb]

# This group is only read by MariaDB-10.1 servers.
# If you use the same .cnf file for MariaDB of different versions,
# use this group for options that older servers don't understand
[mariadb-10.1]
```

#### Roles pma

/ansible/tubes/roles/pma/handlers

```
---
- name: stop apache2
  become: yes
  become_user: root
  become_method: su
  action: service name=apache2 state=stopped

- name: restart nginx
  become: yes
  become_user: root
  become_method: su
  action: service name=nginx state=restarted

- name: restart php
  become: yes
  become_user: root
  become_method: su
  action: service name=php7.2-fpm state=restarted
```

/ansible/tubes/roles/pma/tasks

```
---
- name: delete apt chache
  become: yes
  become_user: root
  become_method: su
  command: rm -vf /var/lib/apt/lists/*

- name: install requirement dpkg to install php5
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - ca-certificates
    - apt-transport-https
    - wget
    - curl
    - python-apt
    - software-properties-common
    - git

- name: Add key
  apt_key:
    url: https://packages.sury.org/php/apt.gpg
    state: present
- name: Add Php Repository
  apt_repository:
      repo: "deb https://packages.sury.org/php/ stretch main"
      state: present
      filename: php.list
      update_cache: true
- name: wget repository php
  shell: wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/ap>

- name: add repository php
  shell: echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee>

- name: wget repository
  shell: wget https://files.phpmyadmin.net/phpMyAdmin/5.1.1/phpMyAdmin-5.1.1-all>

- name: tar phpmyadmin
  shell: tar -zxvf phpMyAdmin-5.1.1-all-languages.tar.gz

- name: move phpmyadmin
  shell: mv phpMyAdmin-5.1.1-all-languages /usr/share/phpMyAdmin

- name: apt update
  shell: apt update

- name: install nginx phpmyadmin
  become: yes
 become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - curl
    - nginx
    - nginx-extras
    - php7.2-fpm
    - php7.2-mysqli
    - php7.2-xml
    - php-mbstring
    - php-zip
    - php-gd
    - php-json
    - php-curl
- name: enable module php mbstring
  command: phpenmod mbstring
  notify:
    - restart php

- name: Copy pma.local
  template:
    src=templates/pma.local
    dest=/etc/nginx/sites-available/{{ domain }}
  vars:
    servername: '{{ domain }}'
- name: Symlink pma.local
  command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enab>  notify:
    - restart nginx

- name: Write {{ domain }} to /etc/hosts
  lineinfile:
    dest: /etc/hosts
    regexp: '.*{{ domain }}$'
    line: "127.0.0.1 {{ domain }}"
    state: present
```

/ansible/tubes/roles/pma/templates

```
server {
    listen 80;

    server_name {{servername}};

    root /usr/share/phpmyadmin;

    index index.php;

    location / {

         try_files $uri $uri/ @phpmyadmin;

 }

 location @phpmyadmin {
            fastcgi_pass unix:/run/php/php7.2-fpm.sock;   #Sesuaikan dengan vers>
            fastcgi_param SCRIPT_FILENAME /usr/share/phpmyadmin/index.php;

            include /etc/nginx/fastcgi_params;

            fastcgi_param SCRIPT_NAME /index.php;

    }
```

Setelah itu, jalankan perintah untuk melakukan install mariadb

```
ansible-playbook -i hosts install-mariadb.yml -k
```



#### **Install Laravel**

Install Laravel install-laravel.yml

```
---
- hosts: laravel
  vars:
    username: 'admin'
    password: 'admin'
    domain: 'lxc_php7_1L.dev'
  roles:
    - laravel
```

/ansible/tubes/roles/laravel/handlers

```
---
- name: stop apache2
  become: yes
  become_user: root
  become_method: su
  action: service name=apache2 state=stopped

- name: restart nginx
  become: yes
  become_user: root
  become_method: su
  action: service name=nginx state=restarted

- name: restart php
  become: yes
  become_user: root
  become_method: su
  action: service name=php7.2-fpm state=restarted
```

/ansible/tubes/roles/laravel/tasks

```
---
- name: delete apt chache
  become: yes
  become_user: root
  become_method: su
  command: rm -vf /var/lib/apt/lists/*

- name: install requirement dpkg to install php7.4
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - ca-certificates
    - apt-transport-https
    - curl
    - python-apt
    - software-properties-common

- name: Add Php Repository 7.4
  apt_repository:
    repo: "ppa:ondrej/php"
    state: present
    filename: php.list
    update_cache: true
- name: install nginx php7.4
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - git
    - nginx
    - nginx-extras
    - php7.4
    - php7.4-fpm
    - php7.4-curl
    - php7.4-mbstring
    - php7.4-xml
    - php7.4-gd
    - php7.4-opcache
    - php7.4-zip
    - php7.4-json
    - php7.4-cli

- name: Download and install Composer
  shell: curl -sS https://getcomposer.org/installer | php
  args:
    chdir: /usr/src/
    creates: /usr/local/bin/composer
    warn: false
     become: yes

- name: Add Composer to global path
  copy:
    dest: /usr/local/bin/composer
    group: root
    mode: '0755'
    owner: root
    src: /usr/src/composer.phar
    remote_src: yes
  become: yes

- name: Composer create project
  composer:
    command: create-project
    arguments: laravel/laravel landing
    working_dir: /var/www/html
    prefer_dist: yes
  environment:
    COMPOSER_NO_INTERACTION: "1"

- name: set APP_URL
  lineinfile:
    dest=/var/www/html/landing/.env
    regexp='^APP_URL='
    line=APP_URL=http://kelompok05.fpsas

- name: set DB_HOST
  lineinfile:
    dest=/var/www/html/landing/.env
    regexp='^DB_HOST='
    line=DB_HOST=10.0.3.200

- name: set DB_DATABASE
  lineinfile:
    dest=/var/www/html/landing/.env
    regexp='^DB_DATABASE='
    line=DB_DATABASE=landing

- name: set DB_USERNAME
  lineinfile:
     dest=/var/www/html/landing/.env
     regexp='^DB_USERNAME='
     line=DB_USERNAME=admin

- name: set DB_PASSWORD
  lineinfile:
    dest=/var/www/html/landing/.env
    regexp='^DB_PASSWORD='
    line=DB_PASSWORD=admin

- name: change permission storage
  command: chmod -R 777 /var/www/html/landing/storage
- name: Copy landing.conf
  template:
    src=templates/landing
    dest=/etc/nginx/sites-available/{{ domain }}
  vars:
      servername: '{{ domain }}'

- name: www.conf
  lineinfile:
     dest: /etc/php/7.4/fpm/pool.d/www.conf
     regexp: '^listen = /run/php/php7.4-fpm.sock'
     line: listen = 127.0.0.1:9001
     state: present

- name: Delete another nginx config
  become: yes
  become_user: root
  become_method: su
  command: rm -f /etc/nginx/sites-enabled/*

- name: Symlink landing.conf
  command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enab>  notify:
    restart nginx

- name: Write {{ domain }} to /etc/hosts
  lineinfile:
    dest: /etc/hosts
    regexp: '.*{{ domain }}$'
    line: "127.0.0.1   {{ domain }}"
    state: present
```

/ansible/tubes/roles/laravel/templates$ nano landing

```
server {

    listen 80;

    server_name {{ domain }};

    root /var/www/html/landing/public;
    index index.php index.html index.htm;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        #fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_pass 127.0.0.1:9001;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
 }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

Setelah itu, jalankan perintah untuk melakukan install laravel

```
ansible-playbook -i hosts install-laravel.yml -k
```



#### Install Codeigniter

Install-ci.yml

```
- hosts: php5
  vars:
    git_url: 'https://github.com/aldonesia/sas-ci'
    destdir: '/var/www/html/ci'
    domain: 'lxc_php5_1.dev'
  roles:
    - app
```

/ansible/tubes/roles/ci/handlers

```
---
- name: restart nginx
  become: yes
  become_user: root
  become_method: su
  action: service name=nginx state=restarted

- name: restart php
  become: yes
  become_user: root
  become_method: su
  action: service name=php5.6-fpm state=restarted

```

/ansible/tubes/roles/ci/tasks

```
---
- name: delete apt chache
  become: yes
  become_user: root
  become_method: su
  command: rm -vf /var/lib/apt/lists/*

- name: install requirement dpkg to install php5
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - ca-certificates
    - apt-transport-https
    - wget
    - curl
    - python-apt
    - software-properties-common
    - git

- name: Add key
  apt_key:
    url: https://packages.sury.org/php/apt.gpg
    state: present
- name: Add Php Repository
  apt_repository:
      repo: "deb https://packages.sury.org/php/ stretch main"
      state: present
      filename: php.list
      update_cache: true

- name: wget repository
  shell: wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/ap>

- name: add repository
  shell: echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee>

- name: apt update
  shell: apt update

- name: install nginx php5
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - nginx
    - nginx-extras
    - php5.6
    - php5.6-fpm
 - php5.6-common
    - php5.6-cli
    - php5.6-curl
    - php5.6-mbstring
    - php5.6-mysqlnd
    - php5.6-xml

- name: Git clone repo sas-ci
  become: yes
  git:
    repo: '{{ git_url }}'
    dest: "{{ destdir }}"

- name: Copy app.conf
  template:
    src=templates/app.conf
    dest=/etc/nginx/sites-available/{{ domain }}
  vars:
    servername: '{{ domain }}'

- name: Delete another nginx config
  become: yes
  become_user: root
  become_method: su
  command: rm -f /etc/nginx/sites-enabled/*

- name: Symlink app.conf
  command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enab>  notify:
    - restart nginx

- name: Write {{ domain }} to /etc/hosts
  lineinfile:
    dest: /etc/hosts
    regexp: '.*{{ domain }}$'
    line: "127.0.0.1 {{ domain }}"
    state: present
```

/ansible/tubes/roles/ci/templates$ nano app.conf

```
server {
  listen 80;`
  server_name {{servername}};
  root {{ destdir }};
  index index.php;
  location / {
     try_files $uri $uri/ /index.php?$query_string;
  }
  location ~ \.php$ {
     fastcgi_pass unix:/run/php/php5.6-fpm.sock;  #Sesuaikan dengan versi PHP
     fastcgi_index index.php;
     fastcgi_param SCRIPT_FILENAME {{ destdir }}$fastcgi_script_name;
     include fastcgi_params;
  }
}
```

Setelah itu, jalankan perintah untuk melakukan install codeigniter

```
ansible-playbook -i hosts install-ci.yml -k
```



#### Install Wordpress

Install-wp.yml

```
---
- hosts: wordpress
  vars:
    username: 'admin'
    password: 'admin' #DON'T FORGET TO CHANGE
    domain: 'wordpress.dev' #wordpress_1.dev wordpress_2.dev wordpress_3.dev
  roles:
    - wp
```

/ansible/tubes/roles/wp/handlers

```
- name: restart nginx
  become: yes
  become_user: root
  become_method: su
  action: service name=nginx state=restarted

- name: restart php
  become: yes
  become_user: root
  become_method: su
  action: service name=php7.4-fpm state=restarted

```

/ansible/tubes/roles/wp/tasks

```
---
- name: delete apt chache
  become: yes
  become_user: root
  become_method: su
  command: rm -vf /var/lib/apt/lists/*

- name: install requirement dpkg to install php7.4
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - ca-certificates
    - apt-transport-https
    - curl
    - python-apt
    - software-properties-common

- name: Add Php Repository 7.4
  apt_repository:
    repo: "ppa:ondrej/php"
    state: present
    filename: php.list
    update_cache: true

- name: install nginx php7.4
  become: yes
  become_user: root
  become_method: su
  apt: name={{ item }} state=latest update_cache=true
  with_items:
    - nginx
    - nginx-extras
    - curl
    - wget
    - php7.4
    - php7.4-fpm
    - php7.4-curl
    - php7.4-xml
    - php7.4-gd
    - php7.4-opcache
    - php7.4-mbstring
    - php7.4-zip
    - php7.4-json
    - php7.4-cli
    - php7.4-mysqlnd
    - php7.4-xmlrpc

- name: wget wordpress
  shell: wget -c http://wordpress.org/latest.tar.gz

- name: tar latest.tar.gz
  shell: tar -xvzf latest.tar.gz

- name: copy folder wordpress
  shell: cp -R wordpress /var/www/html/blog

- name: chmod
  become: yes
  become_user: root
  become_method: su
  command: chmod 775 -R /var/www/html/blog/

- name: copy .wp-config.conf
  template:
    src=templates/wp.conf
    dest=/var/www/html/blog/wp-config.php

- name: copy wp.local
  template:
    src=templates/wp.local
    dest=/etc/nginx/sites-available/{{ domain }}
  vars:
    servername: '{{ domain }}'

- name: Delete another nginx config
  become: yes
 become_user: root
  become_method: su
  command: rm -f /etc/nginx/sites-enabled/*

- name: Symlink sites-available wordpress
  command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enab>  notify:
    - restart nginx

- name: Write {{ domain }} to /etc/hosts
  lineinfile:
    dest: /etc/hosts
    regexp: '.*{{ domain }}$'
    line: "127.0.0.1   {{ domain }}"
    state: present

- name: enable module php mbstring
  command: phpenmod mbstring
  notify:
    - restart php
```

/ansible/tubes/roles/wp/templates$ nano wp.conf

```
<?php
/**
* The base configuration for WordPress
*
* The wp-config.php creation script uses this file during the installation.
* You don't have to use the web site, you can copy this file to "wp-config.php"
* and fill in the values.
*
* This file contains the following configurations:
*
* * MySQL settings
* * Secret keys
* * Database table prefix
* * ABSPATH
*
* @link https://wordpress.org/support/article/editing-wp-config-php/
*
* @package WordPress
*/

define( 'WP_HOME', 'http://news.kelompok5.fpsas' );
define( 'WP_SITEURL', 'http://news.kelompok5.fpsas' );

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define( 'DB_NAME', 'news' );

/** MySQL database username */
define( 'DB_USER', 'admin' );

/** MySQL database password */
define( 'DB_PASSWORD', 'chintya' );

/** MySQL hostname */
define( 'DB_HOST', '10.0.3.200:3306' );

/** Database charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8' );

/** The database collate type. Don't change this if in doubt. */
define( 'DB_COLLATE', '' );

/**#@+
* Authentication unique keys and salts.
*
* Change these to different unique phrases! You can generate these using
* the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret>*
* You can change these at any point in time to invalidate all existing cookies.
* This will force all users to have to log in again.
*
* @since 2.6.0
*/
define( 'AUTH_KEY',         'put your unique phrase here' );
define( 'SECURE_AUTH_KEY',  'put your unique phrase here' );
define( 'LOGGED_IN_KEY',    'put your unique phrase here' );
define( 'NONCE_KEY',        'put your unique phrase here' );
define( 'AUTH_SALT',        'put your unique phrase here' );
define( 'SECURE_AUTH_SALT', 'put your unique phrase here' );
define( 'LOGGED_IN_SALT',   'put your unique phrase here' );
define( 'NONCE_SALT',       'put your unique phrase here' );

/**#@-*/

/**
* WordPress database table prefix.
*
* You can have multiple installations in one database if you give each
* a unique prefix. Only numbers, letters, and underscores please!
*/
$table_prefix = 'wp_';

/**
* For developers: WordPress debugging mode.
*
* Change this to true to enable the display of notices during development.
* It is strongly recommended that plugin and theme developers use WP_DEBUG
* in their development environments.
*
* For information on other constants that can be used for debugging,
* visit the documentation.
*
* @link https://wordpress.org/support/article/debugging-in-wordpress/
*/
define( 'WP_DEBUG', false );

/* Add any custom values between this line and the "stop editing" line. */



/* That's all, stop editing! Happy publishing. */

/** Absolute path to the WordPress directory. */
if ( ! defined( 'ABSPATH' ) ) {
      define( 'ABSPATH', __DIR__ . '/' );
}

/** Sets up WordPress vars and included files. */
require_once ABSPATH . 'wp-settings.php';
```

Isi templates/wp.local

```
server {

    listen 80;

    server_name {{ domain }};

    root /var/www/html/blog;
    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

Setelah itu, jalankan perintah untuk melakukan install wordpress

```
ansible-playbook -i hosts install-wp.yml -k
```



#### Install Yii 2.0

Install-yii.yml

```
---
- hosts: yii
  vars:
    username: 'admin'
    password: 'admin'
    domain: 'lxc_php7_2Y.dev'
  roles:
    - yii
```

/ansible/tubes/roles/yii/handlers

```
---
- name: restart nginx
  become: yes
  become_user: root
  become_method: su
  action: service name=nginx state=restarted

- name: restart php
  become: yes
  become_user: root
  become_method: su
  action: service name=php5.6-fpm state=restarted
```

/ansible/tubes/roles/wp/tasks

```
---
- name: delete apt chache
  become: yes
  become_user: root
  become_method: su
  command: rm -vf /var/lib/apt/lists/*

- name: Download and install Composer
  shell: curl -sS https://getcomposer.org/installer | php
  args:
    chdir: /usr/src/
    creates: /usr/local/bin/composer
    warn: false
  become: yes

- name: Add Composer to global path
  copy:
    dest: /usr/local/bin/composer
    group: root
    mode: '0755'
    owner: root
    src: /usr/src/composer.phar
    remote_src: yes
  become: yes

- name: Ansible delete file create-project
 file:
    path: /var/www/html/basic
    state: absent

- name: composer create-project
  shell: /usr/local/bin/composer create-project --prefer-dist yiisoft/yii2-app-b>

- name: chmod
  become: yes
  become_user: root
  become_method: su
  command: chmod +x /usr/local/bin/composer

- name: composer
  shell: cd /var/www/html/basic; /usr/local/bin/composer install  --no-interacti>

- name: Copy .env.template
  template:
    src=templates/env.template
    dest=/var/www/html/basic/config/db.php

- name: Copy yii.conf
  template:
    src=templates/yii.conf
    dest=/etc/nginx/sites-available/{{ domain }}
  vars:
 servername: '{{ domain }}'

- name: Symlink yii.conf
  command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enab>  notify:
    - restart nginx

- name: Write {{ domain }} to /etc/hosts
  lineinfile:
    dest: /etc/hosts
    regexp: '.*{{ domain }}$'
    line: "127.0.0.1 {{ domain }}"
    state: present
```

/ansible/tubes/roles/wp/templates$ nano db.php

```
<?php

return [
    'class' => 'yii\db\Connection',
    'dsn' => 'mysql:host=127.0.3.200:3306;dbname=product',
    'username' => 'admin',
    'password' => 'admin',
    'charset' => 'utf8',
];
```

/ansible/tubes/roles/wp/templates$ nano product.config

```
server {
        listen 80;
        listen [::]:80;

        server_name {{servername}};

        root /var/www/html/product/web;
        index index.php;

        charset utf-8;

        location / {
                index  index.html index.php;
                try_files $uri $uri/ /index.php?$args;
        }

        location ~ ^/(protected|framework|themes/\w+/views) {
                deny  all;
        }

        # pass the PHP scripts to FastCGI server listening on UNIX socket
        location ~ \.php {
                fastcgi_split_path_info  ^(.+\.php)(.*)$;
        #let yii catch the calls to unexising PHP files
                set $fsn /index.php;
                if (-f $document_root$fastcgi_script_name){
 set $fsn $fastcgi_script_name;
                }
                fastcgi_pass   127.0.0.1:9001;
                include fastcgi_params;
                fastcgi_param  SCRIPT_FILENAME  $document_root$fsn;

       #PATH_INFO and PATH_TRANSLATED can be omitted, but RFC 3875 specifies the>                fastcgi_param  PATH_INFO        $fastcgi_path_info;
                fastcgi_param  PATH_TRANSLATED  $document_root$fsn;
        }

        # prevent nginx from serving dotfiles (.htaccess, .svn, .git, etc.)
        location ~ /\. {
                deny all;
                access_log off;
                log_not_found off;
        }
}
```

Setelah itu, jalankan perintah untuk melakukan install yii

```
ansible-playbook -i hosts install-yii.yml -k
```

