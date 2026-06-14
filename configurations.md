---
layout: default
title: "Lab Configurations"
permalink: /configurations/
---------------------------

# 💻 Lab Infrastructure Configurations

[⬅️ Return to Main Telemetry Dashboard](/)

## Overview

This page documents the Docker-based cyber security lab infrastructure, including network segmentation, container roles, and orchestration configuration.

---

## Docker Compose Configuration

```yaml
services:
  attacker-kali:
    image: kalilinux/kali-rolling
    container_name: attacker-kali
    tty: true
    stdin_open: true
    command: /bin/bash
    volumes:
      - ./Kali-Data:/root/data
    networks:
      external_net:
        ipv4_address: 192.168.240.10
      dmz_net:
        ipv4_address: 192.168.241.50

  victim-ubuntu:
    image: ubuntu:latest
    container_name: victim-ubuntu
    command: /bin/bash -c "apt-get update && apt-get install -y curl netcat-traditional && tail -f /dev/null"
    networks:
      dmz_net:
        ipv4_address: 192.168.241.99

  victim-dvwa:
    image: vulnerables/web-dvwa
    container_name: victim-dvwa
    ports:
      - "9000:80"
    networks:
      dmz_net:
        ipv4_address: 192.168.241.10

  victim-juiceshop:
    image: bkimminich/juice-shop
    container_name: victim-juiceshop
    ports:
      - "3000:3000"
    networks:
      dmz_net:
        ipv4_address: 192.168.241.20

  dmz-gateway:
    image: nginx:alpine
    container_name: dmz-gateway
    ports:
      - "8088:80"
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
    networks:
      external_net:
        ipv4_address: 192.168.240.20
      dmz_net:
        ipv4_address: 192.168.241.5

  internal-web:
    image: nginx:alpine
    container_name: internal-web
    volumes:
      - ./internal-site:/usr/share/nginx/html:ro
    networks:
      internal_net:
        ipv4_address: 192.168.242.10

  internal-db:
    image: mysql:5.7
    container_name: internal-db
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: secureapp
      MYSQL_USER: appuser
      MYSQL_PASSWORD: apppass
    volumes:
      - db_data:/var/lib/mysql
    networks:
      internal_net:
        ipv4_address: 192.168.242.20

  suricata:
    image: jasonish/suricata
    container_name: suricata
    command: ["-c", "/etc/suricata/suricata.yaml", "-i", "eth0"]
    volumes:
      - ./suricata/suricata.yaml:/etc/suricata/suricata.yaml:ro
    networks:
      external_net:
        ipv4_address: 192.168.240.30
    depends_on:
      - victim-dvwa
      - victim-juiceshop

  admin-service:
    image: php:7.4-apache
    container_name: admin-service
    volumes:
      - ./misconfigured-admin:/var/www/html
    networks:
      internal_net:
        ipv4_address: 192.168.242.30
      admin_net:
        ipv4_address: 192.168.243.30
    ports:
      - "8089:80"

  admin-network:
    image: nginx:alpine
    container_name: admin-network
    ports:
      - "8090:80"
    volumes:
      - ./admin_network/admin.conf:/etc/nginx/conf.d/default.conf:ro
    networks:
      admin_net:
        ipv4_address: 192.168.243.5

volumes:
  db_data:

networks:
  external_net:
    driver: bridge
    ipam:
      config:
        - subnet: 192.168.240.0/24

  dmz_net:
    driver: bridge
    ipam:
      config:
        - subnet: 192.168.241.0/24

  internal_net:
    driver: bridge
    ipam:
      config:
        - subnet: 192.168.242.0/24

  admin_net:
    driver: bridge
    ipam:
      config:
        - subnet: 192.168.243.0/24
```

---

## Network Architecture

| Network  | Subnet           | Purpose                  |
| -------- | ---------------- | ------------------------ |
| External | 192.168.240.0/24 | Public-facing services   |
| DMZ      | 192.168.241.0/24 | Exposed application tier |
| Internal | 192.168.242.0/24 | Backend services         |
| Admin    | 192.168.243.0/24 | Administrative systems   |

---

## Container Roles

| Container        | Function                                |
| ---------------- | --------------------------------------- |
| attacker-kali    | Security testing workstation            |
| victim-dvwa      | Deliberately vulnerable web application |
| victim-juiceshop | Modern vulnerable web application       |
| victim-ubuntu    | General Linux target                    |
| dmz-gateway      | Reverse proxy and ingress controller    |
| internal-web     | Internal web server                     |
| internal-db      | Backend database                        |
| admin-service    | Administrative web application          |
| admin-network    | Administrative network gateway          |
| suricata         | IDS/Network monitoring                  |
|                  |                                         |
