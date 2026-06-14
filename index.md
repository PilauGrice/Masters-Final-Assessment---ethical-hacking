---
layout: default
title: Security Lab Report
permalink: /
---

<style>
/* Base Styles & Layout Fixes */
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;
  background: #0d1117;
  color: #c9d1d9;
}

header {
  position: sticky;
  top: 0;
  background: #161b22;
  border-bottom: 1px solid #30363d;
  padding: 15px 20px;
  z-index: 1000;
  font-family: "Courier New", monospace;
  box-shadow: 0 4px 12px rgba(0,0,0,0.5);
}

.sidebar {
  position: fixed;
  top: 55px;
  left: 0;
  width: 240px;
  height: 100%;
  background: #161b22;
  border-right: 1px solid #30363d;
  padding: 20px;
  overflow-y: auto;
}

.sidebar strong {
  color: #8b949e;
  text-transform: uppercase;
  font-size: 12px;
  letter-spacing: 1px;
  margin-bottom: 10px;
  display: block;
}

.sidebar a {
  display: block;
  color: #58a6ff;
  text-decoration: none;
  margin: 10px 0;
  font-size: 14px;
  transition: color 0.2s ease;
}

.sidebar a:hover {
  color: #79c0ff;
  text-decoration: underline;
}

.content {
  margin-left: 240px;
  padding: 30px;
  max-width: calc(100vw - 240px);
}

h1, h2, h3, h4 {
  color: #58a6ff;
  border-bottom: 1px solid #21262d;
  padding-bottom: 8px;
  margin-top: 30px;
}

/* Image & Lightbox Styles */
img {
  max-width: 100%;
  height: auto;
  border: 1px solid #30363d;
  margin: 15px 0;
  border-radius: 6px;
  cursor: zoom-in;
  transition: transform 0.2s;
}

img:hover {
  transform: scale(1.01);
  border-color: #58a6ff;
}

/* Overlap Fixes for Code Blocks */
pre {
  background: #0d1117 !important;
  padding: 15px !important;
  display: block !important;
  overflow-x: auto !important;
  border: 1px solid #30363d !important;
  border-left: 4px solid #58a6ff !important;
  border-radius: 6px !important;
  max-width: 100% !important;
}

code {
  font-family: "SFMono-Regular", Consolas, "Liberation Mono", Menlo, monospace;
  font-size: 13px;
  color: #e6edf3;
}

.terminal {
  background: #05080c;
  border: 1px solid #30363d;
  padding: 15px;
  margin: 20px 0;
  border-radius: 6px;
  color: #39ff14;
  font-family: "Courier New", monospace;
  line-height: 1.6;
  max-width: 100%;
  overflow-x: auto;
}

/* Modal (Lightbox) Background */
.modal {
  display: none;
  position: fixed;
  z-index: 2000;
  padding-top: 60px;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  background-color: rgba(0,0,0,0.9);
  backdrop-filter: blur(5px);
}

.modal-content {
  margin: auto;
  display: block;
  max-width: 90%;
  max-height: 85vh;
  object-fit: contain;
  border: none;
  cursor: zoom-out;
}

.close-modal {
  position: absolute;
  top: 15px;
  right: 35px;
  color: #f1f1f1;
  font-size: 40px;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
}

.close-modal:hover,
.close-modal:focus {
  color: #58a6ff;
  text-decoration: none;
}
</style>

<header>
  <strong>🛡️ Security Lab — Elite Submission Dashboard</strong>
</header>

<div class="sidebar">
  <strong>Navigation</strong>
  <a href="#overview">📌 Overview</a>
  <a href="#evidence">🖼️ Telemetry Evidence</a>
  <a href="#config">⚙️ Infrastructure Config</a>
  <a href="#findings">🚨 Vulnerability Findings</a>
  <a href="#monitor">📊 IDS Monitoring</a>
  <a href="#remediation">🔒 Remediation Code</a>
</div>

<div class="content" markdown="1">

# 🧪 SECURITY LAB REPORT
**Student ID:** 2512782  
**Module:** Ethical Hacking (MSc Computer Science)  

