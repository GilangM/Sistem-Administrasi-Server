# Laporan Hasil Praktikum Sistem Administrasi Server

1. Pertama Rename ubuntu_php5.6 menjadi ubuntu_landing terlebih dahulu

   ```markdown
   sudo lxc-copy -R ubuntu_php5.6 name -N ubuntu_landing
   ```

   

   ![1](E:\KULIAH\Semester 5\Sistem Administrasi Server\ss prak sas\ss prak sas\1.PNG)

* kemudian jalankan container 

```markdown
sudo lxc-start -n ubuntu_landing -d
sudo lxc-attach -n ubuntu_landing
```

![image-20211023214202061](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023214202061.png)

* Ganti IP yang terdapat di ubuntu_landing

  ```markdown
  nano /etc/network/interfaces
  ```

  ![image-20211023214408842](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023214408842.png)

* lakukan Reboot dan pastikan IP telah terganti

  ```markdown
  reboot
  ```

  ![image-20211023214517408](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023214517408.png)

* Lakukan ping google.com dan pastikan berhasil

  ```markdown
  ping google.com
  ```

  ![image-20211023214939066](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023214939066.png)



2. install lxc debian 9 dengan nama debian_php5.6

* create debian_php5.6 

  ```markdown
  sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-
  ```

![WhatsApp Image 2021-10-24 at 8.43.02 PM](C:\Users\user\Downloads\WhatsApp Image 2021-10-24 at 8.43.02 PM.jpeg)

* Download debian_php5.6 telah berhasil

  ```markdown
  sudo lxc-ls -f (untuk cek container)
  ```

  ![image-20211023215521262](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023215521262.png)

* Start debian_php5.6

```markdown
sudo lxc-start -n debian_php5.6 -d
sudo lxc-attach -n debian_php5.6
```

![image-20211023215702181](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023215702181.png)



3. setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev , buat halaman index.html yang menerangkan informasi nama lxc

* Lakukan penginstallan net-tools pada debian_php5.6

  ```markdown
  apt install nano net-tools curl –y
  ```

  ![image-20211023220029677](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023220029677.png)

* Lakukan setting ip debian_php5.6 

  ```markdown
  nano /etc/network/interfaces
  ```

  ![image-20211023220220242](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023220220242.png)

* Ip pada debian_php5.6 telah berhasil di install

  ```markdown
  ifconfig
  ```

  ![image-20211023220333620](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023220333620.png)

* Lakukan penginstallan nginx pada debian_php5.6

  ```markdown
  apt install nginx nginx-extras –y
  ```

  ![image-20211023220757404](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023220757404.png)

* Lakukan setting nginx

  ```markdown
  cd /etc/nginx/sites-available
  touch lxc_php5.6.dev
  nano lxc_php5.6.dev
  ```

  ![image-20211023220905545](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023220905545.png)

* Setting nginx 

  ```markdown
  cd ../sites-enabled
  ln -s /etc/nginx/sites-available/lxc_php5.6.dev 
  nginx -t
  nginx -s reload
  ```

  ![image-20211023221009402](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023221009402.png)

* Lakukan setting hosts 

  ```markdown
  nano /etc/hosts
  ```

  ![image-20211023221052210](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023221052210.png)

* Lakukan setting index.html debian_php5.6 

  ```markdown
  lxc-attach -n debian_php5.6
  cd /var/www/html
  mkdir lxc_php5.6
  cp index.nginx-debian.html lxc_php5.6/index.html
  cd lxc_php5.6/
  ```

  ![WhatsApp Image 2021-10-24 at 8.43.01 PM](C:\Users\user\Downloads\WhatsApp Image 2021-10-24 at 8.43.01 PM.jpeg)

* Tambah file index.html 

  ```
  nano index.html
  ```

  ![image-20211023221246290](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023221246290.png)

* Setelah curl -I 

  ```
  curl -i http://lxc_php5.dev 
  ```

  ![image-20211023221337189](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023221337189.png)



4. setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev , buat halaman index.html yang menerangkan informasi nama lxc

* masuk ke ubuntu_landing

```markdown
sudo lxc-attach -n ubuntu_landing
cd /etc/nginx/sites-available/
nano lxc_php5.6.dev
```

![WhatsApp Image 2021-10-24 at 8.48.17 PM](C:\Users\user\Downloads\WhatsApp Image 2021-10-24 at 8.48.17 PM.jpeg)

