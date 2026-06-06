<p align="center">
  <img src="https://img.shields.io/badge/Platform-Splunk%20Enterprise%209.4-00A4EF?style=for-the-badge&logo=splunk&logoColor=white" alt="Splunk Enterprise"/>
  <img src="https://img.shields.io/badge/OS-Windows%20Server%202022-0078D4?style=for-the-badge&logo=windows&logoColor=white" alt="Windows Server"/>
  <img src="https://img.shields.io/badge/Type-SIEM%20Deployment-FF6600?style=for-the-badge&logo=shield&logoColor=white" alt="SIEM"/>
  <img src="https://img.shields.io/badge/Status-Complete-28A745?style=for-the-badge" alt="Complete"/>
</p>

<h1 align="center">🛡️ Enterprise Network Monitoring Using Splunk SIEM</h1>

<p align="center">
  <strong>A comprehensive, end-to-end deployment of Splunk Enterprise as a Security Information and Event Management (SIEM) solution for real-time log collection, threat detection, and security dashboard visualization.</strong>
</p>

<p align="center">
  <a href="#-project-overview">Overview</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-technology-stack">Tech Stack</a> •
  <a href="#-implementation-phases">Implementation</a> •
  <a href="#-results">Results</a> •
  <a href="#-screenshots">Screenshots</a> •
  <a href="#-documentation">Documentation</a>
</p>

---

## 📋 Project Overview

This project demonstrates a **production-grade SIEM deployment** using Splunk Enterprise in a virtualized enterprise environment. The implementation covers the complete security monitoring pipeline — from endpoint log collection through centralized indexing and interactive security dashboard visualization.

### 🎯 Key Objectives

| # | Objective | Status |
|---|-----------|--------|
| 1 | Deploy Splunk Enterprise 9.4.1 as central SIEM indexer | ✅ Complete |
| 2 | Configure Splunk Universal Forwarder on monitored endpoint | ✅ Complete |
| 3 | Establish Windows Firewall rules for Splunk communication | ✅ Complete |
| 4 | Validate end-to-end data ingestion pipeline | ✅ Complete |
| 5 | Develop targeted SPL queries for security analysis | ✅ Complete |
| 6 | Build interactive Authentication Security Dashboard | ✅ Complete |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        SIEM ARCHITECTURE                            │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   ┌──────────────────────┐         ┌──────────────────────────┐     │
│   │   MONITORED ENDPOINT │         │     SPLUNK SIEM SERVER   │     │
│   │   ────────────────── │         │   ────────────────────── │     │
│   │                      │  TCP    │                          │     │
│   │  Windows 10/11       │  9997   │  Windows Server 2022     │     │
│   │  DESKTOP-EPLK670     │ ──────► │  WIN-CJ0J0L41QG0         │     │
│   │                      │         │                          │     │
│   │  ┌───────────────┐   │         │  ┌───────────────────┐   │     │
│   │  │  Universal    │   │         │  │ Splunk Enterprise │   │     │
│   │  │  Forwarder    │   │         │  │     Indexer       │   │     │
│   │  │  v9.4.3       │   │         │  │     v9.4.1        │   │     │
│   │  └───────────────┘   │         │  └───────────────────┘   │     │
│   │                      │         │          │               │     │
│   │  Data Sources:       │         │          ▼               │     │
│   │  • Security Logs     │         │  ┌──────────────────┐    │     │
│   │  • System Logs       │         │  │  Search Head     │    │     │
│   │  • Setup Logs        │         │  │  (Web UI :8000)  │    │     │
│   │  • Application Logs  │         │  └──────────────────┘    │     │
│   └──────────────────────┘         └──────────────────────────┘     │
│                                                                     │
│   ┌─────────────────────────────────────────────────────────┐       │
│   │                FIREWALL CONFIGURATION                   │       │
│   │  Inbound:  TCP 8000 (Web), TCP 9997 (Data Receiving)    │       │
│   │  Outbound: splunkd.exe → Indexer (TCP 9997)             │       │
│   └─────────────────────────────────────────────────────────┘       │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Technology Stack

| Technology | Version | Purpose |
|-----------|---------|---------|
| **Splunk Enterprise** | 9.4.1 | Central SIEM platform for log indexing, search, and visualization |
| **Splunk Universal Forwarder** | 9.4.3 | Lightweight log collection agent for endpoint deployment |
| **Windows Server 2022** | Standard Evaluation | SIEM server operating system |
| **Windows Defender Firewall** | Advanced Security | Network traffic filtering and rule management |
| **Oracle VirtualBox** | 7.x | Hypervisor for lab environment virtualization |
| **SPL** | Native | Splunk Search Processing Language for data analysis |

---

## 📦 Implementation Phases

### Phase 1: Splunk Enterprise Installation

