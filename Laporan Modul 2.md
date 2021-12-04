# Laporan Modul 2

Kelompok 5 

Gilang Maulana 1202190011 | Dinda Tresna Teja Nirwana 1202190050

1. Rubah LXC landing dengan ubuntu focal (destroy n create, same ip, same name)

   ```markdown
   rm /var/lib/lxc/ubuntu_landing/lxc_snapshots
   lxc-destroy ubuntu_landing
   lxc-ls -f
   ```

   ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\1.PNG)

kemudian buat ubuntu focal

```markdown
sudo lxc-create -n ubuntu_landing -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\2.PNG)

jalankan ubuntu_landing dan instal net-tools

```markdown
lxc-start ubuntu_landing
lxc-attach ubuntu_landing
apt install nano net-tools curl
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\3.PNG)

setting ip ubuntu_landing 10.0.3.103/24

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\4.PNG)

```markdown
netplan apply
ip r
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\5.PNG)

konfigurasi ssh server pada ubuntu_landing

```markdown
apt install openssh-server phyton -y
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\6.PNG)

konfigurasi file sshd_config

```markdown
PermitRootLogin yes
RSAAuthentication yes
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\7.PNG)

```markdown
service sshd restart
passwd
exit
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\8.PNG)

jalankan ssh server

```markdown
ssh root@10.0.3.103
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 1\soal nomor 1\9.PNG)

2. Rubah LXC php7 dengan ubuntu focal (destroy n create, same ip, same name)

   ```markdown
   rm /var/lib/lxc/ubuntu_php7.4/lxc_snapshots
   lxc-destroy ubuntu_php7.4 -f
   lxc-ls -f
   ```

   ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\1.PNG)

```markdown
sudo lxc-create -n ubuntu_php7.4 -t download -- --dist ubuntu --release focal --arch amd64 --force-cache --no-validate --server images.linuxcontainers.org
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\2.PNG)

jalankan lxc 

```markdown
lxc-start ubuntu_php7.4
lxc-attach ubuntu_php7.4
apt install nano net-tools curl
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\3.PNG)

setting ip menjadi 10.10.3.101/24

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\4.PNG)

```markdown
netplan apply
ip r
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\5.PNG)

kemudian instal ssh server

```markdown
apt-get install openssh-server -y
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\6.PNG)

konfigurasi file sshd_config

```markdown
PermitRootLogin yes
RASAAuthentication yes
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\7.PNG)

```markdown
service sshd restart
passwd
```

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\8.PNG)

jalankan ssh server

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\soal nomor 2\soal nomor 2\9.PNG)

3. vm.local/

   * Pertama-tama yaitu membuat directory laravel 8 pada lxc_landing

     ```markdown
     mkdir laravel
     cd laravel/
     ```

     ![](C:\Users\user\Documents\SAS no 3\1.PNG)

* Setelah membuat directory laravel 8, maka langkah selanjutnya yaitu mengatur konfigurasi ansible di nano hosts dan nano nginxphp.yml

  ```markdown
  nano hosts
  [landing]
  ubuntu_landing ansible_host=lxc_landing.dev ansible_ssh_user=root ansible_become_pass=1234
  ```

  ![](C:\Users\user\Documents\SAS no 3\2.PNG)

```markdown
nano nginxphp.yml
```

```markdown
---
- hosts: all
  become : yes
  tasks:
    - name: install nginx nginx extras
      apt:
       pkg:
         - nginx
         - nginx-extras
       state: latest
    - name: start nginx
      service:
       name: nginx
       state: started
    - name: menginstall tools
      apt:
       pkg:
         - curl
         - software-properties-common
         - unzip
       state: latest
    - name: "Repo PHP 7.4"
      apt_repository:
        repo="ppa:ondrej/php"
    - name: "Updating the repo"
      apt: update_cache=yes
    - name: Installation PHP 7.4
      apt: name=php7.4 state=present
    - name: install php untuk laravel
      apt:
       pkg:
          - php7.4-fpm
          - php7.4-mysql
          - php7.4-mbstring
          - php7.4-xml
          - php7.4-bcmath
          - php7.4-json
          - php7.4-zip
          - php7.4-common
       state: present

```

![](C:\Users\user\Documents\SAS no 3\3.PNG)

* Setelah berhasil di konfigurasi, maka langkah selanjutnya yaitu mencoba untuk menjalankan ansible playbook nginxphp.yml

  ```markdown
  ansible-playbook -i hosts nginxphp.yml -k
  ```

  ![](C:\Users\user\Documents\SAS no 3\4.PNG)

