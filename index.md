---
layout: default
permalink: /
---

# Technical Appendix: Containerized DMZ Security Audit Lab
**Student ID:** 2512782  
**Module:** Advanced Network Security (MSc Computer Science)  
**Academic Term:** Final Assessment  
**Platform Environment:** Local Docker Sandbox Infrastructure  
**Date:** June 2026

---

## 📁 Repository Overview
This repository serves as the official, unedited technical evidence locker for the final multi-subnet penetration testing assessment. It archives high-resolution image telemetry, environmental verification logs, custom exploit targets, and configuration architectures to support the core report submission.

---

## 🖼️ Telemetry & Exploitation Evidence Index

### Phase 1: Environmental Provisioning & Verification
#### 1. Container Infrastructure Initialization
* **Filename:** `01_docker_compose_up.png`
* **Technical Value:** Confirms error-free infrastructure creation.
![01_docker_compose_up](01_docker_compose_up.png)

#### 2. Cross-Subnet ICMP Routing Validation
* **Filename:** `02_network_connectivity_ping.png`
* **Technical Value:** Proves active transport-layer routing.
![02_network_connectivity_ping](02_network_connectivity_ping.png)

#### 3. Interactive Testing Platform Console Access
* **Filename:** `03_kali_container_access.png`
* **Technical Value:** Documents root workspace access execution.
![03_kali_container_access](03_kali_container_access.png)

#### 4. Automated Defensive Toolkit Provisioning
* **Filename:** `04_tooling_installation.png`
* **Technical Value:** Confirms package framework sync loops.
![04_tooling_installation](04_tooling_installation.png)

---

### Phase 2: Active Perimeter Reconnaissance & Fuzzing
#### 5. Active Port Status Mapping
* **Filename:** `06_nmap_port80_scan.png`
* **Technical Value:** Confirms ingress gateway TCP port status.
![06_nmap_port80_scan](06_nmap_port80_scan.png)

#### 6. Automated Directory Path Enumeration
* **Filename:** `05_gobuster_directory_enumeration.png`
* **Technical Value:** Identifies proxy application reverse paths.
![05_gobuster_directory_enumeration](05_gobuster_directory_enumeration.png)

#### 7. Transport Layer Banner Grabbing (Finding 1)
* **Filename:** `07_nmap_banner_grab.png`
* **Technical Value:** Identifies perimeter system software banner leakage.
![07_nmap_banner_grab](07_nmap_banner_grab.png)

#### 8. Out-of-Scope Security Boundary Audit
* **Filename:** `09_nmap_filtered_db.png`
* **Technical Value:** Verifies strict adherence to RoE boundaries.
![09_nmap_filtered_db](09_nmap_filtered_db.png)

---

### Phase 3: Perimeter Bypass & Pre-Packaged Target Testing
#### 9. Direct Subnet Boundary Access (Finding 2)
* **Filename:** `08_direct_subnet_bypass.png`
* **Technical Value:** Proves isolation control network failure vectors.
![08_direct_subnet_bypass](08_direct_subnet_bypass.png)

#### 10. Gateway Access Control Testing (Juice Shop)
* **Filename:** `14_juiceshop_vulnerability_analysis.png`
* **Technical Value:** Identifies verbose backend exception dumps.
![14_juiceshop_vulnerability_analysis](14_juiceshop_vulnerability_analysis.png)

#### 11. Upstream Parameter Injection Blocks (DVWA)
* **Filename:** `12_dvwa_blocked_injection.png` & `13_juiceshop_payload_probe.png`
* **Technical Value:** Confirms perimeter dropped query payload loops.
![12_dvwa_blocked_injection](12_dvwa_blocked_injection.png)
![13_juiceshop_payload_probe](13_juiceshop_payload_probe.png)

---

### Phase 4: Custom Target Breakout & Root Exploitation
#### 12. Vulnerable Server Configuration Engine
* **Filename:** `15_vulnerable_script_source.png`
* **Technical Value:** Confirms localized `/tmp/web.py` system call configurations.
![15_vulnerable_script_source](15_vulnerable_script_source.png)

#### 13. Dynamic Daemon Initialization & Logging Telemetry
* **Filename:** `16_python_server_traffic_logs.png`
* **Technical Value:** Captures inbound target exploit request tracking logs.
![16_python_server_traffic_logs](16_python_server_traffic_logs.png)

#### 14. Remote Code Execution (RCE) Validation (Finding 3)
* **Filename:** `17_rce_parameter_validation.png`
* **Technical Value:** Proves unauthenticated OS command evaluations.
![17_rce_parameter_validation](17_rce_parameter_validation.png)

#### 15. Root Shell Catch Validation
* **Filename:** `18_root_shell_pop.png`
* **Technical Value:** Documents Netcat catcher administrative socket returns.
![18_root_shell_pop](18_root_shell_pop.png)

#### 16. Post-Exploitation Write Validation
* **Filename:** `19_filesystem_write_proof.png` & `20_filesystem_rmdir_cleanup.png`
* **Technical Value:** Proves active directory write permissions.
![19_filesystem_write_proof](19_filesystem_write_proof.png)
![20_filesystem_rmdir_cleanup](20_filesystem_rmdir_cleanup.png)

---

### Phase 5: Incident Detection & Forensic Audit
#### 17. Suricata Telemetry Void Validation
* **Filename:** `10_suricata_empty_logs.png` & `11_suricata_directory_la.png`
* **Technical Value:** Confirms complete missing logging telemetry states.
![10_suricata_empty_logs](10_suricata_empty_logs.png)
![11_suricata_directory_la](11_suricata_directory_la.png)

---

## 🛠️ Extended Technical Lab Manifests
To review the core code frameworks used to orchestrate, analyze, and remediate this network environment, visit the child layout matrices below:

* 📄 **[Lab Infrastructure Environment Configurations](./configurations)**
* 🔒 **[Actionable Remediation & Hardening Blueprints](./remediations)**
