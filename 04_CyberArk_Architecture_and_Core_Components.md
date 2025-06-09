# 04\_CyberArk Architecture and Core Components

## 1. Overview

CyberArk is a leading Privileged Access Management (PAM) platform designed to secure, control, and monitor privileged credentials and sessions across hybrid and multi-cloud environments. Its architecture supports enterprise-scale deployments with high availability, disaster recovery, and deep integration into IAM, SIEM, and DevOps ecosystems.

---

## 2. Deployment Models

CyberArk supports multiple deployment architectures depending on organizational requirements:

### 2.1 On-Premises

* Deployed within the organization's data center
* Common in highly regulated environments (e.g., banks, government)
* Full control over infrastructure, patching, and network segmentation

### 2.2 Hybrid

* Core components (Vault, CPM, PSM) on-premises
* Cloud-native analytics and monitoring in SaaS
* Enables flexible scaling and advanced analytics without exposing critical assets

### 2.3 CyberArk SaaS (Cloud-hosted)

* Managed by CyberArk in dedicated or shared cloud infrastructure
* Fast deployment and reduced infrastructure overhead

All models support:

* High Availability (HA)
* Disaster Recovery (DR)
* Identity Federation (LDAP, SAML, RADIUS)
* Secure REST APIs and SDK integrations

---

## 3. Core Platform Components

| Component                                | Description                                                                                     |
| ---------------------------------------- | ----------------------------------------------------------------------------------------------- |
| **Enterprise Password Vault (EPV)**      | Encrypted storage for privileged credentials; central policy enforcement and auditing           |
| **Central Policy Manager (CPM)**         | Automates credential rotation, reconciliation, and enforcement of password policies             |
| **Privileged Session Manager (PSM)**     | Proxy-based session access to targets; enforces isolation and provides full session recording   |
| **Privileged Session Manager for Web**   | Manages privileged access to web-based portals (e.g., AWS, Azure, Salesforce) via browser proxy |
| **Password Vault Web Access (PVWA)**     | Web interface for users and administrators (approvals, access requests, logs)                   |
| **Application Access Manager (AAM)**     | Securely injects credentials into applications and DevOps pipelines via APIs or Conjur platform |
| **Endpoint Privilege Manager (EPM)**     | Applies least privilege and privilege elevation policies on endpoints (Windows, macOS, Linux)   |
| **Identity Security Intelligence (ISI)** | Performs behavioral analytics, anomaly detection, and risk scoring for privileged activities    |

---

## 4. Operational Flow

1. **Credential Request**: User or application requests access via PVWA, API, or automated workflow
2. **Policy Evaluation**: CPM validates policy, approvals, time-bound access requirements
3. **Session Launch**: PSM brokers the session without revealing credentials
4. **Activity Monitoring**: Session is recorded and optionally monitored live
5. **Credential Rotation**: CPM rotates credentials after session or based on schedule
6. **Audit and Reporting**: ISI and PVWA expose logs, alerts, and analytics to SIEM/SOAR tools

---

## 5. Integration Ecosystem

CyberArk integrates with:

* **Directory Services**: Active Directory, LDAP, Azure AD
* **Authentication Providers**: SAML, RADIUS, Kerberos
* **SIEM and SOAR**: Splunk, QRadar, Sentinel, ArcSight
* **ITSM Platforms**: ServiceNow, Jira
* **DevOps Tools**: Jenkins, Kubernetes, GitHub Actions, Terraform

---

## 6. Regulatory and Standards Alignment

CyberArk directly supports controls defined in:

* **NIST SP 800-53**: AC (Access Control), AU (Audit), IA (Authentication)
* **ISO/IEC 27001 / 27002**: A.9 (Access Control), A.12 (Operations), A.18 (Compliance)
* **PCI DSS v4.0**: Requirements 7, 8, 10 (Access, Authentication, Logging)
* **DORA / NIS2**: Secure access governance, accountability, privileged operation controls

---

## 7. Summary

CyberArk delivers a modular and extensible architecture that enables comprehensive control over privileged access across traditional, hybrid, and cloud-native environments. Its platform aligns with security standards, supports Zero Trust design, and is adaptable to the specific operational and regulatory needs of financial institutions, IT service providers, and critical infrastructure operators.
