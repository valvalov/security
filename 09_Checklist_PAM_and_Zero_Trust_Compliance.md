# 09\_Checklist: PAM and Zero Trust Compliance

## 1. Purpose

This document provides a practical checklist for validating Privileged Access Management (PAM) and Zero Trust Architecture (ZTA) implementations against leading standards and regulatory frameworks. It can be used by security teams, auditors, and compliance officers to assess alignment with technical and procedural requirements.

---

## 2. General Readiness

| Item                                              | Status | Notes                      |
| ------------------------------------------------- | ------ | -------------------------- |
| PAM solution deployed and operational             |        | e.g., CyberArk             |
| Governance policies for privileged access defined |        | Aligned with ISO/NIST      |
| Risk assessment conducted                         |        | Includes PAM/ZTA scope     |
| Roles and responsibilities documented             |        | Including privileged users |
| Compliance with organizational security policy    |        |                            |

---

## 3. Identity and Access Management

| Item                                                      | Standard(s)               | Status | Notes |
| --------------------------------------------------------- | ------------------------- | ------ | ----- |
| RBAC implemented for all privileged users                 | ISO A.9, NIST AC-5        |        |       |
| Multi-factor authentication (MFA) enforced for PAM access | DORA, NIS2, PCI DSS 8.3   |        |       |
| Federated identity support (SAML, LDAP, RADIUS)           | NIST IA-2, ISO A.9.4      |        |       |
| JIT privilege elevation (no standing privilege)           | NIST AC-2(5), ISO A.9.4.1 |        |       |
| Least privilege policy enforced                           | NIST AC-6, CIS Control 4  |        |       |

---

## 4. Session Management and Auditing

| Item                                                      | Standard(s)              | Status | Notes |
| --------------------------------------------------------- | ------------------------ | ------ | ----- |
| Session brokering in place (via PSM)                      | ISO A.12.4, NIST AC-17   |        |       |
| Full session recording (text and/or video) enabled        | PCI DSS 10.2, NIST AU-12 |        |       |
| Session audit logs forwarded to SIEM                      | NIST AU-6, ISO A.18      |        |       |
| Real-time session monitoring and termination capabilities | DORA Art. 10, NIST IR-4  |        |       |
| Tamper-proof storage for audit logs                       | ISO A.12.7, NIST AU-9    |        |       |

---

## 5. Secrets and Application Integration

| Item                                                          | Standard(s)               | Status | Notes |
| ------------------------------------------------------------- | ------------------------- | ------ | ----- |
| Secrets stored securely (vault-based or encrypted store)      | ISO A.10, PCI DSS 3.5     |        |       |
| Secret injection via API/sidecar/CSI (for apps and pipelines) | NIST SC-12, CIS Control 4 |        |       |
| Conjur or AAM integration in DevOps workflows                 | ISO A.12, NIST CM-6       |        |       |
| Automated credential rotation enabled                         | NIST IA-5, PCI DSS 8.3.9  |        |       |

---

## 6. Kubernetes and Zero Trust Controls

| Item                                                             | Standard(s)                  | Status | Notes |
| ---------------------------------------------------------------- | ---------------------------- | ------ | ----- |
| Cluster segmentation using namespaces and network policies       | ISO A.13.1, NSA, CIS K8s     |        |       |
| No dual-homed (multi-zoned) Kubernetes nodes                     | NIST SP 800-207              |        |       |
| PSM Gateway used for DMZ privileged access                       | DORA Art. 10, PCI DSS Req. 7 |        |       |
| Secrets Provider (sidecar/CSI) used for app secret delivery      | ISO A.9.3, NIST SC-12        |        |       |
| Mutual TLS enforced between services and CyberArk endpoints      | NIST SC-12, SC-13            |        |       |
| Kubernetes audit logs ingested into centralized logging pipeline | NIST AU-6, PCI DSS 10        |        |       |

---

## 7. Summary and Remediation Plan

* This checklist provides a structured, standards-aligned approach to validating PAM and Zero Trust implementations.
* Each unchecked item should be evaluated and remediated in accordance with:

  * Regulatory compliance priorities (e.g., DORA, NIS2)
  * Security policy mandates (e.g., ISO 27001 controls)
  * Technical feasibility and deployment model (e.g., hybrid, DMZ)

It is recommended to review this checklist quarterly or upon any significant architecture change, regulatory update, or audit finding.

---

## 8. Reference Standards

* ISO/IEC 27001:2022 / 27002:2022
* NIST SP 800-53 Rev. 5
* NIST SP 800-207 (Zero Trust)
* DORA (EU Regulation 2022/2554)
* NIS2 Directive (EU 2022/2555)
* PCI DSS v4.0
* CIS Controls v8
* NSA Kubernetes Hardening Guide
