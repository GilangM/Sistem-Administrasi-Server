## Report Module 4

From Group 5 [ IT 02 02]

Gilang Maulana 1202190011 | Dinda Tresna Teja Nirwana 1202190050

* Make 2 copies of ubuntu_php7.4

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\1.PNG)

* after that start both containers

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\2.PNG) 

* Go to ubuntu_php7.4_2 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\3.PNG)

* change ip address ubuntu_php7.4_2  to 10.0.3.111 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\4.PNG)

* go to etc/hosts then add lxc_php7_2.dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\5.PNG)

* After that go to /etc/nginx/sites-available/lxc_php7.dev then change server name 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\6.PNG)

* restart nginx

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\7.PNG)

* try accesing lxc_php7_2.dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\8.PNG)

* Go to ubuntu_php7.4_3

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\9.PNG)

* change ip address ubuntu_php7.4_3  to 10.0.3.151 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\10.PNG)

* after that restart network lxc

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\11.PNG)

* go to etc/hosts then add lxc_php7_3.dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\12.PNG)

* After that go to /etc/nginx/sites-available/lxc_php7.dev then change server name 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\13.PNG)

* restart nginx

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\7.PNG)

* try accesing lxc_php7_3.dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\14.PNG)

* Make 2 copies of debian_php5.6 and start both containers

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\15.PNG)

* Go to debian_php5.6_2 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\16.PNG)

* change ip address debian_php5.6_2  to 10.0.3.112 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\17.PNG)

* go to etc/hosts then add lxc_php5_2.dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\18.PNG)

* After that go to /etc/nginx/sites-available/lxc_php5.dev then change server name 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\19.PNG)

* restart and try accesing lxc_php5_2.dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\20.PNG)

* 

* Go to debian_php5.6_3

  ```markdown
  sudo lxc-attach -n debia_php5.6_3
  ```

  

* change ip address debian_php5.6_2  to 10.0.3.122 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\21.PNG)

* go to etc/hosts then add lxc_php5_3.dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\22.PNG)

* After that go to /etc/nginx/sites-available/lxc_php5.dev then change server name 

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\23.PNG)

* restart and try accesing lxc_php5_3.dev

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\24.PNG)

* Register all new containers in /etc/hosts (on vm)

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\25.PNG)

* Run the jmeter. change the number of threads from user access from 50,100,150

  * user access 50

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (349).png)

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (350).png)

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (351).png)

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (352).png)

  * User Access 100

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (353).png)

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (354).png)

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (355).png)

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (356).png)

  * user access 150

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (357).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (358).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (359).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (360).png)

* back to vm and go to 

  ```markdown
  sudo nano /etc/nginx/sites-available/vm.local
  ```

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\28.PNG)

* change proxy pass

  ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\29.PNG)

* go back to jmeter

  * user access 50

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (361).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (362).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (363).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (364).png)

  * user access 100

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (365).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (366).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (367).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (368).png)

  * user access 150

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (369).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (370).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (371).png)

    ![](E:\KULIAH\Semester 5\Sistem Administrasi Server\SS MODUL 4\Screenshot (372).png)

