# Install Geonode Docker di Ubuntu

## Install Docker Engine

Lihat di sini:   
[https://docs.docker.com/engine/install/ubuntu/](https://docs.docker.com/engine/install/ubuntu/)   
   
Catatan:   
Jika instalasi docker engine pada bagian setup repository berikut ini error   
 `sudo apt-get install \`   
    `ca-certificates \`   
    `curl \`   
    `gnupg \`   
    `lsb-release`   
   
Ubah command menjadi   
```bash
 sudo apt-get install ca-certificates curl gnupg lsb-release
```

___   
## Docker Engine Linux Post Install

Lihat di sini:   
[https://docs.docker.com/engine/install/linux-postinstall/](https://docs.docker.com/engine/install/linux-postinstall/)

___   
## Install Docker Compose Plugin

Lihat di sini:  
[https://docs.docker.com/compose/install/](https://docs.docker.com/compose/install/)

___   
## Install Docker Compose

```bash
sudo apt-get update
```   
```bash
sudo apt-get install docker-compose
```      

___   
## Cek Versi Docker, Docker Compose

Cek versi docker   
```bash
docker --version
```

Cek versi docker-compose   
```bash
docker-compose --version
```

___   
## Configure where the Docker daemon listens for connections

Reload the systemctl configuration   
```bash
sudo systemctl daemon-reload
```   

Restart Docker   
```bash
sudo systemctl restart docker.service
```

#   
# Deploy GeoNode menggunakan Docker

## Install Git (jika diperlukan)   
```bash
sudo apt-get update
```   
```bash
sudo apt-get install git
```

## Membuat folder geonode dan clone geonode
```bash
sudo mkdir -p /opt/geonode/
```   
```bash
sudo chmod -Rf 775 /opt/geonode/
```

## Clone the GeoNode source code di direktori /opt/geonode
```bash
cd /opt
```   
```bash
git clone https://github.com/GeoNode/geonode.git -b 4.4.x geonode
```

Jika akan clone geonode versi 3 bisa menggunakan command berikut   
```bash
git clone https://github.com/GeoNode/geonode.git -b 3.2.x geonode
```

___   
Cara git clone spesifik branch seperti ini   
`git clone <remote-repo-url> -b <branch-name> <folder-destination>`

## Create .env geonode 4
```bash
python create-envfile.py
```

#   
# Memulai Docker di localhost

```bash
cd /opt/geonode
```   
```bash
docker-compose build --no-cache
```   
```bash
docker-compose up -d
```   

#   
# Menghentikan Docker Container
```bash
cd /opt/geonode
```   
```bash
docker-compose stop
```   

#   
# Remote PostGIS Geonode
```bash
cd /opt/geonode
```   
```bash
sudo nano docker-compose.yml
```   

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
# Mengubah Default Bahasa Indonesia dan Filter Bahasa hanya Indonesia dan English
Buka .env dengan nano atau vim   
`sudo nano .env`   

Aktifkan syntax berikut   
`# LANGUAGE_CODE=pt`   
`# LANGUAGES=(('en','English'),('pt','Portuguese'))`   

menjadi   
`LANGUAGE_CODE=id`   
`LANGUAGES=(('id','Indonesia'),('en','English'))`   

Simpan .env kemudian jalankan   
`docker-compose up -d`   

#   
# Sumber
[https://docs.geonode.org/en/master/install/advanced/core/index.html#deploy-a-vanilla-geonode-with-docker](https://docs.geonode.org/en/master/install/advanced/core/index.html#deploy-a-vanilla-geonode-with-docker)

#
> unsorry@2021