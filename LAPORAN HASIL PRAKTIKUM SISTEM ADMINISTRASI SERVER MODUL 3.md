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

![1](https://user-images.githubusercontent.com/26424175/147068332-e0f1e0f1-dc31-4ae8-922d-5fff356a456c.PNG)

* Run or install ansible playbook larav.yml

  ```markdown
  ansible-playbook -i hosts larav.yml -k
  ```

![2](https://user-images.githubusercontent.com/26424175/147068343-26ceece7-0a84-43f0-a72a-826f6d3e191c.PNG)

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

![3](https://user-images.githubusercontent.com/26424175/147068347-7e555816-42d1-4356-87b7-4984d23c4108.PNG)

* Run or install ansible playbook config2.yml

  ```markdown
  ansible-playbook -i hosts config2.yml -k
  ```

![4](https://user-images.githubusercontent.com/26424175/147068351-c3976032-a9f7-4158-9ab9-a5438347019d.PNG)

* Add this in file hosts

  ```markdown
  dev.vm.local
  10.0.3.103	dev.vm.local	
  ```

![5](https://user-images.githubusercontent.com/26424175/147068359-a8c126e2-8ed0-4a37-a3d5-80b98a42e329.PNG)

* Log in to root ubuntulanding then edit vm.local

  ```markdown
  ssh root@lxc_landing.dev
  ```

![6](https://user-images.githubusercontent.com/26424175/147068371-d22555d2-85e5-4a9f-b973-1ba228de0833.PNG)

* Write in vm.local, then add line www

  ```markdown
  nano /var/www/html/dev/landing/vm.local
  ```

![7](https://user-images.githubusercontent.com/26424175/147068376-955615ea-ceb7-456c-a5a2-36d375912c30.PNG)

* The next step is edit vm.local. Add dev.vm.local

  ```markdown
  nano /etc/nginx/sites-enabled/vm.local
  dev.vm.local
  ```

![8](https://user-images.githubusercontent.com/26424175/147068383-2600213b-cc21-4a2c-b4b0-71cb2be16317.PNG)

* Edit file vm.local in directory bind. Add line dev

![9](https://user-images.githubusercontent.com/26424175/147068385-ab7e779f-8b53-43aa-a7b5-86c62777e7c2.PNG)

* For the last step, do a restart for all services.

  ```markdown
  sudo service bind9 restart
  sudo service nginx restart
  sudo /etc/init.d/named restart
  ```

![10](https://user-images.githubusercontent.com/26424175/147068397-52d64e65-6e0e-4142-95db-015a0b13fac0.PNG)

* To check your configuration, open the browser and search for dev.vm.local and dev.vm.local/blog

![11](https://user-images.githubusercontent.com/26424175/147068406-11d7da9a-f05e-4a9a-b0c8-de978f5c4fcc.PNG)

![12](https://user-images.githubusercontent.com/26424175/147068415-4f0bd03f-3c09-4f56-9924-a9ebc008b17f.PNG)
