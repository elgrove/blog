---
layout: post
title: "Torstack: automated torrenting behind a VPN"
description: 
summary: 
---

Sonarr - automated TV downloading  
Radarr - automated movie downloading  
Jackett - proxy for torrent searches  
Haugene - legendary openvpn+transmission container  

Docker compose file:  

```
version: '3.3'
services:
    haugene:
        container_name: haugene
        cap_add:
            - NET_ADMIN
        volumes:
            - /home/user/torrents:/data
            - ./haugene:/config
        environment:
            - PUID=1000
            - PGID=1000
            - OPENVPN_PROVIDER=NORDVPN
            - "OPENVPN_USERNAME=EMAIL"
            - "OPENVPN_PASSWORD=PASSWORD"
            - LOCAL_NETWORK=10.0.0.0/8
        logging:
            driver: json-file
            options:
                max-size: 10m
        ports:
            - '9091:9091'
            - '9117:9117'
            - '8989:8989'
            - '7878:7878'
        image: haugene/transmission-openvpn
        restart: unless-stopped
    jackett:
        image: ghcr.io/linuxserver/jackett
        container_name: jackett
        environment:
            - PUID=1000
            - PGID=1000
            - TZ=Europe/London
        volumes:
            - ./jackett:/config
            - /home/user/torrents:/downloads
        network_mode: service:haugene
        depends_on:
            - haugene
        restart: unless-stopped
    sonarr:
        image: ghcr.io/linuxserver/sonarr
        container_name: sonarr
        environment:
        - PUID=1000
        - PGID=1000
        - TZ=Europe/London
        volumes:
        - ./sonarr:/config
        - /mnt/main/media/tv:/tv #optional
        - /home/user/torrents:/data #optional
        network_mode: service:haugene
        depends_on:
            - haugene
        restart: unless-stopped
    radarr:
        image: ghcr.io/linuxserver/radarr
        container_name: radarr
        environment:
            - PUID=1000
            - PGID=1000
            - TZ=Europe/London
        volumes:
            - ./radarr:/config
            - /mnt/main/media/movies:/movies #optional
            - /home/user/torrents:/data #optional
        network_mode: service:haugene
        depends_on:
            - haugene
        restart: unless-stopped
networks:
    default:
```