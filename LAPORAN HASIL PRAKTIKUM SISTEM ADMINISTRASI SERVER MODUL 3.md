# LAPORAN HASIL PRAKTIKUM SISTEM ADMINISTRASI SERVER MODUL 3

#### Create subdomain dev.vm.local use ansible and there are some rules:

 a) Use ansible

 b) Use same lxc which is used by vm.local

 c) The folder code must be in /var/www/html/dev/{nama_app}

* Create a new file sublaravel.yml in directory ansible/laravel

  ``` markdown
  nano larav.yml
  ```

  ```markdown
  ---
  - hosts: all
    become : yes
    tasks:
      - name: install bind9 dan dnsutils
        apt:
         pkg:
           - bind9
           - dnsutils
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\1.PNG)

* Run or install ansible playbook larav.yml

  ```markdown
  ansible-playbook -i hosts larav.yml -k
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\2.PNG)

* Create a new file config2.yml

  ```markdown
  nano config2.yml 
  ```

  ```markdown
  ---
  - hosts: all
    become : yes
    tasks:
     - name: membuat direktori
       file:
        path: /var/www/html/dev/landing
        state: directory
     - name: copy file vm.local
       copy:
        src: /etc/bind/vm/vm.local
        dest: /var/www/html/dev/landing
     - name: mengganti konfigurasi
       replace:
        path: /var/www/html/dev/landing/vm.local
        regexp: 'www'
        replace: 'dev'
     - name: copy file named.conf.local
       copy:
        src: /etc/bind/named.conf.local
        dest: /etc/bind/named.conf.local
     - name: mengganti konfigurasi conf local
       replace:
        path: /etc/bind/named.conf.local
        regexp: '/etc/bind/vm/vm.local'
        replace: '/var/www/html/dev/landing/vm.local'
     - name: mengganti konfigurasi conf local part2
       replace:
        path: /etc/bind/named.conf.local
        regexp: '/etc/bind/vm/1.168.192.in-addr.arpa'
        replace: '/var/www/html/dev/landing/1.168.192.in-addr.arpa'
     - name: copy file 1.168.192.in-addr.arpa
       copy:
        src: /etc/bind/vm/1.168.192.in-addr.arpa
        dest: /var/www/html/dev/landing
     - name: copy file resolv.conf
       copy:
        src: /etc/resolv.conf
        dest: /etc/resolv.conf
     - name: copy file named.conf.options
       copy:
        src: /etc/bind/named.conf.options
        dest: /etc/bind/named.conf.options
     - name: restart nginx
       service:
        name: nginx
        state: restarted
     - name: restart bind9
       action: service name=bind9 state=restarted
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\3.PNG)

* Run or install ansible playbook config2.yml

  ```markdown
  ansible-playbook -i hosts config2.yml -k
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\4.PNG)

* Add this in file hosts

  ```markdown
  dev.vm.local
  10.0.3.103	dev.vm.local	
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\5.PNG)

* Log in to root ubuntulanding then edit vm.local

  ```markdown
  ssh root@lxc_landing.dev
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\6.PNG)

* Write in vm.local, then add line www

  ```markdown
  nano /var/www/html/dev/landing/vm.local
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\7.PNG)

* The next step is edit vm.local. Add dev.vm.local

  ```markdown
  nano /etc/nginx/sites-enabled/vm.local
  dev.vm.local
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\8.PNG)

* Edit file vm.local in directory bind. Add line dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\9.PNG)

* For the last step, do a restart for all services.

  ```markdown
  sudo service bind9 restart
  sudo service nginx restart
  sudo /etc/init.d/named restart
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\10.PNG)

* To check your configuration, open the browser and search for dev.vm.local and dev.vm.local/blog

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\11.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak 4\12.PNG)