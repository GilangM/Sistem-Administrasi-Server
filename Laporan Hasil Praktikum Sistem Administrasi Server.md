# Laporan Hasil Praktikum Sistem Administrasi Server

1. Pertama Rename ubuntu_php5.6 menjadi ubuntu_landing terlebih dahulu

   ```markdown
   sudo lxc-copy -R ubuntu_php5.6 name -N ubuntu_landing
   ```

   

  ![1](https://user-images.githubusercontent.com/26424175/138599359-4c80e261-9340-4726-978b-0b66d18f8ea3.PNG)

* kemudian jalankan container 

```markdown
sudo lxc-start -n ubuntu_landing -d
sudo lxc-attach -n ubuntu_landing
```

![2](https://user-images.githubusercontent.com/26424175/138599813-8199a121-8052-4ee9-920f-cf272d9d2d05.PNG)

* Ganti IP yang terdapat di ubuntu_landing

  ```markdown
  nano /etc/network/interfaces
  ```

  ![3](https://user-images.githubusercontent.com/26424175/138599892-31883b29-fa2b-4c11-b63a-676172aa670f.PNG)
  

* lakukan Reboot dan pastikan IP telah terganti

  ```markdown
  reboot
  ```

![4](https://user-images.githubusercontent.com/26424175/138599943-4c38bbd5-21e2-40cf-9180-c4b8f74fcc9d.PNG)
* Lakukan ping google.com dan pastikan berhasil

  ```markdown
  ping google.com
  ```

 ![5](https://user-images.githubusercontent.com/26424175/138599947-cbdc433f-5e03-4485-a2ac-6cbbbc6cb1ad.PNG)



2. install lxc debian 9 dengan nama debian_php5.6

* create debian_php5.6 

  ```markdown
  sudo lxc-create -n debian_php5.6 -t download -- --dist debian --release stretch --arch amd64 --force-
  ```

![WhatsApp Image 2021-10-24 at 8 43 02 PM](https://user-images.githubusercontent.com/26424175/138600132-5f61d38d-8c0d-441c-91e9-39b9414d7c86.jpeg)
* Download debian_php5.6 telah berhasil

  ```markdown
  sudo lxc-ls -f (untuk cek container)
  ```

 ![6](https://user-images.githubusercontent.com/26424175/138600176-965c3f74-7047-45dd-97ff-7d3ad7fddee5.PNG)

* Start debian_php5.6

```markdown
sudo lxc-start -n debian_php5.6 -d
sudo lxc-attach -n debian_php5.6
```

![8](https://user-images.githubusercontent.com/26424175/138600183-88da154e-6211-4381-b98e-e9e463cc461f.PNG)



3. setup nginx pada debian_php5.6 untuk domain http://lxc_php5.dev , buat halaman index.html yang menerangkan informasi nama lxc

* Lakukan penginstallan net-tools pada debian_php5.6

  ```markdown
  apt install nano net-tools curl –y
  ```

 ![9](https://user-images.githubusercontent.com/26424175/138600233-7cd37dc4-fdfc-42b3-b59d-365fc1a05e96.PNG)

* Lakukan setting ip debian_php5.6 

  ```markdown
  nano /etc/network/interfaces
  ```

 ![10](https://user-images.githubusercontent.com/26424175/138600249-28f1a2f5-c123-481b-9d7b-be1de071e8a3.PNG)

* Ip pada debian_php5.6 telah berhasil di install

  ```markdown
  ifconfig
  ```

![11](https://user-images.githubusercontent.com/26424175/138600254-f021dc9b-3ee6-4d73-b2ce-7633c27eca61.PNG)

* Lakukan penginstallan nginx pada debian_php5.6

  ```markdown
  apt install nginx nginx-extras –y
  ```

 ![12](https://user-images.githubusercontent.com/26424175/138600524-9822ea6a-959e-4b0f-b082-87940f0b12fa.PNG)

* Lakukan setting nginx

  ```markdown
  cd /etc/nginx/sites-available
  touch lxc_php5.6.dev
  nano lxc_php5.6.dev
  ```

![13](https://user-images.githubusercontent.com/26424175/138600539-43a64e44-d03a-4a5b-828c-7e41ed604954.PNG)


* Setting nginx 

  ```markdown
  cd ../sites-enabled
  ln -s /etc/nginx/sites-available/lxc_php5.6.dev 
  nginx -t
  nginx -s reload
  ```

![14](https://user-images.githubusercontent.com/26424175/138600555-04a69ed0-1b60-4026-b8e3-7f844373ed4b.PNG)

* Lakukan setting hosts 

  ```markdown
  nano /etc/hosts
  ```

 ![15](https://user-images.githubusercontent.com/26424175/138600331-d92318e7-df82-42fa-81c5-b8cd9c66b25f.PNG)

* Lakukan setting index.html debian_php5.6 

  ```markdown
  lxc-attach -n debian_php5.6
  cd /var/www/html
  mkdir lxc_php5.6
  cp index.nginx-debian.html lxc_php5.6/index.html
  cd lxc_php5.6/
  ```

  ![WhatsApp Image 2021-10-24 at 8 43 01 PM](https://user-images.githubusercontent.com/26424175/138600587-34335203-3a5c-46b8-9d1f-dc6c3f78870f.jpeg)

* Tambah file index.html 

  ```
  nano index.html
  ```

  ![17](https://user-images.githubusercontent.com/26424175/138600650-83745d6c-ffaa-4207-969a-f671875b3fde.PNG)
)

* Setelah curl -I 

  ```
  curl -i http://lxc_php5.dev 
  ```

 ![18](https://user-images.githubusercontent.com/26424175/138600690-bc8dd15a-c505-46db-a91a-b9a628bc2aec.PNG)



4. setup nginx pada ubuntu_landing untuk domain http://lxc_landing.dev , buat halaman index.html yang menerangkan informasi nama lxc

* masuk ke ubuntu_landing

```markdown
sudo lxc-attach -n ubuntu_landing
cd /etc/nginx/sites-available/
nano lxc_php5.6.dev
```

![WhatsApp Image 2021-10-24 at 8 48 17 PM](https://user-images.githubusercontent.com/26424175/138600722-508191f9-7a3d-4f23-93c5-0fa121acc71b.jpeg)


* Lakukan setting lxc_landing 

![19](https://user-images.githubusercontent.com/26424175/138600872-2c123a42-d282-44af-be32-5005eca0e271.PNG)

* Setting hosts landing

  ```markdown
  cd ../sites-enabled
  rm lxc_php5.6.dev
  ln -s /etc/nginx/sites-available/lxc_php5.6.dev
  nginx -t
  nginx -s reload
  nano /etc/hosts
  ```

 ![20](https://user-images.githubusercontent.com/26424175/138600906-80fedc6a-9114-4838-888e-d88fc830eb0e.PNG)

![15](https://user-images.githubusercontent.com/26424175/138601011-d25c0de0-26be-447d-83d9-c83432da577d.PNG)

* Masuk ke index.html

  ```markdown
  cd /var/www/html/
  nano index.html
  ```

 ![21](https://user-images.githubusercontent.com/26424175/138601091-1f752a14-c317-4493-b7ba-f9cb20e81a30.PNG)

* setting file index landing

![22](https://user-images.githubusercontent.com/26424175/138601097-a0327deb-d08b-419a-a7a1-59588244c6b1.PNG)

* Curl I lxc landing

  ```markdown
  curl -i http://lxc_landing.dev 
  ```

 ![23](https://user-images.githubusercontent.com/26424175/138601104-1a4e783a-e6db-4f87-852c-3031c86819f5.PNG)


5. LXC ubuntu_landing harus auto start ketika vm dinyalakan, hal ini digunakan untuk menjaga agar website company profile tidak mengalami downtime

* Auto start

  ```markdown
  lxc-ls -f
  echo “lxc.start.auto =1” >> /var/lib/lxc/ubuntu_landing/config
  lxc-ls –f
  ```

  ![24](https://user-images.githubusercontent.com/26424175/138601111-7328d6fb-6ba5-42ed-8bdd-eec34a1d9957.PNG)



6.  setup nginx pada vm.local untuk mengatur *proxy_pass* 

* Setting hosts vm.local 

  ```markdown
  sudo nano /etc/hosts
  ```

![25](https://user-images.githubusercontent.com/26424175/138601116-e1858769-2410-4608-adcf-c42eed19e978.PNG)

* Start ubuntu_php7.4

  ```markdown
  sudo lxc-start -n ubuntu_php7.4
  sudo lxc-start -n ubuntu_php5.6
  lxc-ls –f
  ```

 ![26](https://user-images.githubusercontent.com/26424175/138601135-9d7d3aa2-653c-420a-b72b-8efe10d0db88.PNG)
 
* Masuk vm.local

  ```markdown
  cd /etc/nginx/sites-available/
  sudo nano vm.local
  ```

 ![WhatsApp Image 2021-10-24 at 8 56 22 PM](https://user-images.githubusercontent.com/26424175/138601144-92ded180-5151-4d90-bf94-ecba7389a7ac.jpeg)

* Setting vm.local

![27](https://user-images.githubusercontent.com/26424175/138601225-b54c5756-84ad-43d7-8337-7e4a0223839e.PNG)

* Curl vm.local

  ```markdown
  cd ../sites-enabled/
  sudo ln /etc/nginx/sites-available/vm.local
  sudo nginx -t
  sudo nginx -s reload
  curl -I http://vm.local
  ```

 ![28](https://user-images.githubusercontent.com/26424175/138601237-128f3c6b-9a09-4b50-807c-4108716526bf.PNG)



7. hasil mengakses ketiga url

   * mengakses http://vm.local/app akan diartahkan ke http://lxc_php5.dev
![30](https://user-images.githubusercontent.com/26424175/138601256-4a66b14e-2d14-4ced-96c8-5d40bad1dc4d.PNG)

*  mengakses http://vm.local/blog akan diarahkan ke http://lxc_php7.dev!
![31](https://user-images.githubusercontent.com/26424175/138601264-2e9ec531-4cb9-4d1c-9d2d-540396fd3eff.PNG)

*  mengakses http://vm.local akan diarahkan ke http://lxc_landing.dev!
![32](https://user-images.githubusercontent.com/26424175/138601271-39ff0423-7562-43d9-ab63-13871f58b44f.PNG)
 

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

