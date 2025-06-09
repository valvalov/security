# 03\_PAM: Concept, Scope, and Standards

## 1. Definition of Privileged Access Management (PAM)

**Privileged Access Management (PAM)** refers to the security discipline dedicated to controlling, monitoring, securing, and auditing access to critical systems and sensitive data by users or accounts with elevated privileges.

These privileged accounts include:

* Domain and local administrators
* System/service accounts with elevated access
* Cloud control plane identities
* DevOps pipelines and secrets in CI/CD tools

---

## 2. Objectives of PAM

PAM aims to:

* Enforce the principle of least privilege
* Prevent unauthorized privilege escalation and lateral movement
* Mitigate credential theft (e.g., pass-the-hash, Kerberoasting)
* Enable full auditability of privileged sessions
* Satisfy regulatory and standards-based access control requirements

---

## 3. Core Capabilities of a PAM Solution

| Capability                       | Description                                                        |
| -------------------------------- | ------------------------------------------------------------------ |
| Credential vaulting              | Secure storage and access control for passwords, keys, secrets     |
| Just-in-time (JIT) privilege     | Temporary elevation of access on demand                            |
| Privileged session management    | Proxy access, session isolation, live monitoring, and recording    |
| Application secret management    | Secure injection of credentials to applications and services       |
| Role-based access control (RBAC) | Access governance based on roles and business context              |
| Full auditing and reporting      | Immutable logs of access, behavior analytics, and session playback |

---

## 4. Standards Referencing PAM

### 4.1 NIST SP 800-53 Rev. 5

* **Access Control (AC):** Controls AC-2, AC-5, AC-6 for privilege restrictions
* **Audit and Accountability (AU):** Session recording and anomaly detection
* **Identification and Authentication (IA):** MFA and policy-driven identity enforcement

### 4.2 NIST SP 800-207 (Zero Trust Architecture)

* PAM is critical to enforcing identity-aware policy decisions at every access point
* Continuous verification and session-level controls are central tenets of ZTA

### 4.3 ISO/IEC 27001:2022 & ISO/IEC 27002:2022

* **A.9 – Access Control:** Restrictions on access rights
* **A.12 – Operations Security:** Use of secure system administration practices
* **A.18 – Compliance:** Logging, traceability, and policy compliance

### 4.4 PCI DSS v4.0

* **Req. 7:** Restrict access to cardholder data by business need-to-know
* **Req. 8:** Identify and authenticate access to system components
* **Req. 10:** Log and monitor all access to system components

### 4.5 DORA (EU Regulation 2022/2554)

* Identity governance and secure access enforcement are explicitly required
* Technical access controls must be defined and enforced for privileged operations

### 4.6 NIS2 Directive (EU 2022/2555)

* Secure authentication, auditability, and access control across critical sectors
* Emphasis on traceability of privileged actions and role-based security

---

## 5. PAM as a Foundational Control

PAM is a cross-cutting capability that supports:

* Regulatory compliance
* Operational resilience
* Insider threat mitigation
* Secure DevOps (via secret injection and access brokering)

It plays a critical role in:

* **Zero Trust Architectures**: Identity-aware policy enforcement and trust reduction
* **Incident Response**: Attribution and containment of privileged activity
* **Governance**: Enforcement of least privilege, approval workflows, and audit trails

---

## 6. Summary

Privileged Access Management is a security discipline required for compliance with modern regulatory frameworks and standards. Its implementation enforces secure and auditable control over high-risk access vectors and aligns with Zero Trust principles. PAM technologies such as CyberArk deliver the capabilities needed to satisfy technical and procedural requirements across industry sectors and threat models.
