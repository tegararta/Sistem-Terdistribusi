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

3. install lxc 

```jsx
sudo apt-get install lxc lxctl lxc-templates net-tools  
```
![assets/gambar4.jpg](https://github.com/tegararta/Sistem-Terdistribusi/blob/main/Tugas%201%20LXC/assets/ss4.png)

- sudo lxc-checkconfig
