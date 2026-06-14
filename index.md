---

layout: default
permalink: /
title: "Technical Appendix"
---------------------------

# Technical Appendix: Containerized DMZ Security Audit Lab

**Student ID:** 2512782
**Module:** Advanced Network Security (MSc Computer Science)
**Academic Term:** Final Assessment
**Platform Environment:** Local Docker Sandbox Infrastructure
**Date:** June 2026

---

## 📁 Repository Overview

This repository serves as the official technical evidence repository for the final multi-subnet penetration testing assessment. It archives environmental verification logs, configuration architectures, screenshots, and supporting documentation used throughout the assessment.

---

## 🖼️ Telemetry & Evidence Index

### Phase 1: Environmental Provisioning & Verification

#### 1. Container Infrastructure Initialization

**Filename:** `01_docker_compose_up.png`

![01\_docker\_compose\_up](01_docker_compose_up.png)

#### 2. Cross-Subnet Connectivity Validation

**Filename:** `02_network_connectivity_ping.png`

![02\_network\_connectivity\_ping](02_network_connectivity_ping.png)

#### 3. Kali Testing Platform Access

**Filename:** `03_kali_container_access.png`

![03\_kali\_container\_access](03_kali_container_access.png)

#### 4. Security Tool Installation

**Filename:** `04_tooling_installation.png`

![04\_tooling\_installation](04_tooling_installation.png)

---

### Phase 2: Reconnaissance

#### 5. Port Enumeration

**Filename:** `06_nmap_port80_scan.png`

![06\_nmap\_port80\_scan](06_nmap_port80_scan.png)

#### 6. Directory Enumeration

**Filename:** `05_gobuster_directory_enumeration.png`

![05\_gobuster\_directory\_enumeration](05_gobuster_directory_enumeration.png)

#### 7. Banner Analysis

**Filename:** `07_nmap_banner_grab.png`

![07\_nmap\_banner\_grab](07_nmap_banner_grab.png)

#### 8. Boundary Validation

**Filename:** `09_nmap_filtered_db.png`

![09\_nmap\_filtered\_db](09_nmap_filtered_db.png)

---

### Phase 3: Application Testing

#### 9. DMZ Access Validation

**Filename:** `08_direct_subnet_bypass.png`

![08\_direct\_subnet\_bypass](08_direct_subnet_bypass.png)

#### 10. Juice Shop Assessment

**Filename:** `14_juiceshop_vulnerability_analysis.png`

![14\_juiceshop\_vulnerability\_analysis](14_juiceshop_vulnerability_analysis.png)

#### 11. DVWA Testing

**Filename:** `12_dvwa_blocked_injection.png`

![12\_dvwa\_blocked\_injection](12_dvwa_blocked_injection.png)

---

### Phase 4: Custom Service Assessment

#### 12. Service Source Code

**Filename:** `15_vulnerable_script_source.png`

![15\_vulnerable\_script\_source](15_vulnerable_script_source.png)

#### 13. Service Logging

**Filename:** `16_python_server_traffic_logs.png`

![16\_python\_server\_traffic\_logs](16_python_server_traffic_logs.png)

#### 14. Command Execution Validation

**Filename:** `17_rce_parameter_validation.png`

![17\_rce\_parameter\_validation](17_rce_parameter_validation.png)

#### 15. Shell Validation

**Filename:** `18_root_shell_pop.png`

![18\_root\_shell\_pop](18_root_shell_pop.png)

---

### Phase 5: Monitoring & Detection

#### 16. Suricata Analysis

![10\_suricata\_empty\_logs](10_suricata_empty_logs.png)

![11\_suricata\_directory\_la](11_suricata_directory_la.png)

---

## 🛠️ Additional Documentation

* 📄 [Lab Infrastructure Configurations](./configurations/)
* 🔒 [Remediations & Source Code](./remediations/)
