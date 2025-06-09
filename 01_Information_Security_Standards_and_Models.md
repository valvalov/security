# 01\_Information Security Standards and Models

## 1. Purpose

This document outlines the primary cybersecurity standards, models, and regulatory frameworks that govern information security programs. It provides a factual overview of internationally recognized standards with a focus on their applicability to Privileged Access Management (PAM), Zero Trust Architecture (ZTA), and operational environments such as Kubernetes.

---

## 2. International and National Standards

### 2.1 ISO/IEC 27001:2022 and ISO/IEC 27002:2022

* **Type:** International standard (published by ISO and IEC)
* **Purpose:** Information Security Management Systems (ISMS)
* **Key Clauses:**

  * **A.5–A.18:** Organizational, people, physical, and technical controls
  * **A.9:** Access control
  * **A.12:** Operations security
  * **A.18:** Compliance and audit logging
* **Relevance to PAM/ZTA:** Supports role-based access, auditability, and least privilege principles

### 2.2 NIST SP 800 Series (United States)

#### NIST SP 800-53 Rev. 5

* **Focus:** Security and Privacy Controls for Information Systems
* **Control Families:** Access Control (AC), Audit and Accountability (AU), Identification and Authentication (IA), System and Communications Protection (SC), and Incident Response (IR)
* **Use:** Mandatory for U.S. federal systems; globally referenced for best practices

#### NIST SP 800-171 Rev. 2

* **Focus:** Controlled Unclassified Information (CUI) in non-federal systems
* **Use:** Enforced in government contracts

#### NIST SP 800-207

* **Title:** Zero Trust Architecture (ZTA)
* **Relevance:** Defines identity-centric security architecture, session-based policy evaluation, and trust evaluation through continuous verification

---

## 3. Regulatory Frameworks in the European Union

### 3.1 GDPR – Regulation (EU) 2016/679

* **Focus:** Protection of personal data
* **Key Articles:** Art. 5–32 (data minimization, accountability, security, breach notification)
* **Relation to PAM:** Requires secure access to personal data, user accountability, and audit logs

### 3.2 NIS2 Directive – Directive (EU) 2022/2555

* **Focus:** Cybersecurity resilience across critical and important entities
* **Obligations:**

  * Secure access control
  * Supply chain risk management
  * Incident traceability and reporting
  * Governance and accountability measures

### 3.3 DORA – Regulation (EU) 2022/2554

* **Scope:** Financial institutions and ICT third-party providers
* **Domains Covered:**

  * ICT risk management
  * ICT incident reporting
  * Digital operational resilience testing
  * ICT third-party risk
* **Security Enforcement:** Identity governance, secure remote access, and logging of privileged operations

---

## 4. Sector-Specific Standards and Frameworks

### 4.1 PCI DSS v4.0

* **Issuer:** PCI Security Standards Council
* **Focus:** Cardholder data protection
* **Key Requirements Relevant to PAM:**

  * **Req. 7:** Access control by business need-to-know
  * **Req. 8:** Identity and authentication
  * **Req. 10:** Logging and monitoring access to systems

### 4.2 CIS Critical Security Controls v8

* **Issuer:** Center for Internet Security (CIS)
* **Role:** Prioritized, implementable cybersecurity best practices
* **Relevant Controls:**

  * Control 4: Controlled use of admin privileges
  * Control 5: Account management
  * Control 6: Access control management
  * Control 14: Security awareness and skills training

---

## 5. Zero Trust Standardization

| Organization | Standard/Document                  | Type               | Status        |
| ------------ | ---------------------------------- | ------------------ | ------------- |
| NIST         | SP 800-207                         | Voluntary standard | Final (2020)  |
| ENISA        | Zero Trust Maturity Model          | Guidance           | Published     |
| ISO/IEC      | Draft ISO/IEC 27090 (ZT Framework) | Under development  | Draft (2025+) |

> **Note:** While Zero Trust is not mandated by EU law under that name, its core principles are embedded in DORA, NIS2, and the EBA Guidelines.

---

## 6. Summary

Security standards and regulatory frameworks form the foundation for enterprise security programs. Organizations operating in regulated environments—particularly in finance, critical infrastructure, and cloud-based operations—must align with both formal standards (e.g., ISO, NIST) and sector-specific obligations (e.g., DORA, PCI DSS).

This document provides the necessary reference baseline to assess and validate PAM and Zero Trust implementations in line with these authoritative requirements.