Splunk Enterprise 9.4.1 was downloaded and installed on Windows Server 2022. A dedicated administrator account (`phour44`) was configured with secure credentials, and the platform was activated under an enterprise trial license.

<p align="center">
  <img src="Screenshots/Splunk%20Downloaded.jpg" alt="Splunk Enterprise Downloaded" width="600"/>
  <br/><em>Figure 1: Splunk Enterprise installer downloaded to Windows Server 2022</em>
</p>

<p align="center">
  <img src="Screenshots/installing%20and%20configuring%20splunk%20user.jpg" alt="Splunk User Configuration" width="600"/>
  <br/><em>Figure 2: Administrator account creation during Splunk Enterprise installation</em>
</p>

<p align="center">
  <img src="Screenshots/splunk%20login%20page.jpg" alt="Splunk Login Page" width="600"/>
  <br/><em>Figure 3: Splunk Enterprise web login interface at 127.0.0.1:8000</em>
</p>

---

### Phase 2: Universal Forwarder Deployment

The Splunk Universal Forwarder 9.4.3 was installed on the monitored endpoint (DESKTOP-EPLK670) and configured with the indexer IP address and receiving port (TCP 9997).

<p align="center">
  <img src="Screenshots/splunk%20universal%20forwarder%20installation.jpg" alt="UF Installation" width="600"/>
  <br/><em>Figure 4: Universal Forwarder installation wizard on the monitored endpoint</em>
</p>

<p align="center">
  <img src="Screenshots/configuring%20splunk%20universal%20forwarder.jpg" alt="UF Configuration" width="600"/>
  <br/><em>Figure 5: Universal Forwarder connection configuration with indexer parameters</em>
</p>

<p align="center">
  <img src="Screenshots/splunk%20universal%20forwarder%20successfully%20installed.jpg" alt="UF Success" width="600"/>
  <br/><em>Figure 6: Successful Universal Forwarder installation confirmation</em>
</p>

---

### Phase 3: Windows Firewall Configuration

Windows Defender Firewall rules were configured on both the server and endpoint. Inbound rules permit Splunk traffic on TCP 8000 and 9997. Outbound rules allow the Universal Forwarder to transmit logs to the indexer.

<p align="center">
  <img src="Screenshots/Configuring%20Windows%20Firewall%20With%20Advance%20Security.jpg" alt="Firewall Config" width="600"/>
  <br/><em>Figure 7: Windows Defender Firewall with Advanced Security management console</em>
</p>

<p align="center">
  <img src="Screenshots/allowing%20all%20domain_public_private%20for%20splunkd.jpg" alt="Network Profiles" width="600"/>
  <br/><em>Figure 8: Firewall rule applied across Domain, Private, and Public network profiles</em>
</p>

<p align="center">
  <img src="Screenshots/splunk%20firewall%20outbound%20rule%20enabled.jpg" alt="Outbound Rule Enabled" width="600"/>
  <br/><em>Figure 9: Splunk outbound firewall rule successfully enabled</em>
</p>

---

### Phase 4: Indexer and Receiving Port Configuration

The Splunk Enterprise indexer was configured to listen on TCP port 9997 for incoming Universal Forwarder data through the Forwarding and Receiving settings.

<p align="center">
  <img src="Screenshots/bandicam%202026-06-04%2020-45-50-902.jpg" alt="Receiving Port" width="600"/>
  <br/><em>Figure 10: Splunk Enterprise receiving port (TCP 9997) configuration</em>
</p>

---

### Phase 5: Data Ingestion Verification

The `index=*` search query confirmed **5,406 events** were successfully ingested from the monitored endpoint, covering Security, System, Setup, and Application logs.

<p align="center">
  <img src="Screenshots/bandicam%202026-06-04%2021-23-05-520.jpg" alt="Data Ingestion" width="700"/>
  <br/><em>Figure 11: Search results confirming 5,406 events ingested from DESKTOP-EPLK670</em>
</p>

---

### Phase 6: SPL Search and Analysis

Targeted SPL queries were developed to analyze security events, including host-specific filtering and EventCode-based analysis for authentication monitoring.

<p align="center">
  <img src="Screenshots/bandicam%202026-06-04%2021-38-16-267.jpg" alt="SPL Analysis" width="700"/>
  <br/><em>Figure 12: SPL query filtering EventCode=1 events for host DESKTOP-EPLK670</em>
</p>

---

### Phase 7: Security Dashboard Creation

A custom **Authentication Dashboard** was built with visualization panels including Failed Logon Trend (line chart), Total Failed Logons (single value), and host-based event monitoring.

<p align="center">
  <img src="Screenshots/bandicam%202026-06-05%2015-51-00-583.jpg" alt="Dashboard Editor" width="700"/>
  <br/><em>Figure 13: Splunk Dashboard Editor showing the Authentication Dashboard with Failed Logon Trend chart and Total Failed Logons counter</em>
</p>

