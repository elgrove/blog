---
layout: post
title: Self-hosting a notes app on my own subdomain
description: 
summary: 
---

First I bought my domain from Google Domains for £10 a year, then signed up for Cloudflare free tier and set up DNS rules for root and WWW

Set up docker-compose on Linode

Set up SWAG container from LSIO, with Bookstack

Un-grey out proxy confs for the site required, most lsio containers are already in there. Change the subdomain where required.

Set up DNS rules for notes subdomain to the root IP address, the reverse proxy will catch the request to the root IP and forward it to the subdomain

```yaml
---
version: "2.1"
services:
  swag:
    image: ghcr.io/linuxserver/swag
    container_name: swag
    cap_add:
      - NET_ADMIN
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/London
      - URL=elgrove.xyz
      - SUBDOMAINS=www,notes
      - VALIDATION=dns
      - DNSPLUGIN=cloudflare
      - EMAIL=aaronlovegrove@protonmail.com
    volumes:
      - ./config:/config
    ports:
      - 443:443
      - 80:80
    restart: unless-stopped

  bookstack:
    image: ghcr.io/linuxserver/bookstack
    container_name: bookstack
    environment:
      - PUID=1000
      - PGID=1000
      - APP_URL=https://notes.elgrove.xyz
      - DB_HOST=bookstack_db
      - DB_USER=bookstack
      - DB_PASS=1111
      - DB_DATABASE=bookstackapp
    volumes:
      - ./bookstack:/config
    ports:
      - 6875:80
    restart: unless-stopped
    depends_on:
      - bookstack_db
  bookstack_db:
    image: ghcr.io/linuxserver/mariadb
    container_name: bookstack_db
    environment:
      - PUID=1000
      - PGID=1000
      - MYSQL_ROOT_PASSWORD=1111
      - TZ=Europe/London
      - MYSQL_DATABASE=bookstackapp
      - MYSQL_USER=bookstack
      - MYSQL_PASSWORD=1111
    volumes:
      - ./bookstack/db:/config
    restart: unless-stopped


```