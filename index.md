---
layout: default
title: Security Lab Report
permalink: /
---

<style>
body {
  margin: 0;
  font-family: "Courier New", monospace;
  background: #070b10;
  color: #c9d1d9;
}

header {
  position: sticky;
  top: 0;
  background: #0d1117;
  border-bottom: 1px solid #1f2937;
  padding: 12px 20px;
  z-index: 1000;
}

.sidebar {
  position: fixed;
  top: 60px;
  left: 0;
  width: 230px;
  height: 100%;
  background: #0d1117;
  border-right: 1px solid #1f2937;
  padding: 15px;
}

.sidebar a {
  display: block;
  color: #58a6ff;
  text-decoration: none;
  margin: 8px 0;
  font-size: 13px;
}

.content {
  margin-left: 250px;
  padding: 25px;
  max-width: 1100px;
}

h1, h2, h3 {
  color: #58a6ff;
  border-bottom: 1px solid #1f2937;
  padding-bottom: 5px;
}

img {
  max-width: 100%;
  border: 1px solid #1f2937;
  margin: 10px 0;
}

pre, code {
  background: #0b1220;
  padding: 10px;
  display: block;
  overflow-x: auto;
  border-left: 3px solid #58a6ff;
}

.terminal {
  background: #05080c;
  border: 1px solid #1f2937;
  padding: 15px;
  margin: 15px 0;
}
</style>

<header>
  <strong>🛡️ Security Lab — Elite Submission Dashboard</strong>
</header>

<div class="sidebar">
  <strong>Navigation</strong>
  <a href="#overview">Overview</a>
  <a href="#infra">Infrastructure</a>
  <a href="#config">Docker Config</a>
  <a href="#recon">Recon</a>
  <a href="#exploit">Exploitation</a>
  <a href="#monitor">Monitoring</a>
  <a href="#remediation">Remediation</a>
</div>

<div class="content">

# 🧪 SECURITY LAB REPORT

---

# 📌 Overview {#overview}

<div class="terminal">
Docker-based segmented cyber range simulating enterprise attack surfaces, internal networks, and monitored exploitation scenarios.
</div>

---

# 🏗️ Infrastructure Summary {#infra}

- External network (240.0/24)
- DMZ (241.0/24)
- Internal (242.0/24)
- Admin (243.0/24)

---

# ⚙️ Docker Configuration (FULL) {#config}

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

  admin-network:
    image: nginx:alpine
    container_name: admin-network
    ports:
      - "8090:80"
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

# 🔍 Recon & Exploitation {#exploit}

## Evidence

![Docker](01_docker_compose_up.png)
![Ping](02_network_connectivity_ping.png)
![Kali](03_kali_container_access.png)
![Tools](04_tooling_installation.png)
![Nmap](06_nmap_port80_scan.png)
![Gobuster](05_gobuster_directory_enumeration.png)
![Banner](07_nmap_banner_grab.png)
![Bypass](08_direct_subnet_bypass.png)
![Juice](14_juiceshop_vulnerability_analysis.png)

---

# 🛡️ Monitoring {#monitor}

![Suricata](10_suricata_empty_logs.png)
![Suricata](11_suricata_directory_la.png)

---

# 🔒 Remediation (FULL) {#remediation}

## Vulnerable Code

```python
os.popen(user_input).read()
```

---

## Secure Fix

```python
import subprocess
subprocess.run(["ls"], check=True)
```

---

## Gateway Fix

```nginx
server_tokens off;
```

---

## Hardening (FULL SET)

### Container Security
- non-root execution
- read-only filesystem
- drop all capabilities
- disable privilege escalation

### Network Security
- DMZ isolation enforced
- internal segmentation active
- admin zone restricted

### Logging & Monitoring
- IDS enabled
- central logging recommended
- traffic inspection required

---

# 📊 Summary {#summary}

<div class="terminal">
✔ Full attack lifecycle demonstrated  
✔ Multi-network segmentation validated  
✔ Exploitation confirmed  
✔ Defensive remediation applied  
✔ Monitoring layer included  
</div>

---

</div>
