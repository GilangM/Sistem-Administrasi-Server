# UJIAN TENGAH SEMESTER SISTEM ADMINISTRASI SERVER

Nama	: Gilang Maulana

NIM	   : 1202190011

Kelas	 : IT 02 02



1. ### Instalasi Windows Server 2022

   *Buka  Virtual Box dan create machine dan setting seperti gambar di bawah ini*

  ![1](https://user-images.githubusercontent.com/26424175/143666701-889f90d7-7cf9-4234-95a8-fb3ab07209f6.PNG)

   *Kemudian setting memori dengan kapasitas 4GB atau 4096MB* 

   ![2](https://user-images.githubusercontent.com/26424175/143666703-cfed8e8f-783c-48f7-be08-dd11d40a76ee.PNG)

   *Create VHD*

  ![4](https://user-images.githubusercontent.com/26424175/143666719-41b4dd42-574d-4173-a7cf-90d51aa5bf1e.PNG)

  ![5](https://user-images.githubusercontent.com/26424175/143666725-5479738c-b9b0-4cfc-b1d6-2a8119095fe6.PNG)

   *Setting VHD dengan kapasitas 50 GB*

   ![6](https://user-images.githubusercontent.com/26424175/143666728-4031b451-276a-425c-a45a-0b3d8662b2de.PNG)

   *Masuk ke setting > network dan ubah NAT menjadi Bridge 

![7](https://user-images.githubusercontent.com/26424175/143666741-28fe94f2-7317-49b6-97ea-eabe158d28fd.PNG)

*Klik start dan pilih file ISO yang sudah di download*

![8](https://user-images.githubusercontent.com/26424175/143666765-2fd52813-892f-49d9-8825-d73fea6ecbc0.PNG)

*setting bahasa, waktu dan jenis keyboard*

![9](https://user-images.githubusercontent.com/26424175/143666767-34006d9c-aecf-4db4-88c6-8ba4f72a2eb3.PNG)

*Kemudian klik Install Now*

![10](https://user-images.githubusercontent.com/26424175/143666770-fbe6e073-5396-4936-9e8f-7e213ede3ef7.PNG)

*setelah itu pilih Windows Server 2022 Datacenter Evaluation (Desktop Experience)*

![11](https://user-images.githubusercontent.com/26424175/143666924-81f15b7a-d5d8-4c09-a81b-1fcebb26c39a.PNG)

*Klik next*

![12](https://user-images.githubusercontent.com/26424175/143666928-8c10e47e-edbe-4122-977e-0e1ed69f36c8.PNG)

*Pilih Custom: Install Microsoft Server Operating System Only (advanced)*

![13](https://user-images.githubusercontent.com/26424175/143666929-99d20bcd-693a-4586-b3b5-2243a6c3f42c.PNG)
*Klik Drive 0 lalu Klik Next*

![14](https://user-images.githubusercontent.com/26424175/143666931-058c79f0-037f-4cca-9121-def26fd46acf.PNG)

*Tunggu Proses instalasi sampai selesai*

![15](https://user-images.githubusercontent.com/26424175/143666933-87dbba9e-84a4-4b67-b3cb-cc0da57370b5.PNG)

*Setelah proses install sudah selesai akan tampil seperti gambar dibawah ini*

![16](https://user-images.githubusercontent.com/26424175/143666940-00562318-3b17-4716-b4d6-00e0e040f909.PNG)

*Setelah selesai buat password untuk login windows server 2022 *

![17](https://user-images.githubusercontent.com/26424175/143666946-a69915e5-650f-455c-a498-71825f2a8965.PNG)

*Setelah selesai membuat password pergi ke input > keyboard > insert ctrl-alt-del, lalu masukkan password yang sudah di buat tadi*

![18](https://user-images.githubusercontent.com/26424175/143666948-227518ff-44a3-44cf-aa6c-b4dc131a32b0.PNG)

*Pergi ke device > insert guest addtions CD image lalu ke file explorer > CD Drive Virtual Box > lalu pilih vBox WindowsAddtions *

![19](https://user-images.githubusercontent.com/26424175/143666954-d8fedc93-a5fd-41bd-897a-b874b681e12e.PNG)

*Lakukan proses instalasi sebagai berikut*

![20](https://user-images.githubusercontent.com/26424175/143666958-ff2b35d8-a367-46b4-a684-57df7d8cca37.PNG)

![21](https://user-images.githubusercontent.com/26424175/143666960-b7e79451-dca9-48c3-aef9-dd26a6d578c1.PNG)

![22](https://user-images.githubusercontent.com/26424175/143666962-e368bf50-aa61-4281-80ac-2d10bf50eb37.PNG)

*Lalu reboot now*

![23](https://user-images.githubusercontent.com/26424175/143667050-29362bbb-bdc7-4244-8072-25fc8492f069.PNG)

*pergi ke input > keyboard > insert ctrl-alt-del*

![24](https://user-images.githubusercontent.com/26424175/143666966-3e9e434f-6f65-4fa4-abae-e738cca65348.PNG)

### 2. Instalasi Active Directory Domain Server

*Ubah nama computer di windows powershell dengan mengetik > “rename-computer -Newname Server2022”*

![25](https://user-images.githubusercontent.com/26424175/143666967-2d7e6c4c-2afa-40eb-b172-9f605b47d7fe.PNG)

*Kemudian masuk ke server manager pilih menu manage* 

![26](https://user-images.githubusercontent.com/26424175/143666974-2647b5fe-8a1b-4191-bd11-12514844d276.PNG)

*Setelah itu pilih Add Roles and Features dan next*

![27](https://user-images.githubusercontent.com/26424175/143666979-6ae22045-4de2-465d-b6d7-769567e8ea02.PNG)

*Pilih Role-Based or feature-based installation kemudian next*

![28](https://user-images.githubusercontent.com/26424175/143666981-1f6c6f4d-c322-4391-8575-00a57836a39e.PNG)

*Setelah itu pilih select a server from the server pool
Lalu pilih active directory domain server*

![29](https://user-images.githubusercontent.com/26424175/143666982-035acfe3-edf9-4cd6-9d11-3cab2be9e3f6.PNG)

*Kemudain klik add features*

![30](https://user-images.githubusercontent.com/26424175/143666984-ff743f2d-6d53-4044-8aec-727db835870e.PNG)

*Kemudian ke features lalu centang Group Policy Management dan next*

![31](https://user-images.githubusercontent.com/26424175/143667080-fd649e5e-f1c0-47d6-97f4-e65aa228ebeb.PNG)

*Kemudian install*

![32](https://user-images.githubusercontent.com/26424175/143667082-1f71cecd-c8ab-41ec-9f05-4253ce0b97d1.PNG)

*Setting ip static di cmd menggunakan command> sconfig*

![34](https://user-images.githubusercontent.com/26424175/143667084-9eb4059b-9766-40f3-968d-7ad3856e0bef.PNG)

![35](https://user-images.githubusercontent.com/26424175/143667085-41a23ced-dd35-436b-a9b0-53aa3358b67a.PNG)

![36](https://user-images.githubusercontent.com/26424175/143667087-c7296a51-f62b-4ca1-9660-18b2b0b5605f.PNG)

![37](https://user-images.githubusercontent.com/26424175/143667091-fb3b5798-4ef6-4844-9c18-96f54e17556d.PNG)

### 3. Instalasi DNS Server

*Instal DNS Server seperti pada gambar*

![38](https://user-images.githubusercontent.com/26424175/143667094-3b8ee91e-711c-4fa4-b0e6-77483c464b76.PNG)

![39](https://user-images.githubusercontent.com/26424175/143667095-fad756e3-7dac-4bc7-b998-f5ab235536d6.PNG)

![40](https://user-images.githubusercontent.com/26424175/143667096-da9e0aa4-f905-41ff-b260-3e1c272cb797.PNG)

![41](https://user-images.githubusercontent.com/26424175/143667099-88c68ba9-1c79-412c-a7ce-8cc25f7c97c9.PNG)

![42](https://user-images.githubusercontent.com/26424175/143667103-efb7020e-18db-4124-9208-d6dfa74660e2.PNG)

![43](https://user-images.githubusercontent.com/26424175/143667104-96a5acf8-4e21-4c10-af39-905cb87175c7.PNG)

![44](https://user-images.githubusercontent.com/26424175/143667106-5dfc2cbb-cfc5-4d52-8796-ab133c9bc931.PNG)

![45](https://user-images.githubusercontent.com/26424175/143667109-00e97c70-9dd9-4544-a862-457b1d39f094.PNG)

### 4. Instalasi NET FRAMEWORK 3.5

![46](https://user-images.githubusercontent.com/26424175/143667111-24922e43-1136-4ba3-8e04-ad0e75a547f7.PNG)

### 5. Promote Server  To a Domain

*Kemudian Promote Server to a Domain Controller dengan menekan tanda seru*

![47](https://user-images.githubusercontent.com/26424175/143667112-22251fbc-f16c-4290-99bb-f8c030f388ad.PNG)

*Pilih add new forest dan beri nama*

![48](https://user-images.githubusercontent.com/26424175/143667116-77532d37-5979-44d5-b457-780093ae4058.PNG)

*Kemudian isi Password*

![49](https://user-images.githubusercontent.com/26424175/143667119-4f85ab10-7a92-4f54-85a9-55412de222b6.PNG)

*Klik Next*

![50](https://user-images.githubusercontent.com/26424175/143667125-37246149-4f6a-4d6b-841d-6aab7f17304e.PNG)

![51](https://user-images.githubusercontent.com/26424175/143667129-83c53a9f-09c2-47cb-afd2-43b9f45b1227.PNG)

![52](https://user-images.githubusercontent.com/26424175/143667134-17b3f796-b37c-4e6f-9e39-75395596793f.PNG)

![53](https://user-images.githubusercontent.com/26424175/143667137-771479c4-dd74-43dc-aae0-db34c5289aca.PNG)

*Kemudian Install*

![54](https://user-images.githubusercontent.com/26424175/143667146-06d9c580-7e96-4e20-8ab6-e66fc92dfa2c.PNG)

*Setelah close Windows Server akan restart dan akan berganti nama*

![55](https://user-images.githubusercontent.com/26424175/143667155-210d8178-3f68-4920-8741-97682452f8d5.PNG)

*Lakukan pengecekan konfigurasi pada command prompt untuk mengetahui kesuksesan installasi*

![56](https://user-images.githubusercontent.com/26424175/143667158-f2b4f3e5-adbb-4627-a928-c913325c3895.PNG)

*Kemudian cek ip address di network*

![57](https://user-images.githubusercontent.com/26424175/143667161-761764d9-56d9-4fd8-a0fd-bc3de08d8977.PNG)