---

<h1 id="overview">📌 Overview</h1>

<div class="terminal" markdown="1">
[RANGE LOG] Docker-based multi-network cyber range online.
[RANGE LOG] Simulating enterprise segmentation, vulnerable services, and monitored exploitation lifecycle.
</div>

This dashboard serves as the official, unedited technical evidence locker for the final multi-subnet penetration testing assessment. It archives high-resolution image telemetry, custom exploit targets, and configuration architectures to support the core report submission.

---

<h1 id="evidence">🖼️ Telemetry & Exploitation Evidence Index</h1>

*(Click any image to expand it in full screen)*

### Phase 1: Environmental Provisioning
* **01_docker_compose_up.png:** Confirms error-free execution of the orchestration engine.
![01_docker_compose_up](01_docker_compose_up.png)
* **02_network_connectivity_ping.png:** Proves active transport-layer routing.
![02_network_connectivity_ping](02_network_connectivity_ping.png)
* **03_kali_container_access.png:** Documents secure execution access into `attacker-kali`.
![03_kali_container_access](03_kali_container_access.png)
* **04_tooling_installation.png:** Confirms deployment frameworks (`gobuster`, `nmap`, `curl`).
![04_tooling_installation](04_tooling_installation.png)

### Phase 2: Active Perimeter Reconnaissance
* **06_nmap_port80_scan.png:** Confirms Port 80/TCP is open on the ingress proxy.
![06_nmap_port80_scan](06_nmap_port80_scan.png)
* **05_gobuster_directory_enumeration.png:** Identifies upstream reverse proxy mounts.
![05_gobuster_directory_enumeration](05_gobuster_directory_enumeration.png)
* **07_nmap_banner_grab.png:** Documents an Information Disclosure flaw (`Server: nginx/1.29.6`).
![07_nmap_banner_grab](07_nmap_banner_grab.png)
* **09_nmap_filtered_db.png:** Verifies secure database tier (`192.168.243.20:3306`) responds as filtered.
![09_nmap_filtered_db](09_nmap_filtered_db.png)

### Phase 3: Perimeter Bypass & Pre-Packaged Targets
* **08_direct_subnet_bypass.png:** Proves critical network isolation failure bypassing Nginx.
![08_direct_subnet_bypass](08_direct_subnet_bypass.png)
* **14_juiceshop_vulnerability_analysis.png:** Gateway appending verbose banners to unhandled exceptions.
![14_juiceshop_vulnerability_analysis](14_juiceshop_vulnerability_analysis.png)
* **12_dvwa_blocked_injection.png** & **13_juiceshop_payload_probe.png:** Nginx securely dropping payloads.
![12_dvwa_blocked_injection](12_dvwa_blocked_injection.png)
![13_juiceshop_payload_probe](13_juiceshop_payload_probe.png)

### Phase 4: Custom Target Breakout & Root Exploitation
* **15_vulnerable_script_source.png:** deployment of the vulnerable web server code.
![15_vulnerable_script_source](15_vulnerable_script_source.png)
* **16_python_server_traffic_logs.png:** Python server runtime logs recording incoming hits.
![16_python_server_traffic_logs](16_python_server_traffic_logs.png)
* **17_rce_parameter_validation.png:** Proves unauthenticated remote command execution.
![17_rce_parameter_validation](17_rce_parameter_validation.png)
* **18_root_shell_pop.png:** Netcat listener catching an inbound administrative shell context.
![18_root_shell_pop](18_root_shell_pop.png)
* **19_filesystem_write_proof.png** & **20_filesystem_rmdir_cleanup.png:** Validates write permissions.
![19_filesystem_write_proof](19_filesystem_write_proof.png)
![20_filesystem_rmdir_cleanup](20_filesystem_rmdir_cleanup.png)

### Phase 5: Incident Detection & Forensic Audit
* **10_suricata_empty_logs.png** & **11_suricata_directory_la.png:** Confirms a critical defensive blindspot.
![10_suricata_empty_logs](10_suricata_empty_logs.png)
![11_suricata_directory_la](11_suricata_directory_la.png)

