# How to title?

How to install Docker on Ubuntu/Linux

# Created by ?

Muhamad Reza Anugrah Maskadi, Technical Lead Divisi Web
PT. GITS Indonesia

# Created at ?

22 Mei 2018

# Update by ?

1. --

# Updated at ?

1. --

# Type ? 

Panduan atau tutorial

# Description ?

Docker adalah container apps atau Virtual-Machine yang berjalan diatas OS, hasil build atau run dari Docker disebut image, Docker digunakan untuk memudahkan deployment suatu apps ke server bisa pula untuk instalasi aplikasi atau tools yang akan digunakan di lokal komputer kita

# How - to?
## why ?

Dengan menggunakan Docker, proses instalasi tools yang kita perlukan untuk menjalankan suatu aplikasi atau web akan lebih mudah. Contoh nya jika kita ingin menaikan aplikasi website kita ke server cukup dengan menggunakan Docker my-apache2 dan tidak perlu install atau setting apache manual di server kita. jika kita ingin melakukan un-install apache yang sudah di install cukup dengan stop Docker image yang sudah running lalu hapus Docker image tersebut. namun jangan lupa pastikan kembali apakah terdapat data-data yang dibutuhkan di dalam Docker image tersebut.

## How-to-use ?

### How-to-install
1. Syarat yang wajib, memiliki server VPS yang dapat kita remote melalui terminal atau SSH selain di server Docker juga dapat di install komputer lokal anda, sangat direkomendasi kan bagi komputer/laptop yang baru dan belum terinstall - tools yang diperlukan. cukup dengan Docker maka komputer anda akan bersih. Jangan lupa di how-to ini saya ambil contoh untuk Ubuntu OS dengan versi 14.04

2. Update OS terlebih dahulu

        sudo apt-get update

        sudo apt-get -y upgrade

3. Pastikan OS anda support untuk dilakukan instalasi Docker

        sudo apt-get install linux-image-extra-`uname -r`

4. Tambahkan kunci repository Docker ke dalam apt-key OS untuk verifikasi paket

        sudo apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
        
5. Tambahkan repository Docker ke dalam Apt OS

        echo "deb https://apt.dockerproject.org/repo ubuntu-trusty main" | sudo tee /etc/apt/sources.list.d/docker.list

6. Lakukan update OS kembali

        sudo apt-get update

7. Setelah itu eksekusi install Docker

        sudo apt-get install docker-engine

8. Beberapa intruksi di dalam Docker

        docker ps 
        [untuk melihat hanya Docker yang sedang running]

        docker ps -a 
        [untuk melihat Semua Docker]

        docker images 
        [untuk melihat list Docker images yang pernah kita pull]

        docker start <Docker-name> 
        [untuk menjalankan kembali Docker yang berhenti]

        docker run --name <nama-Docker> -p <port on server>:<default port vm-Docker> <image-Docker>
        [<run> untuk pertama kali menjalankan Docker untuk --name untuk inisiasi nama Docker -p untuk inisiasi port terakhir nama Docker-image]

        docker exec -it <nama-Docker> bash 
        [untuk masuk ke dalam VM-Docker]

        docker logs <nama-Docker> 
        [untuk melakukan check logs Docker]

        docker --help 
        [untuk lebih detail tentang intruksi dalam Docker]

### How-to-use Docker (Deploy Web Statis)

1. Saya mengambil contoh cara melakukan deploy website bootstrap statis yang saya dapatkan dari
    
    https://startbootstrap.com/template-overviews/creative/

    github(sample): 

2. Lakukan 'docker pull httpd' untuk men-download docker apache/httpd

    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526946040/Docker-how-to-1.png)

3. Setelah itu buat file Dockerfile di dalam source code web statis

4. Tambahkan code berikut kedalam file Dockerfile
    
        FROM httpd:2.4 [docker image + version]
        COPY ./ /usr/local/apache2/htdocs/
        [melakukan copy source code anda ke dalam folder apache htdocs di VM-Docker]

5. Setelah itu pull source code ke dalam server atau lokal anda

6. Lakukan intruksi berikut untuk menjalankan Dockerfile
        
        docker build -t my-apache2 .
        
    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526946039/Docker-how-to-2.png)
        
7. Setelah itu lakukan instruksi berikut untuk menjalankan Docker

        docker run -dit --name web-statis -p 8090:80 my-apache2
        [nama: web-statis | port akses 8090 | port di dalam vm-Docker 80 | image-Docker: my-apache2]
    
    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526946039/Docker-how-to-3.png)

8. Lalu check apakah Website anda sudah berjalan di port 8090
        
        docker ps 
        [untuk melihat list docker running]
    
    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526946039/Docker-how-to-4.png)

        curl localhost:8090
        [untuk melakukan pengecekan apakah running di local atau tidak]
    
    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526946040/Docker-how-to5.png)

        akses via <alamat IP anda>:8090
        [untuk memastikan apakah website sudah berjalan di server]
    
    ![alt text](http://res.cloudinary.com/rezamaskadi/image/upload/v1526946040/Docker-how-to-6.png)

# Link
About Docker: 
https://docs.docker.com/

Instalasi Docker :
https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-getting-started

Docker Hub Apache : 
https://hub.docker.com/_/httpd/

Service Server : https://my.vultr.com
(saya menggunakan VPS Vulter, untuk testing dan belajar, selain itu karena Vulter murah hehe XD)

Hasil build Docker saya ada di :
http://207.148.79.65:8090/

# Source Code
Source code web-bootstrap statis saya dapatkan dari
https://startbootstrap.com/template-overviews/creative/