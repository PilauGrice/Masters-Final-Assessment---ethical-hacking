---
layout: default
permalink: /
---

# Technical Appendix: Containerized DMZ Security Audit Lab
**Student ID:** 2512782
**Module:** Ethical Hacking  
**Academic Term:** Final Assessment   
**Platform Environment:** Local Docker Sandbox Infrastructure  
**Date:** June 2026   

---

## 📁 Repository Overview
This repository serves as the official, unedited technical evidence locker for final assignment for ethical hacking. It includes all screenshots that are able to be viewed in highier quality.
---

#### 1. Container Infrastructure Initialization
* **Filename:** `01_docker_compose_up.png`
* **Technical Value:** Confirms the creation of four error free custom networks and launching 13 independent microservice containers successfully.

![01_docker_compose_up](01_docker_compose_up.png)

#### 2. Cross-Subnet ICMP Routing Validation
* **Filename:** `02_network_connectivity_ping.png`
* **Technical Value:** Proves active routing from the Attacker space across all targeted infrastructure layers (`192.168.240.20`, `192.168.241.99`, and `192.168.241.10`).

![02_network_connectivity_ping](02_network_connectivity_ping.png)

#### 3. Interactive Testing Platform Console Access
* **Filename:** `03_kali_container_access.png`
* **Technical Value:** Documents secure execution access into the `attacker-kali` container workspace (`root@7b03fdffd330`).

![03_kali_container_access](03_kali_container_access.png)

#### 4. Automated Defensive Toolkit Provisioning
* **Filename:** `04_tooling_installation.png`
* **Technical Value:** Confirms installation of deployment frameworks (`gobuster`, `nmap`, `curl`).

![04_tooling_installation](04_tooling_installation.png)

---

#### 5. Active Port Status Mapping
* **Filename:** `06_nmap_port80_scan.png`
* **Technical Value:** Confirms that Port 80/TCP is open on the ingress proxy interface (`192.168.240.20`) and actively accepting incoming HTTP transactions.

![06_nmap_port80_scan](06_nmap_port80_scan.png)

#### 6. Automated Directory Path Enumeration
* **Filename:** `05_gobuster_directory_enumeration.png`
* **Technical Value:** Identifies hidden upstream application reverse proxy mounts (`/dvwa/` and `/juiceshop/`) via returned `301 Moved Permanently` status responses.

![05_gobuster_directory_enumeration](05_gobuster_directory_enumeration.png)

#### 7. Transport Layer Banner Grabbing (Finding 1)
* **Filename:** `07_nmap_banner_grab.png`
* **Technical Value:** Documents an Information Disclosure flaw. Nmap scripts successfully force the perimeter proxy to leak its specific deployment signature version: `Server: nginx/1.29.6`.

![07_nmap_banner_grab](07_nmap_banner_grab.png)

#### 8. Out-of-Scope Security Boundary Audit
* **Filename:** `09_nmap_filtered_db.png`
* **Technical Value:** Verifies strict adherence to the engagement's Rules of Engagement (RoE). The secure database tier (`192.168.243.20:3306`) responds correctly as `filtered`, confirming out-of-band protections were intact.

![09_nmap_filtered_db](09_nmap_filtered_db.png)

---

### Phase 3: Perimeter Bypass & Pre-Packaged Target Testing
Initial testing loops focused on pre-packaged application targets behind the proxy to evaluate if the gateway intercepted or dropped typical application exploitation vectors.

#### 9. Direct Subnet Boundary Access (Finding 2)
* **Filename:** `08_direct_subnet_bypass.png`
* **Technical Value:** Proves a critical network isolation failure. The attacker container directly reaches the backend private application server (`192.168.241.10`) via a raw curl request, completely bypassing Nginx gateway monitoring.

![08_direct_subnet_bypass](08_direct_subnet_bypass.png)

#### 10. Gateway Access Control Testing (Juice Shop)
* **Filename:** `14_juiceshop_vulnerability_analysis.png`
* **Technical Value:** Examines how the edge proxy handles bad URL path queries (`/this-page-does-not-exist`). The response shows that the gateway appends its verbose banner to unhandled exceptions.

![14_juiceshop_vulnerability_analysis](14_juiceshop_vulnerability_analysis.png)

#### 11. Upstream Parameter Injection Blocks (DVWA)
* **Filename:** `12_dvwa_blocked_injection.png` & `13_juiceshop_payload_probe.png`
* **Technical Value:** Documents early testing stages. The Nginx application gateway securely drops raw inline shell payloads and drops the state cookie, redirecting the request back to the `login.php` root path.

