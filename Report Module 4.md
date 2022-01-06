## Report Module 4

From Group 5 [ IT 02 02]

Gilang Maulana 1202190011 | Dinda Tresna Teja Nirwana 1202190050

* Make 2 copies of ubuntu_php7.4

![1](https://user-images.githubusercontent.com/26424175/148408860-add5b086-8bd9-4bb5-995b-22d812362781.PNG)

* after that start both containers

![2](https://user-images.githubusercontent.com/26424175/148408875-ca1365d9-adc9-4ce1-9881-139db2b92ebf.PNG)

* Go to ubuntu_php7.4_2 

![3](https://user-images.githubusercontent.com/26424175/148408883-db3d4dbc-194f-4987-8e9d-1d66c544851d.PNG)

* change ip address ubuntu_php7.4_2  to 10.0.3.111 

![4](https://user-images.githubusercontent.com/26424175/148408889-e03ed416-5376-4f2e-97b3-e38f1d0dd974.PNG)

* go to etc/hosts then add lxc_php7_2.dev

![5](https://user-images.githubusercontent.com/26424175/148408900-99aa0600-f73e-4dd5-a4cc-e063c399d48d.PNG)

* After that go to /etc/nginx/sites-available/lxc_php7.dev then change server name 

![6](https://user-images.githubusercontent.com/26424175/148408911-c9ce2feb-6284-411f-894d-36015e79e5ae.PNG)

* restart nginx

![7](https://user-images.githubusercontent.com/26424175/148408928-85cf290e-be68-4a8e-87eb-6269f073d968.PNG)

* try accesing lxc_php7_2.dev

![8](https://user-images.githubusercontent.com/26424175/148408936-2a1d03b7-e3c5-43f6-86b4-ce7e39f18f4d.PNG)

* Go to ubuntu_php7.4_3

![9](https://user-images.githubusercontent.com/26424175/148408949-60840b9f-331d-4c20-b095-f3c45d5e25ad.PNG)

* change ip address ubuntu_php7.4_3  to 10.0.3.151 

![10](https://user-images.githubusercontent.com/26424175/148408959-6861b07b-519e-4d5c-8b21-5c80d2bce50d.PNG)

* after that restart network lxc

![11](https://user-images.githubusercontent.com/26424175/148408974-647a0b7e-7182-4d88-9fac-be7124813136.PNG)

* go to etc/hosts then add lxc_php7_3.dev

![12](https://user-images.githubusercontent.com/26424175/148408978-6ebeeb72-320b-450e-911a-d1abc76f22cf.PNG)

* After that go to /etc/nginx/sites-available/lxc_php7.dev then change server name 

![13](https://user-images.githubusercontent.com/26424175/148408990-8c6ce3d2-d67e-4719-bfa5-b809919aa8de.PNG

* restart nginx

![7](https://user-images.githubusercontent.com/26424175/148408928-85cf290e-be68-4a8e-87eb-6269f073d968.PNG)

* try accesing lxc_php7_3.dev

![14](https://user-images.githubusercontent.com/26424175/148408994-f81f16a6-7728-4894-bd84-eea0f11ddc7a.PNG)

* Make 2 copies of debian_php5.6 and start both containers

![15](https://user-images.githubusercontent.com/26424175/148409003-7f609460-0a49-4c02-b761-2b70beb65bf7.PNG)

* Go to debian_php5.6_2 

![16](https://user-images.githubusercontent.com/26424175/148409013-ab92ac33-4bb7-4c10-a64a-0a22a7ed1c6b.PNG)

* change ip address debian_php5.6_2  to 10.0.3.112 

![17](https://user-images.githubusercontent.com/26424175/148409027-88afdefd-848b-4195-85f0-e1ee4ede0182.PNG)

* go to etc/hosts then add lxc_php5_2.dev

![18](https://user-images.githubusercontent.com/26424175/148409050-16d1467c-374a-4168-bb4a-e2917e042348.PNG)

* After that go to /etc/nginx/sites-available/lxc_php5.dev then change server name 

![19](https://user-images.githubusercontent.com/26424175/148409058-854e97b3-1f70-4ced-9073-8e10c324b255.PNG)

* restart and try accesing lxc_php5_2.dev

![20](https://user-images.githubusercontent.com/26424175/148409069-9a0b8a17-ba5c-48a4-a3b7-3b3558e483da.PNG)

* 

* Go to debian_php5.6_3

  ```markdown
  sudo lxc-attach -n debian_php5.6_3
  ```

  

* change ip address debian_php5.6_2  to 10.0.3.122 

![21](https://user-images.githubusercontent.com/26424175/148409073-646c72e9-265d-433c-915b-4dc7bf5049f1.PNG)

* go to etc/hosts then add lxc_php5_3.dev

![22](https://user-images.githubusercontent.com/26424175/148409086-d0d5afb6-9225-49c0-97d9-b3f1dea38688.PNG)

* After that go to /etc/nginx/sites-available/lxc_php5.dev then change server name 

![23](https://user-images.githubusercontent.com/26424175/148409090-abcf83b6-7da3-4e8f-b2cb-1b6a18795ddf.PNG)

* restart and try accesing lxc_php5_3.dev

![24](https://user-images.githubusercontent.com/26424175/148409102-8c884fa2-b4cf-4504-9308-85e06c01a9f7.PNG)

* Register all new containers in /etc/hosts (on vm)

![25](https://user-images.githubusercontent.com/26424175/148409151-1b3da433-32c8-4b6f-9918-1cf5140a8155.PNG)

* Run the jmeter. change the number of threads from user access from 50,100,150

  * user access 50

  ![Screenshot (349)](https://user-images.githubusercontent.com/26424175/148410013-1a3da54b-830b-40e5-bd91-0f199febba68.png)

  ![Screenshot (350)](https://user-images.githubusercontent.com/26424175/148410024-2ec1a86f-1433-4375-90cb-7d5c5c3c43fd.png)

  ![Screenshot (351)](https://user-images.githubusercontent.com/26424175/148410031-655ae6fc-a6b9-4614-87f7-f9358f7d4cfc.png)

  ![Screenshot (352)](https://user-images.githubusercontent.com/26424175/148410041-f5daa322-dae8-4264-a4ad-67a684c96fff.png)

  * User Access 100

  ![Screenshot (353)](https://user-images.githubusercontent.com/26424175/148410057-78146ecb-2ae5-4f35-8e86-a5de6ead445c.png)

  ![Screenshot (354)](https://user-images.githubusercontent.com/26424175/148410068-1f204be7-af60-4539-8a91-c4be211fd4ef.png)

  ![Screenshot (355)](https://user-images.githubusercontent.com/26424175/148410093-e54d89e0-729d-4a3f-9090-17900a331d44.png)

  ![Screenshot (356)](https://user-images.githubusercontent.com/26424175/148410100-59287b4f-c460-432e-8a82-cf2c6cb6c646.png)

  * user access 150

  ![Screenshot (357)](https://user-images.githubusercontent.com/26424175/148410136-374f8e86-f5ea-4110-b374-2d7c46d79cfb.png)

  ![Screenshot (358)](https://user-images.githubusercontent.com/26424175/148410147-d2f42f58-54c1-429e-9dd1-d4b828eedcb6.png)

  ![Screenshot (359)](https://user-images.githubusercontent.com/26424175/148410158-ef2f1f2e-3e6c-47bb-a8bd-2f4b1100302b.png)

  ![Screenshot (360)](https://user-images.githubusercontent.com/26424175/148410172-0e1c82b9-c7ec-4a4b-936d-2d3d6a886df4.png)

* back to vm and go to 

  ```markdown
  sudo nano /etc/nginx/sites-available/vm.local
  ```

![28](https://user-images.githubusercontent.com/26424175/148409194-cc2d07c2-32b7-47bb-8d55-3d8cd1f4599b.PNG)

* change proxy pass

![29](https://user-images.githubusercontent.com/26424175/148409201-42de1a23-44de-405f-beaf-1f5ff8f53d9f.PNG)

* go back to jmeter

  * user access 50

  ![Screenshot (361)](https://user-images.githubusercontent.com/26424175/148410184-a69453c3-ad04-4dac-a542-ac2488918f59.png)

  ![Screenshot (362)](https://user-images.githubusercontent.com/26424175/148410203-2fa27e05-dbd7-4687-86a0-bf38fe603153.png)

  ![Screenshot (363)](https://user-images.githubusercontent.com/26424175/148410213-2e636f03-dd03-405e-804c-e76bf742f850.png)

  ![Screenshot (364)](https://user-images.githubusercontent.com/26424175/148410224-d1b55962-2320-4305-a851-a3ea1619f556.png)

  * user access 100

  ![Screenshot (365)](https://user-images.githubusercontent.com/26424175/148410234-3bb1ad3a-2e2a-4421-8a07-9f3a2302b2a5.png)

  ![Screenshot (366)](https://user-images.githubusercontent.com/26424175/148410254-8e403159-04ef-4b06-b776-1b35fb331e5e.png)

  ![Screenshot (367)](https://user-images.githubusercontent.com/26424175/148410266-dbb5187e-7459-4bd6-8337-c632ffdc9026.png)

  ![Screenshot (368)](https://user-images.githubusercontent.com/26424175/148410271-38a2e22e-e630-4ef1-b849-7a66b81fedd4.png)

  * user access 150

  ![Screenshot (369)](https://user-images.githubusercontent.com/26424175/148410278-3c9b133b-2a16-4deb-97fb-caa085203fac.png)

  ![Screenshot (370)](https://user-images.githubusercontent.com/26424175/148410288-ef56283b-9300-48ab-99dd-fe2bf2ce9f67.png)

  ![Screenshot (371)](https://user-images.githubusercontent.com/26424175/148410296-e237e478-26f1-4912-a9c7-f9006bfb1544.png)

  ![Screenshot (372)](https://user-images.githubusercontent.com/26424175/148410303-93183cae-72c6-415a-8b15-db4b461cb8d8.png)

