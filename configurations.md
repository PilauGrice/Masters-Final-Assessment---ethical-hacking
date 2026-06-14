---

layout: default
title: "Lab Configurations"
permalink: /configurations/
---------------------------

# 💻 Lab Infrastructure Configurations

[⬅️ Return to Main Telemetry Dashboard](/)

## Overview

This page documents the Docker-based security testing environment including network segmentation and service deployment architecture.

---

## Docker Compose Configuration

```yaml
services:
  attacker-kali:
    image: kalilinux/kali-rolling
    container_name: attacker-kali

  victim-ubuntu:
    image: ubuntu:latest
    container_name: victim-ubuntu

  victim-dvwa:
    image: vulnerables/web-dvwa

  victim-juiceshop:
    image: bkimminich/juice-shop

  dmz-gateway:
    image: nginx:alpine

  internal-web:
    image: nginx:alpine

  internal-db:
    image: mysql:5.7

  suricata:
    image: jasonish/suricata

  admin-service:
    image: php:7.4-apache

  admin-network:
    image: nginx:alpine
```

---

## Network Architecture

| Network  | Subnet           | Purpose                 |
| -------- | ---------------- | ----------------------- |
| External | 192.168.240.0/24 | External services       |
| DMZ      | 192.168.241.0/24 | Public application tier |
| Internal | 192.168.242.0/24 | Backend services        |
| Admin    | 192.168.243.0/24 | Administrative systems  |

---

## Container Roles

| Container        | Function                     |
| ---------------- | ---------------------------- |
| attacker-kali    | Security testing workstation |
| victim-dvwa      | Vulnerable web application   |
| victim-juiceshop | Training application         |
| victim-ubuntu    | Linux target host            |
| dmz-gateway      | Reverse proxy                |
| internal-web     | Internal website             |
| internal-db      | Database server              |
| admin-service    | Administrative service       |
| admin-network    | Admin gateway                |
| suricata         | IDS monitoring               |

---

## Segmentation Model

```text
Internet
    │
    ▼
External Network
    │
    ▼
DMZ Network
    │
    ▼
Internal Network
    │
    ▼
Admin Network
```
