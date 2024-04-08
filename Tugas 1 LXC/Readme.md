# Sistem Terdistribusi

  instalasi vm [https://ciperx.com/install-ubuntu-server/](https://ciperx.com/install-ubuntu-server/)
  
  Server WSL ubuntu yang telah di buat
  ![assets/gambar1.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss1.png)
  
  
  ## persiapan server host 
  ```sudo apt install -y build-essential linux-headers-$(uname -r)```
    
  ![assets/gambar2.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss2.png)
    
  jika error menggunakan poin 2
  
  ## mengganti sources list ubuntu 
  
  ```jsx
  sudo nano /etc/apt/sources.list
  ```
  
  menjadi 
  
  ```jsx
  deb http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse
  deb-src http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse
  
  deb http://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse
  deb-src http://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse
  
  deb http://archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
  deb-src http://archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
  
  deb http://archive.ubuntu.com/ubuntu/ jammy-backports main restricted universe multiverse
  deb-src http://archive.ubuntu.com/ubuntu/ jammy-backports main restricted universe multiverse
  
  deb http://archive.canonical.com/ubuntu/ jammy partner
  deb-src http://archive.canonical.com/ubuntu/ jammy partner
  ```
  ![assets/gambar3.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss3.png)
  lalu update
  ```jsx
  sudo apt update
  ```
  
  ##  LXC
  LXC (Linux Containers) adalah sebuah teknologi virtualisasi yang memungkinkan Anda untuk menjalankan beberapa lingkungan Linux terisolasi (container) di dalam satu host Linux. Kontainer ini berbagi kernel yang sama dengan host mereka, tetapi terisolasi dari kontainer lainnya.
  - install
  ```jsx
  sudo apt-get install lxc lxctl lxc-templates net-tools  
  ```
  ![assets/gambar4.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss4.png)
  
  - sudo lxc-checkconfig
    ```jsx
    sudo lxc-checkconfig
    ```
  - Menampilkan template container yang tersedia
    ```jsx
    sudo ls /usr/share/lxc/templates/
    ```
    ![assets/gambar5.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss5.png)
  
  ## Case 1
  <p align="center">
  <img src="https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Contoh1.png" alt="">
  </p>

  Membuat web server dengan nama `sister.local` pada server ubuntu yang di buat tadi

1. Nginx
     - install
       ```jsx
        sudo apt install nginx nginx-extras 
       ```
       ![assets/gambar7.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss7.png)
       
     - Konfigurasi file nginx agar bisa di akses pada web
       1. Masuk pada Diretori nginx
         ```jsx
          cd /etc/nginx/sites-enable/
         ```
       2. Copy file **`Default`** menjadi **`sister.local`**
         ```jsx
          sudo cp Default sister.local
         ```
       3. Lalu edit file menggunakan apk `nano` , tambahkan `server name sister.local`
         ```jsx
          sudo nano sister.local
         ``` 
         - Setelah di edit
           ![assets/gambar8.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss8.png)
  
           lalu save, dan menjalankan konfigurasinya
           ```jsx
            sudo nginx -t
            sudo nginx -s reload
           ``` 
  
2. Masuk pada Diretori `/var/www/html`
          ```jsx
            cd /var/www/html
           ```
         - Copy file `index.nginx-debian.html` menjadi `index.html`
           ```
            sudo cp index.nginx-debian.html index.html
           ```
         - Edit file `index.html`
            ![assets/gambar9.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss9.png)

3. Edit pada file `host` pada directory `C:\Windows\System32\drivers\etc` menggunakan `Notepad` Run Administator
         ```
          Tambahkan `127.0.0.1       sister.local`
          ```
          - Lalu jalankan domain `sister.local` pada web
            ![assets/gambar10.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/result.png)

## Case 2
  <p align="center">
  <img src="https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Contoh2.png" alt="">
  </p>

1. Membuat web server dengan menambahkan microservices ubuntu 20 untuk `sister.local/blog`, lalu microservices ubuntu 18 untuk `sister.local/about-us`
    - Microservice 1
      ``` jsx
      sudo lxc-create -t download -n microservice1 -- -d ubuntu -r fancy -a amd64 --force-cache
      sudo lxc-start -n microservice1
      ```
    - Microservice 2
      ``` jsx
      sudo lxc-create -t download -n microservice2 -- -d ubuntu -r bionic -a amd64 --force-cache
      sudo lxc-start -n microservice2
      ```
    - Melihat info dari LXC 
      ``` jsx
      sudo lxc-ls -f
      ```
      ![assets/gambar10.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-04%2012-03-06.png)

2. Jalankan LXC dengan membuka 2 terminal baru,jalankan menggunakan `lxc-attach ` dan update setelah itu  instal `nginx` pada masing-masing lxc
   - Microservice 1
     ``` jsx
     sudo lxc-attach -n microservice1
     sudo update && upgrade -y
     sudo apt install nginx nginx-extras
     ```
   - Microservice 2
     ```jsx
     sudo lxc-attach -n microservice1
     sudo update && upgrade -y
     sudo apt install nginx nginx-extras
     ```
     ![assets/gambar10.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-04%2012-10-57.png)

3. Ubah Ip LXC ke static agar tidak berubah-ubah
    - Masuk ke directory `netplan` akses file `10-lxc.yaml`
      ```
      sudo nano /etc/netplan/10-lxc.yaml
      ```
      - Example:
        ```
        network:
          version: 2
          renderer: networkd
          ethernets:
            ens3:
              dhcp4: no
              addresses:
                - 10.0.3.2/24
              gateway4: 10.0.3.1
              nameservers:
                  addresses: [8.8.8.8, 1.1.1.1]
          ```
          ![assets/gambar10.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-04%2019-54-50.png)

4. Konfigurasi *`nginx`* dengan *microservice1* = `mcsv1.local` bagian /blog dan *microservice2* = `mcsv2.local` bagian /about-us
   - Masuk pada Diretori nginx
     ```jsx
      cd /etc/nginx/sites-enable/
     ```
  - Copy file **`Default`** dan edit  tambahkan `server name mcvs1/mvsc2.local`
    - Microservice1
      ```jsx
        sudo cp Default mcsv1.local
        sudo nano mcsv1.local
      ```
    - Microservice2
      ```jsx
        sudo cp Default mcsv2.local
        sudo nano mcsv1.local
      ```
      ![assets/gambar8.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-05%2003-19-49.png)
  
  - lalu save, dan menjalankan konfigurasinya
    ```jsx
    sudo nginx -t
    sudo nginx -s reload
    ```

5. Masuk pada Diretori `/var/www/html` dan edit *index.html*
   ```jsx
     cd /var/www/html
     sudo cp index.nginx-debian.html index.html
     sudo nano index.html
   ```
    ![assets/gambar9.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-04%2020-02-06.png)

6. Edit file `/etc/hosts` agar bisa di akses di web dengan nama domain yang di buat
   ```
     sudo nano /etc/hosts
     ```
   - Web-server
     tambahkan *ip* dan nama *server*-nya dari masing-masing microservice yang di buat
       ![assets/gambar9.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-04%2020-58-53.png)

     - Tambakan Route pada `/blog` dan `/about-us` pada *sister.local* pada *web-server*
       ![assets/gambar9.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-05%2003-26-20.png)
     

   - Microservice 1 dan 2 tidak lupa tambahkan dengan ip localhost 
      ![assets/gambar9.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-04%2020-50-46.png)
     
7. Akses Website `sister.local/blog` atau `sister.local/about-us` untuk melihat hasilnya
   ![assets/gambar9.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/Screenshot%20from%202024-04-05%2003-12-10.png)


## Case 3
  <p align="center">
  <img src="https://github.com/3milia123/Sistem-Terdistribusi/blob/main/Tugas2/Image/e7dfdf6e-1a15-4e34-a6e6-6af1406b06f9.png" alt="">
  Menambahkan Web-server dengan nama *app.sister.local* dengan 3 Lxc menggunakan distro *Debian* versi *Bionic*
  </p>

  1.  Install 3 lxc ditro `Debian` versi `buster` jd
       ``` jsx
          sudo lxc-create -t download -n microservice3 -- -d debian -r buster -a amd64 --force-cache
          sudo lxc-create -t download -n microservice4 -- -d debian -r buster -a amd64 --force-cache
          sudo lxc-create -t download -n microservice5 -- -d debian -r buster -a amd64 --force-cache
       ```
       - Microservice 1 dan 2 tidak lupa tambahkan dengan ip localhost
          ``` jsx
            sudo lxc-start -n microservice3
            sudo lxc-start -n microservice4
            sudo lxc-start -n microservice5
          ```
  2. Jalankan 3 lxc menggunakan *lxc-attach* dan install nginx
     ``` jsx
     sudo lxc-attach microservice3
     sudo lxc-attach microservice4
     sudo lxc-attach microservice5
     ```
     - Install *nginx*
       ``` jsx
       sudo update
       sudo apt install nginx
       ```
       
      
        
         