* Setelah berhasil dijalankan, maka step selanjutnya yaitu membuat file installcomposer.yml

  ```markdown
  nano installcomposer.yml
  ```

  ```markdown
  ---
   -hosts: all
    become : yes
    tasks:
     - name: Download and install Composer
       shell: curl -sS https://getcomposer.org/installer | php
       args:
        chdir: /usr/src/
        creates: /usr/local/bin/composer
        warn: false
     - name: Add Composer to global path
       copy:
        dest: /usr/local/bin/composer
        group: root
        mode: '0755'
        owner: root
        src: /usr/src/composer.phar
        remote_src: yes
     - name: Composer create project
       become_user: root
       composer:
        command: create-project
        arguments: laravel/laravel landing 
        working_dir: /var/www/html
        prefer_dist: yes
       environment:
          COMPOSER_NO_INTERACTION: "1"
     - name: mengkopi file .env.example jadi .env
       copy:
        dest: /var/www/html/landing/.env.example
        src: /var/www/html/landing/.env
        remote_src: yes
     - name: mengganti konfigurasi .env
       lineinfile:
        path: /var/www/html/landing/.env
        regexp: "{{ item.regexp }}"
        line: "{{ item.line }}"
        backrefs: yes
       loop:
        - { regexp: '^(.)DB_HOST(.)$', line: 'DB_HOST=10.0.3.200' }
        - { regexp: '^(.)DB_DATABASE(.)$', line: 'DB_DATABASE=landing' }
        - { regexp: '^(.)DB_USERNAME(.)$', line: 'DB_USERNAME=admin' }
        - { regexp: '^(.)DB_PASSWORD(.)$', line: 'DB_PASSWORD= ' }
        - { regexp: '^(.)APP_URL(.)$', line: 'APP_URL=http://vm.local' }
        - { regexp: '^(.)APP_NAME=(.)$', line: 'APP_NAME=landing' }
     - name: Composer install ke landing
       composer:
         command: install
         working_dir: /var/www/html/landing
       environment:
         COMPOSER_NO_INTERACTION: "1"
     - name: generate php artisan
       args:
        chdir: /var/www/html/landing
       shell: php artisan key:generate
     - name: mengganti permission storage
       file:
        path: /var/www/html/landing/storage
        mode: 0777
        recurse: yes
  
  ```

  ![](C:\Users\user\Documents\SAS no 3\5.PNG)

* Setelah membuat file install composer.yml, maka langkah selanjutnya yaitu menjalankan ansible playbook installcomposer.yml

  ```markdown
  ansible-playbook -i hosts installcomposer.yml -k
  ```

  ![](C:\Users\user\Documents\SAS no 3\6.PNG)

* Setelah berhasil dijalankan, maka langkah selanjutnya yaitu setting lxc_landing.dev

```markdown
nano lxc_landing.dev
```

```markdown
server {
        listen 80;

        root /var/www/html/landing/public;
        index index.php index.html index.htm;
        server_name lxc_landing.dev;

        error_log /var/log/nginx/landing_error.log;
        access_log /var/log/nginx/landing_access.log;

        client_max_body_size 100M;
        location / {
                try_files $uri $uri/ /index.php$args;
        }
        location ~\.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:run/php/php7.4-fpm.sock;
                fastcgi_param SCRIPTFILENAME $document_root$fastcgi_script_name;
        }
}
```

![](C:\Users\user\Documents\SAS no 3\7.PNG)

* setelah setting lxc_landing dilakukan, maka step selanjutnya yaitu setting config.yml

```markdown
nano config.yml
```

```markdown
---
- hosts: all
  become : yes
  vars:
    domain: 'lxc_landing.dev'
  tasks:
   - name: stop apache2
     service:
      name: apache2
      state: stopped
      enabled: no
   - name: Write {{ domain }} to /etc/hosts
     lineinfile:
      dest: /etc/hosts
      regexp: '.*{{ domain }}$'
      line: "127.0.0.1 {{ domain }}"
      state: present
   - name: ensure nginx is at the latest version
     apt: name=nginx state=latest
   - name: start nginx
     service:
      name: nginx
      state: started
   - name: copy the nginx config file 
     copy:
      src: ~/ansible/laravel/lxc_landing.dev
      dest: /etc/nginx/sites-available/lxc_landing.dev
   - name: Symlink lxc_landing.dev
     command: ln -sfn /etc/nginx/sites-available/lxc_landing.dev /etc/nginx/sites-enabled/lxc_landing.dev
     args:
      warn: false
   - name: restart nginx
     service:
      name: nginx
      state: restarted
   - name: restart php7
     service:
      name: php7.4-fpm
      state: restarted
   - name: curl web
     command: curl -i http://lxc_landing.dev
     args:
      warn: false

```

![](C:\Users\user\Documents\SAS no 3\8.PNG)

* Setelah setting config.yml, maka langkah selanajutnya yaitu coba memanggil config.yml

  ```markdown
   ansible-playbook -i hosts config.yml -k
  ```

  ![](C:\Users\user\Documents\SAS no 3\9.PNG)

* Setelah berhasil dijalankan, maka langkah step selanjutnya yaitu mengakses url vm.local

  ![](C:\Users\user\Documents\SAS no 3\10.PNG)

4. vm.local/blog

   * Pertama-tama membuat directory wordpress terbaru pada ansible

     ```markdown
     cd ~/ansible/
     mkdir wordpress
     cd wordpress/
     ```

     ![](C:\Users\user\Documents\SAS no 4\1.PNG)