---

<h1 id="config">⚙️ Infrastructure (FULL CONFIG)</h1>

### Orchestration Layout (`docker-compose.yml`)

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

<h1 id="findings">🚨 FINDINGS</h1>

## 🔴 Finding 1 — Information Disclosure (Gateway)

### Evidence
- HTTP headers expose server version
- Nginx default banner visible (See Figure 7 telemetry).

### Impact
Attackers can fingerprint infrastructure and target known CVEs via Open-Source intelligence gathering.

---

## 🔴 Finding 2 — Command Injection (Custom Service)

### Vulnerable Daemon Source Code (`web.py`)
```python
#!/usr/bin/env python3
import http.server
import urllib.parse
import os

class VulnerableCommandHandler(http.server.BaseHTTPRequestHandler):
    def do_GET(self):
        self.send_response(200)
        self.send_header("Content-type", "text/plain")
        self.end_headers()
        
        parsed_url = urllib.parse.urlparse(self.path)
        query = urllib.parse.parse_qs(parsed_url.query)
        
        # CRITICAL FLAW: Unvalidated OS Popen execution
        if "cmd" in query:
            try:
                command_string = query["cmd"][0]
                execution_output = os.popen(command_string).read()
                self.wfile.write(execution_output.encode("utf-8"))
            except Exception as e:
                self.wfile.write(f"Execution Exception Context: {str(e)}".encode("utf-8"))
        else:
            self.wfile.write(b"Custom Python Audit Daemon Status: ACTIVE. Use ?cmd= for diagnostic tracking.")

if __name__ == "__main__":
    server_address = ("", 8080)
    audit_daemon = http.server.HTTPServer(server_address, VulnerableCommandHandler)
    print("Initializing Vulnerable Target Core Service on Port 8080...")
    audit_daemon.serve_forever()
```

### Impact
- Remote Code Execution (RCE)
- Full container root compromise
- Potential lateral movement into internal DMZ application networks

---

<h1 id="remediation">🔒 FIXES & REMEDIATION</h1>

---

## ✅ Fix 1 — Remove Information Disclosure

**Gateway Banner Suppression (Mitigates CWE-200)**

```nginx
http {
    # Suppresses specific version signatures from returned headers globally
    server_tokens off;
}
```

### Result
- Removes version leakage from the `dmz-gateway` perimeter.
- Reduces fingerprinting capability.

---

## ✅ Fix 2 — Eliminate Command Injection & Privilege Escalation

**Microservice Privilege Escalation Lockdown (Mitigates CWE-78)**

```yaml
services:
  victim-ubuntu:
    image: ubuntu:latest
    container_name: victim-ubuntu
    # Strips administrative capabilities and sets immutable file structures
    user: "1001:1001"
    read_only: true
```

### Result
- Drops payload execution capabilities.
- Prevents malicious file writes to the backend root directory.

---

<h1 id="monitor">📊 IDS MONITORING</h1>

- IDS (Suricata) deployed on external boundary interface.
- Detection deficit discovered due to lack of network interface port-mirroring.
- Logging baseline proved void: `eve.json` missing (See Figures 19 & 20 telemetry).

---

</div> <div id="imageModal" class="modal">
  <span class="close-modal">&times;</span>
  <img class="modal-content" id="expandedImg">
</div>

<script>
document.addEventListener("DOMContentLoaded", function() {
  var modal = document.getElementById("imageModal");
  var modalImg = document.getElementById("expandedImg");
  var images = document.querySelectorAll(".content img");
  var closeBtn = document.querySelector(".close-modal");

  images.forEach(function(img) {
    img.onclick = function() {
      modal.style.display = "block";
      modalImg.src = this.src;
    }
  });

  closeBtn.onclick = function() {
    modal.style.display = "none";
  }

  modal.onclick = function(e) {
    if (e.target !== modalImg) {
      modal.style.display = "none";
    }
  }
});
</script>