![12_dvwa_blocked_injection](12_dvwa_blocked_injection.png)
![13_juiceshop_payload_probe](13_juiceshop_payload_probe.png)

---

### Phase 4: Custom Target Breakout & Root Exploitation
Because the proxy blocked standard exploit inputs on pre-packaged components, a custom application handler script (`web.py`) was stood up on the internal Ubuntu target (`192.168.241.99`) to evaluate unvalidated backend parameter processing.

#### 12. Vulnerable Server Configuration Engine
* **Filename:** `15_vulnerable_script_source.png`
* **Technical Value:** Captures the deployment of the vulnerable web server code block within `/tmp/web.py`. It details the structural flaw where raw URL parameter arrays are passed directly to `os.popen().read()`.

![15_vulnerable_script_source](15_vulnerable_script_source.png)

#### 13. Dynamic Daemon Initialization & Logging Telemetry
* **Filename:** `16_python_server_traffic_logs.png`
* **Technical Value:** Captures the Python server runtime logs in real time. It records incoming exploitation test hits (`whoami` and `hostname`) originating from the attacker node (`192.168.241.50`).

![16_python_server_traffic_logs](16_python_server_traffic_logs.png)

#### 14. Remote Code Execution (RCE) Validation (Finding 3)
* **Filename:** `17_rce_parameter_validation.png`
* **Technical Value:** Proves unauthenticated remote command execution. Firing curl hooks directly extracts internal target system properties without requiring a password.

![17_rce_parameter_validation](17_rce_parameter_validation.png)

#### 15. Root Shell Catch Validation
* **Filename:** `18_root_shell_pop.png`
* **Technical Value:** The definitive capture image showing the Netcat listener catching an inbound administrative interactive shell context from the target machine.

![18_root_shell_pop](18_root_shell_pop.png)

#### 16. Post-Exploitation Write Validation
* **Filename:** `19_filesystem_write_proof.png` & `20_filesystem_rmdir_cleanup.png`
* **Technical Value:** Validates active write permissions on the compromised container's root file structure by successfully executing `mkdir` and `rmdir` sequences.

![19_filesystem_write_proof](19_filesystem_write_proof.png)
![20_filesystem_rmdir_cleanup](20_filesystem_rmdir_cleanup.png)

---

### Phase 5: Incident Detection & Forensic Audit
A post-exploit security event review was performed on the log collection frameworks to verify if the attack telemetry generated flags within the central monitoring system.

#### 17. Suricata Telemetry Void Validation
* **Filename:** `10_suricata_empty_logs.png` & `11_suricata_directory_la.png`
* **Technical Value:** Confirms a critical defensive blindspot. Inspecting `/var/log/suricata/` reveals `total 8` blocks, proving that the monitoring container generated zero structured security alerts (`eve.json` is entirely missing) during the attack.

![10_suricata_empty_logs](10_suricata_empty_logs.png)
![11_suricata_directory_la](11_suricata_directory_la.png)

# Docker Lab Environment

```yaml
services:
  # Attacker Kali machine
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

  # Victim Ubuntu machine (for manual testing and reconnaissance)
  victim-ubuntu:
    image: ubuntu:latest
    container_name: victim-ubuntu
    command: /bin/bash -c "apt-get update && apt-get install -y curl netcat-traditional && tail -f /dev/null"
    networks:
      dmz_net:
        ipv4_address: 192.168.241.99

  # Victim DVWA
  victim-dvwa:
    image: vulnerables/web-dvwa
    container_name: victim-dvwa
    ports:
      - "9000:80"
    networks:
      dmz_net:
        ipv4_address: 192.168.241.10

  # Victim Juice Shop
  victim-juiceshop:
    image: bkimminich/juice-shop
    container_name: victim-juiceshop
    ports:
      - "3000:3000"
    networks:
      dmz_net:
        ipv4_address: 192.168.241.20

  # DMZ Gateway (reverse proxy)
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

  # Internal Web Server
  internal-web:
    image: nginx:alpine
    container_name: internal-web
    volumes:
      - ./internal-site:/usr/share/nginx/html:ro
    networks:
      internal_net:
        ipv4_address: 192.168.242.10

  # Internal Database
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

  # IDS / Monitoring (Suricata)
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

  # Misconfigured admin service (intentionally weak)
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

  # Admin network gateway
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
