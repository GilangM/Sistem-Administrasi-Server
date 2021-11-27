# UJIAN TENGAH SEMESTER SISTEM ADMINISTRASI SERVER

Nama	: Gilang Maulana

NIM	   : 1202190011

Kelas	 : IT 02 02



1. ### Instalasi Windows Server 2022

   *Buka  Virtual Box dan create machine dan setting seperti gambar di bawah ini*

   ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\1.PNG)

   *Kemudian setting memori dengan kapasitas 4GB atau 4096MB* 

   ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\2.PNG)

   *Create VHD*

   ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\4.PNG)

   ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\5.PNG)

   *Setting VHD dengan kapasitas 50 GB*

   ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\6.PNG)

   *Masuk ke setting > network dan ubah NAT menjadi Bridge 

   ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\7.PNG)

*Klik start dan pilih file ISO yang sudah di download*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\8.PNG)

*setting bahasa, waktu dan jenis keyboard*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\9.PNG)

*Kemudian klik Install Now*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\10.PNG)

*setelah itu pilih Windows Server 2022 Datacenter Evaluation (Desktop Experience)*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\11.PNG)

*Klik next*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\12.PNG)

*Pilih Custom: Install Microsoft Server Operating System Only (advanced)*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\13.PNG)

*Klik Drive 0 lalu Klik Next*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\14.PNG)

*Tunggu Proses instalasi sampai selesai*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\15.PNG)

*Setelah proses install sudah selesai akan tampil seperti gambar dibawah ini*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\16.PNG)

*Setelah selesai buat password untuk login windows server 2022 *

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\17.PNG)

*Setelah selesai membuat password pergi ke input > keyboard > insert ctrl-alt-del, lalu masukkan password yang sudah di buat tadi*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\18.PNG)

*Pergi ke device > insert guest addtions CD image lalu ke file explorer > CD Drive Virtual Box > lalu pilih vBox WindowsAddtions *

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\19.PNG)

*Lakukan proses instalasi sebagai berikut*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\20.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\21.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\22.PNG)

*Lalu reboot now*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\23.PNG)

*pergi ke input > keyboard > insert ctrl-alt-del*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\24.PNG)

### 2. Instalasi Active Directory Domain Server

*Ubah nama computer di windows powershell dengan mengetik > “rename-computer -Newname Server2022”*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\25.PNG)

*Kemudian masuk ke server manager pilih menu manage* 

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\26.PNG)

*Setelah itu pilih Add Roles and Features dan next*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\27.PNG)

*Pilih Role-Based or feature-based installation kemudian next*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\28.PNG)

*Setelah itu pilih select a server from the server pool
Lalu pilih active directory domain server*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\29.PNG)

*Kemudain klik add features*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\30.PNG)

*Kemudian ke features lalu centang Group Policy Management dan next*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\31.PNG)

*Kemudian install*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\32.PNG)

*Setting ip static di cmd menggunakan command> sconfig*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\34.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\35.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\36.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\37.PNG)

### 3. Instalasi DNS Server

*Instal DNS Server seperti pada gambar*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\38.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\39.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\40.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\41.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\42.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\43.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\44.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\45.PNG)

### 4. Instalasi NET FRAMEWORK 3.5

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\46.PNG)

### 5. Promote Server  To a Domain

*Kemudian Promote Server to a Domain Controller dengan menekan tanda seru*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\47.PNG)

*Pilih add new forest dan beri nama*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\48.PNG)

*Kemudian isi Password*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\49.PNG)

*Klik Next*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\50.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\51.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\52.PNG)

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\53.PNG)

*Kemudian Install*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\54.PNG)

*Setelah close Windows Server akan restart dan akan berganti nama*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\55.PNG)

*Lakukan pengecekan konfigurasi pada command prompt untuk mengetahui kesuksesan installasi*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\56.PNG)

*Kemudian cek ip address di network*

![](E:\KULIAH\Semester 5\Sistem Administrasi Server\UTS\57.PNG)