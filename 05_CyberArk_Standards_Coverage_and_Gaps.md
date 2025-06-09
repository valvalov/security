# 05\_CyberArk Standards Coverage and Gaps

## 1. Objective

This document evaluates how CyberArk’s Privileged Access Management (PAM) platform aligns with major information security standards and regulatory frameworks. It identifies areas of full compliance, partial alignment, and functional gaps.

---

## 2. Standards and Frameworks Considered

* **ISO/IEC 27001:2022**
* **NIS2 Directive (EU 2022/2555)**
* **DORA Regulation (EU 2022/2554)**
* **NIST SP 800 Series (800-53, 800-171, 800-207)**
* **PCI DSS v4.0**
* **CIS Critical Security Controls v8**

---

## 3. Core Capabilities Assessed

| CyberArk Capability              | Description                                                             |
| -------------------------------- | ----------------------------------------------------------------------- |
| Credential vaulting              | Secure encrypted storage for passwords and secrets                      |
| Session isolation and monitoring | Full proxy-based session capture and recording                          |
| Just-in-time privilege           | Temporary elevation, no standing privileges                             |
| Secrets injection                | Secure delivery of application secrets                                  |
| Endpoint least privilege         | Local admin removal, controlled elevation                               |
| Behavioral analytics             | Risk scoring and anomaly detection (via Identity Security Intelligence) |
| Auditing and logging             | Tamper-proof logs, session playback, SIEM forwarding                    |

---

## 4. Standards Coverage Matrix

| Standard / Framework      | CyberArk Coverage Scope        | Notes                                                                |
| ------------------------- | ------------------------------ | -------------------------------------------------------------------- |
| **ISO/IEC 27001:2022**    | Strong (A.9, A.12, A.13, A.18) | PAM, logging, segmentation, compliance support                       |
| **NIS2 Directive**        | Partial                        | Identity and access controls, traceability, but lacks full ICT scope |
| **DORA (EU 2022/2554)**   | Partial                        | Secure access and monitoring covered; lacks resilience/test coverage |
| **NIST SP 800-53 Rev. 5** | Strong (AC, AU, IA)            | Covers access control, audit, authentication                         |
| **NIST SP 800-207 (ZTA)** | Partial                        | Identity-aware access and session control; does not include PDP/PEP  |
| **PCI DSS v4.0**          | Strong (Req. 7, 8, 10)         | Controls on access, authentication, and system logging               |
| **CIS Controls v8**       | Partial (Controls 4, 5, 6, 14) | Covers PAM-specific domains; lacks endpoint and network defenses     |

---

## 5. Domains Fully Addressed by CyberArk

* **Access Control (AC):** Credential-based, policy-governed access to critical systems
* **Privileged Session Monitoring (AU):** Real-time monitoring, video/text session capture
* **Identity and Authentication (IA):** Centralized authentication, MFA, SAML, RADIUS
* **Audit Logging (AU):** Immutable logs, session events, SIEM integration
* **Least Privilege Enforcement:** JIT access, EPM policies, role-based access enforcement
* **Secret Protection:** Secure APIs for applications, CI/CD, and containers (via AAM/Conjur)

---

## 6. Functional Gaps and External Dependencies

| Domain                                | Not Addressed by CyberArk            | Explanation                                           |
| ------------------------------------- | ------------------------------------ | ----------------------------------------------------- |
| Network Security                      | ❌ Firewall, segmentation, IDS/IPS    | Requires integration with network security tools      |
| Vulnerability and Patch Management    | ❌ No native scanning or remediation  | External VM/patch platforms required                  |
| Application Security (SDLC)           | ❌ Secure coding, code review         | Outside PAM scope                                     |
| Physical Security                     | ❌ Hardware access, facility controls | Not applicable                                        |
| Email/Web Filtering                   | ❌ Gateway and content inspection     | Requires dedicated platforms                          |
| General IAM (Workforce-wide)          | ❌ Non-privileged identity lifecycle  | Must be paired with full-featured IAM or IGA solution |
| Business Continuity/Disaster Recovery | ❌ Backup, DRP orchestration          | Only vault-level replication supported                |

---

## 7. Summary

CyberArk provides strong coverage of access control, privilege governance, and session auditing requirements defined in international security standards and financial regulations. It is a mature PAM solution aligned with Zero Trust principles and regulatory needs.

However, CyberArk is not a general-purpose cybersecurity platform. Its effectiveness depends on integration with broader enterprise security controls, especially in areas such as network security, vulnerability management, and IAM lifecycle governance.
