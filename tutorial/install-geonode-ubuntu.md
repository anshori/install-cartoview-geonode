# Install Docker Engine

Lihat di sini:   
[https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)   
   
Catatan:   
Jika instalasi docker pada bagian berikut ini error   
 sudo apt-get install \   
    ca-certificates \   
    curl \   
    gnupg \   
    lsb-release   
   
Ubah command menjadi
`
 sudo apt-get install ca-certificates curl gnupg lsb-release
`

___   
## Docker Engine Linux Post Install

Lihat di sini:   
[https://docs.docker.com/engine/install/linux-postinstall/](https://docs.docker.com/engine/install/linux-postinstall/)

___   
## Install Docker Compose

Lihat di sini:  
[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)


___   
## Cek Versi Docker, Docker Compose

Cek versi docker   
`docker --version`

Cek versi docker-compose   
`docker-compose --version`

___   
## Configure where the Docker daemon listens for connections

Reload the systemctl configuration   
`sudo systemctl daemon-reload`   

Restart Docker   
`sudo systemctl restart docker.service`

#   
# Deploy GeoNode menggunakan Docker

## Install Git (jika diperlukan)   
`sudo apt-get update`   
`sudo apt-get install git`

## Membuat folder geonode dan clone geonode
`sudo mkdir -p /opt/geonode/`   
`sudo chmod -Rf 775 /opt/geonode/`

## Clone the GeoNode source code on /opt/geonode
`cd /opt`   
`git clone https://github.com/GeoNode/geonode.git -b 4.x geonode`

Jika akan clone geonode versi 3 bisa menggunakan command berikut   
`git clone https://github.com/GeoNode/geonode.git -b 3.2.x geonode`

___   
Cara git clone spesifik branch seperti ini   
`git clone <remote-repo-url> -b <branch-name> <folder-destination>`

#   
# Memulai Docker di localhost

`cd /opt/geonode`   
`docker-compose build --no-cache`   
`docker-compose up -d`   

## Menghentikan Docker Container
`cd /opt/geonode`   
`docker-compose stop`   

#   
# Remote PostGIS Geonode
`cd /opt/geonode`   
`sudo nano docker-compose.yml`   

## uncomment baris 125 dan 126 sehingga menjadi seperti ini   
`ports:`   
`- "5432:5432"`   

## untuk akses menggunakan aplikasi remote database   
HOST: localhost atau ip-address atau nama domain   
PORT: 5432   
DEFAULT DB NAME: geonode   
DEFAULT POSTGIS DB NAME: geonode_data   
DEFAULT DB USERNAME: postgres   
DEFAULT DB PASSWORD: postgres   

#   
# Sumber
[https://docs.geonode.org/en/master/install/advanced/core/index.html#deploy-a-vanilla-geonode-with-docker](https://docs.geonode.org/en/master/install/advanced/core/index.html#deploy-a-vanilla-geonode-with-docker)