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
  <a href="#config">Infrastructure</a>
  <a href="#findings">Findings</a>
  <a href="#monitor">Monitoring</a>
  <a href="#remediation">Remediation</a>
  <a href="#summary">Summary</a>
</div>

<div class="content">

# 🧪 SECURITY LAB REPORT

---

# 📌 Overview {#overview}

<div class="terminal">
Docker-based multi-network cyber range simulating enterprise segmentation, vulnerable services, and monitored exploitation lifecycle.
</div>

---

# ⚙️ Infrastructure (FULL CONFIG) {#config}

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
    networks:
      external_net:
        ipv4_address: 192.168.240.20
      dmz_net:
        ipv4_address: 192.168.241.5

  internal-web:
    image: nginx:alpine
    container_name: internal-web
    networks:
      internal_net:
        ipv4_address: 192.168.242.10

  internal-db:
    image: mysql:5.7
    container_name: internal-db
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
    networks:
      internal_net:
        ipv4_address: 192.168.242.20

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
```

---

# 🚨 FINDINGS {#findings}

## 🔴 Finding 1 — Information Disclosure (Gateway)

### Evidence
- HTTP headers expose server version
- Nginx default banner visible

### Impact
Attackers can fingerprint infrastructure and target known CVEs.

---

## 🔴 Finding 2 — Command Injection (Custom Service)

### Evidence
```python
os.popen(user_input).read()
```

### Impact
- Remote Code Execution (RCE)
- Full container compromise
- Potential lateral movement into internal network

---

## 🔁 FIXES FOR FINDINGS

---

## ✅ Fix 1 — Remove Information Disclosure

```nginx
server_tokens off;
```

### Result
- Removes version leakage
- Reduces fingerprinting capability

---

## ✅ Fix 2 — Eliminate Command Injection

### Replace unsafe execution:

```python
os.popen(user_input).read()
```

### With secure implementation:

```python
import subprocess

subprocess.run(["ls"], check=True)
```

### Or strict allowlist approach:

- predefined commands only
- no raw user input execution

---

# 🛡️ MONITORING {#monitor}

- IDS (Suricata) deployed
- Traffic captured on external network
- Logging baseline established

---

# 📊 SUMMARY {#summary}

<div class="terminal">
✔ Two critical findings identified  
✔ Exploitation paths validated  
✔ Network segmentation tested  
✔ Secure remediation applied  
✔ Attack surface reduced  
</div>

---

</div>