<p align="center">
  <img src="Screenshots/splunk%20dashboard.jpg" alt="Splunk Dashboard" width="700"/>
  <br/><em>Figure 14: Splunk Enterprise home dashboard overview</em>
</p>

<p align="center">
  <img src="Screenshots/splunk%20dashboard_2.jpg" alt="Dashboard View 2" width="700"/>
  <br/><em>Figure 15: Additional Splunk dashboard view showing available applications and data sources</em>
</p>

---

## 📊 Results

### Data Ingestion Summary

| Metric | Value |
|--------|-------|
| Total Events Ingested | **5,406** |
| Monitored Hosts | 1 (DESKTOP-EPLK670) |
| Log Sources | 4 (Security, System, Setup, Application) |
| Monitoring Period | June 3 - 5, 2026 |
| Failed Logon Events (4625) | 4 |
| Setup Events (EventCode 1) | 8 |
| Unique Account Names | 14 |
| Unique Account Domains | 7 |

### Key SPL Queries Used

```spl
# All indexed events
index=*

# Host-specific event filtering
index=* host="DESKTOP-EPLK670" EventCode=1

# Failed logon trend analysis
index=main sourcetype="WinEventLog:Security" EventCode=4625
| timechart span=1d count by host

# Total failed logon count
index=main sourcetype="WinEventLog:Security" EventCode=4625
| stats count
```

---

## 📸 Screenshots

The `Screenshots/` directory contains **120 high-resolution captures** documenting every phase of the implementation. Key screenshots include:

| Category | File | Description |
|----------|------|-------------|
| 🔽 Download | `Splunk Downloaded.jpg` | Splunk Enterprise installer download |
| ⚙️ Installation | `installing Splunk.jpg` | Installation progress on Windows Server |
| 📜 Licensing | `splunk licensing.jpg` | License agreement and activation |
| 🔐 Login | `splunk login page.jpg` | Splunk web interface authentication |
| 📡 Forwarder | `splunk universal forwarder successfully installed.jpg` | UF deployment confirmation |
| 🧱 Firewall | `splunk firewall outbound rule enabled.jpg` | Firewall rule activation |
| 📊 Dashboard | `splunk dashboard.jpg` | Splunk home dashboard |
| 🔍 Search | `bandicam 2026-06-04 21-23-05-520.jpg` | 5,406 events ingested |
| 📈 Analysis | `bandicam 2026-06-04 21-38-16-267.jpg` | SPL query results |

---

## 📄 Documentation

| Document | Format | Description |
|----------|--------|-------------|
| [`Splunk_SIEM_Network_Monitoring_Report.pdf`](Splunk_SIEM_Network_Monitoring_Report.pdf) | PDF | Comprehensive project report with 38 embedded figures, APA formatting, and professional technical analysis |
| [`README.md`](README.md) | Markdown | This file — project overview, architecture, and technical reference |

> **Note**: The full `.docx` source document is available in the repository for reference alongside the PDF.

---

## 🔐 Security Considerations

| Area | Implementation |
|------|---------------|
| **Firewall Hardening** | Rules configured for specific executables only (least privilege) |
| **Authentication** | Dedicated admin account with strong credentials |
| **Network Segmentation** | VirtualBox internal networking for environment isolation |
| **Data Integrity** | Persistent TCP connections for reliable log transmission |
| **Production Rec.** | Enable SSL/TLS encryption for forwarder-to-indexer traffic |

---

## 🚀 Recommendations for Production

1. **Enable SSL/TLS Encryption** between Universal Forwarders and the indexer
2. **Implement RBAC** (Role-Based Access Control) within Splunk
3. **Deploy Additional Forwarders** across all network endpoints
4. **Configure Alerting** for brute force detection and privilege escalation
5. **Integrate Threat Intelligence** feeds for IOC correlation
6. **Establish Log Retention Policies** aligned with regulatory standards (PCI DSS, HIPAA)
7. **Extend to Syslog** sources from network infrastructure devices

---

## 📚 References

1. Splunk, Inc. (2026). *Splunk Enterprise 9.4 Documentation*. https://docs.splunk.com/Documentation/Splunk/9.4.1
2. Splunk, Inc. (2026). *About the Splunk Universal Forwarder*. https://docs.splunk.com/Documentation/Forwarder/9.4.3
3. Microsoft. (2026). *Windows Defender Firewall with Advanced Security*. https://learn.microsoft.com
4. NIST. (2018). *Framework for Improving Critical Infrastructure Cybersecurity (v1.1)*. https://doi.org/10.6028/NIST.CSWP.04162018
5. SANS Institute. (2024). *Building a SIEM: Centralized Logging Architecture*. https://www.sans.org/white-papers/

---

<p align="center">
  <sub>Built with 🔒 by <strong>Phour44</strong> | Cybersecurity Analyst & Network Security Engineer | June 2026</sub>
</p>
