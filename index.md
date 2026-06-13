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
