## Sistem Terdistribusi

instalasi vm [https://ciperx.com/install-ubuntu-server/](https://ciperx.com/install-ubuntu-server/)


1. persiapan server host 

```jsx
sudo apt install -y build-essential linux-headers-$(uname -r)
```

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

Photo

```jsx
sudo apt update
```

```jsx
sudo apt upgrade -y
```

Photo

3. install lxc 

```jsx
sudo apt-get install lxc lxctl lxc-templates net-tools  
```