* Lakukan setting lxc_landing 

![image-20211023221758790](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023221758790.png)

* Setting hosts landing

  ```markdown
  cd ../sites-enabled
  rm lxc_php5.6.dev
  ln -s /etc/nginx/sites-available/lxc_php5.6.dev
  nginx -t
  nginx -s reload
  nano /etc/hosts
  ```

  ![image-20211023222008181](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023222008181.png)

![image-20211023222016360](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023222016360.png)

* Masuk ke index.html

  ```markdown
  cd /var/www/html/
  nano index.html
  ```

  ![image-20211023222107799](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023222107799.png)

* setting file index landing

![image-20211023222156663](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023222156663.png)

* Curl I lxc landing

  ```markdown
  curl -i http://lxc_landing.dev 
  ```

  ![image-20211023222332565](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023222332565.png)



5. LXC ubuntu_landing harus auto start ketika vm dinyalakan, hal ini digunakan untuk menjaga agar website company profile tidak mengalami downtime

* Auto start

  ```markdown
  lxc-ls -f
  echo “lxc.start.auto =1” >> /var/lib/lxc/ubuntu_landing/config
  lxc-ls –f
  ```

  ![image-20211023222834240](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023222834240.png)



6.  setup nginx pada vm.local untuk mengatur *proxy_pass* 

* Setting hosts vm.local 

  ```markdown
  sudo nano /etc/hosts
  ```

  ![image-20211023223017247](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023223017247.png)

* Start ubuntu_php7.4

  ```markdown
  sudo lxc-start -n ubuntu_php7.4
  sudo lxc-start -n ubuntu_php5.6
  lxc-ls –f
  ```

  ![image-20211023223508071](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023223508071.png)

* Masuk vm.local

  ```markdown
  cd /etc/nginx/sites-available/
  sudo nano vm.local
  ```

  ![WhatsApp Image 2021-10-24 at 8.56.22 PM](C:\Users\user\Downloads\WhatsApp Image 2021-10-24 at 8.56.22 PM.jpeg)

* Setting vm.local

![image-20211023224358845](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023224358845.png)

* Curl vm.local

  ```markdown
  cd ../sites-enabled/
  sudo ln /etc/nginx/sites-available/vm.local
  sudo nginx -t
  sudo nginx -s reload
  curl -I http://vm.local
  ```

  ![image-20211023224633386](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023224633386.png)



7. hasil mengakses ketiga url

   * mengakses http://vm.local/app akan diartahkan ke http://lxc_php5.dev

   ![image-20211023224833174](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023224833174.png)

*  mengakses http://vm.local/blog akan diarahkan ke http://lxc_php7.dev![image-20211023224854533](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023224854533.png)                

*  mengakses http://vm.local akan diarahkan ke http://lxc_landing.dev![image-20211023224909283](C:\Users\user\AppData\Roaming\Typora\typora-user-images\image-20211023224909283.png)

 

8. Menyiapkan analisa untuk diserahkan ke CTO

   * Mengapa untuk kebutuhan php5.6 tidak bisa menggunakan ubuntu 16.04, sehingga perlu diganti os ke debian 9?

     Jawab:

     * ubuntu 16.04 xenial akan mencapai masa kadaluwarsanya atau end of support system dan hanya akan tersedia sebagai opsi berbayar melalui fitur tambahan keamanan ubuntu

   * Kenapa harus menggunakan virtualisasi LXC pada skema website yang akan didevelop?

     Jawab: 

     * Karena LXC menyediakan virtualisasi tingkat sistem operasi, itu bukan melalui mesin virtual yang penuh, tetapi ia menyediakan lingkungan virtualnya sendiri yang memiliki proses dan ruang jaringan sendiri.

   * Apa yang dimaksud dengan proxy server? kenapa vm.local bisa kita anggap sebagai proxy server?

     Jawab:

     * Proxy merupakan sistem yang memungkinkan pengguna mengakses jaringan internet menggunakan IP yang berbeda dengan yang diterima perangkat. Proxy server itu sendiri merupakan sebuah perangkat yang digunakan untuk menyediakan layanan proxy.
     * Vm local memiliki fungsi yang tidak jauh berbeda dengan server fisik, vm local mampu membuat banyak server. Pembuatan server virtual menggunakan teknologi proxy server untuk memblokir ataupun mengontrol aktivitas jaringan