* Setelah berhasil install, maka langkah selanjutnya yaitu masuk dan setting wordpress nano host

  ```markdown
  nano hosts
  ```

  ![](C:\Users\user\Documents\SAS no 4\2.PNG)

* Setelah setting wordpress nano hosts, maka step selanjutnya yaitu setting nano installwordpress.yml

  ```markdown
  nano installwordpress.yml
  ```

  ```markdown
  ---
  - hosts: all
    vars:
      domain: 'lxc_php7.dev'
    tasks:
     - name: delete apt chache
       become: yes
       become_user: root
       become_method: su
       command: rm -vf /var/lib/apt/lists/*
  
     - name: install requirement
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
        - php7.4-curl
  
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
       copy:
        src=~/ansible/wordpress/wp.conf
        dest=/var/www/html/blog/wp-config.php
  
     - name: copy wordpress.conf
       copy:
        src=~/ansible/wordpress/wordpress.conf
        dest=/etc/nginx/sites-available/{{ domain }}
       vars:
        servername: '{{ domain }}'
  
     - name: Symlink wordpress.conf
       command: ln -sfn /etc/nginx/sites-available/{{ domain }} /etc/nginx/sites-enabled/{{ domain }}
     
     - name: restart nginx
       become: yes
       become_user: root
       become_method: su
       action: service name=nginx state=restarted
  
     - name: Write {{ domain }} to /etc/hosts
       lineinfile:
        dest: /etc/hosts
        regexp: '.*{{ domain }}$'
        line: "127.0.0.1 {{ domain }}"
        state: present
  
     - name: enable module php mbstring
       command: phpenmod mbstring
  
     - name: restart php
       become: yes
       become_user: root
       become_method: su
       action: service name=php7.4-fpm state=restarted
  
     - name: restart nginx
       become: yes
       become_user: root
       become_method: su
       action: service name=nginx state=restarted
  
  ```

  ![](C:\Users\user\Documents\SAS no 4\3.PNG)

* Lalu, langkah selanjutnya yaitu setting nano wp.conf

  ```markdown
  nano wp.conf
  ```

  ```markdown
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
  
  define( 'WP_HOME', 'http://vm.local/blog' );
  define( 'WP_SITEURL', 'http://vm.local/blog' );
  
  // * MySQL settings - You can get this info from your web host * //
  /** The name of the database for WordPress */
  define( 'DB_NAME', 'blog' );
  
  /** MySQL database username */
  define( 'DB_USER', 'admin' );
  
  /** MySQL database password */
  define( 'DB_PASSWORD', 'SysAdminSas0102' );
  
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
   * the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}.
   *
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
  
  /*#@-/
  
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
          define( 'ABSPATH', _DIR_ . '/' );
  }
  
  /** Sets up WordPress vars and included files. */
  require_once ABSPATH . 'wp-settings.php';
  
  ```

  ![](C:\Users\user\Documents\SAS no 4\4.PNG)

* Setelah setting di nano wp.conf, maka langkah selanjutnya yaitu setting di nano wordpress.conf

  ```markdown
  nano wordpress.conf
  ```

  ```markdown
  server {
       listen 80;
       listen [::]:80;
  
       # Log files for Debugging
       access_log /var/log/nginx/wordpress-access.log;
       error_log /var/log/nginx/wordpress-error.log;
  
       # Webroot Directory for Laravel project
       root /var/www/html/blog;
       index index.php index.html index.htm;
  
       # Your  Name
       server_name lxc_php7.dev;
  
       location / {
               try_files $uri $uri/ /index.php?$query_string;
       }
  
       # PHP-FPM Configuration Nginx
       location ~ \.php$ {
               try_files $uri =404;
               fastcgi_split_path_info ^(.+\.php)(/.+)$;
               fastcgi_pass unix:/run/php/php7.4-fpm.sock;
               fastcgi_index index.php;
               fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
               include fastcgi_params;
       }
  }
  
  ```

  ![](C:\Users\user\Documents\SAS no 4\5.PNG)

* Setelah setting di nano wordpress.conf, maka step selanjutnya yaitu mencoba memanggil hosts installwordpress.yml

  ```markdown
  sudo ansible-playbook -i hosts installwordpress.yml -k
  ```

  ![](C:\Users\user\Documents\SAS no 4\6.PNG)

* Setelah ansible playbook installwordpress.yml berhasil dijalankan, maka step terakhir yaitu akses url vm.local/blog

  ![](C:\Users\user\Documents\SAS no 4\7.PNG)

* Coba sign in atau membuat akun wordpress yang berisi title (judul), username dan juga password

  ![](C:\Users\user\Documents\SAS no 4\8.PNG)

* Setelah itu kita coba login wordpress dengan username dan password yang sudah dibuat tadi

![](C:\Users\user\Documents\SAS no 4\9.PNG)

* Setelah login, maka akan terdapat tampilan dashboard wordpress seperti gambar dibawah ini
* ![](C:\Users\user\Documents\SAS no 4\10.PNG)

