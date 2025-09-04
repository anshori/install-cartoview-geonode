# Install Geonode Docker di Ubuntu

## Install Docker Engine

Lihat di sini:   
[https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)   

___   
## Docker Engine Linux Post Install

Lihat di sini:   
[https://docs.docker.com/engine/install/linux-postinstall/](https://docs.docker.com/engine/install/linux-postinstall/)

___   
## Install Docker Compose Plugin

Lihat di sini:  
[https://docs.docker.com/compose/install/linux/#install-using-the-repository](https://docs.docker.com/compose/install/linux/#install-using-the-repository)

```
Catatan: Saat ini ketika install docker engine sudah sekaligus install docker compose plugin
```

___   
## Cek Versi Docker, Docker Compose

Cek versi docker   
```bash
docker --version
```

Cek versi docker compose   
```bash
docker compose version
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

## Download Geonode 4.4.3.zip (Sesuaikan versi rilisnya)
```bash
cd /home
```
```bash
sudo wget https://github.com/GeoNode/geonode/archive/refs/tags/4.4.3.zip
```   

## Extract Geonode 4.4.3.zip
```bash
sudo unzip 4.4.3.zip
```   

## Rename Geonode Folder
```bash
sudo mv geonode-4.4.3 geonode
```   

## Create .env geonode 4
```bash
cd /home/geonode
```
```bash
python3 create-envfile.py --env_type dev --hostname localhost --geonodepwd password --geoserverpwd password --pgpwd password --dbpwd password --geodbpwd password
```

#   
# Build Geonode Docker Image
```bash
docker compose build
```   
```bash
docker compose up -d
```   

#   
# Menghentikan Docker Container
```bash
docker compose stop
```   
atau
```bash
docker compose down
```   

#   
# Remote PostGIS Geonode
```bash
cd /home/geonode
```   
```bash
sudo nano docker-compose.yml
```   

## uncomment baris 125 dan 126 sehingga menjadi seperti ini   
`ports:`   
`- "5432:5432"`   

## untuk akses menggunakan aplikasi remote database   
HOST: localhost atau ip-address atau nama-domain   
PORT: 5432   
DEFAULT DB NAME: geonode   
DEFAULT POSTGIS DB NAME: geonode_data   
DEFAULT DB USERNAME: postgres   
DEFAULT DB PASSWORD: postgres   

#   
# Custom Geonode UI
[https://geonode.org/geonode-mapstore-client/master/tutorial-theme.html](https://geonode.org/geonode-mapstore-client/master/tutorial-theme.html)

#   
# Sumber
[https://docs.geonode.org/en/master/install/advanced/core/index.html#deploy-a-vanilla-geonode-with-docker](https://docs.geonode.org/en/master/install/advanced/core/index.html#deploy-a-vanilla-geonode-with-docker)

#
> unsorry@2021