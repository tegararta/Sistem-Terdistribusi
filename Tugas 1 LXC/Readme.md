## Sistem Terdistribusi

  instalasi vm [https://ciperx.com/install-ubuntu-server/](https://ciperx.com/install-ubuntu-server/)
  
  Server WSL ubuntu yang telah di buat
  ![assets/gambar1.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss1.png)
  
  
  1. persiapan server host 
  
  ```jsx
  sudo apt install -y build-essential linux-headers-$(uname -r)
  ```
  ![assets/gambar2.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss2.png)
  
  jika error menggunakan poin 2
  
  2. mengganti sources list ubuntu 
  
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
  
  3.  LXC
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
  
  4. Nginx
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
  
       4. Masuk pada Diretori `/var/www/html`
          ```jsx
            cd /var/www/html
           ```
         - Copy file `index.nginx-debian.html` menjadi `index.html`
           ```
            sudo cp index.nginx-debian.html index.html
           ```
         - Edit file `index.html`
            ![assets/gambar9.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss9.png)

       5. Edit pada file `host` pada directory `C:\Windows\System32\drivers\etc` menggunakan `Notepad` Run Administator
           ``
          Tambahkan `127.0.0.1       sister.local`
          ``
          - Lalu jalankan domain `sister.local` pada web
            ![assets/gambar10.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/result.png) 
         
