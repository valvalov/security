# 08\_Compliance Mapping: PAM and Security Standards

## 1. Purpose

This document provides a structured compliance mapping between Privileged Access Management (PAM) capabilities and the key requirements of international standards and regulatory frameworks. It assists security architects and compliance officers in validating whether implemented PAM controls (e.g., via CyberArk) satisfy applicable control objectives.

---

## 2. Standards and Frameworks Mapped

* **ISO/IEC 27001:2022 / 27002:2022**
* **NIST SP 800-53 Rev. 5**
* **NIST SP 800-207 (Zero Trust)**
* **DORA (EU 2022/2554)**
* **NIS2 Directive (EU 2022/2555)**
* **PCI DSS v4.0**
* **CIS Controls v8**

---

## 3. Mapping Matrix

| PAM Capability                   | ISO/IEC 27001     | NIST 800-53        | PCI DSS v4.0    | DORA / NIS2           | CIS Controls v8 |
| -------------------------------- | ----------------- | ------------------ | --------------- | --------------------- | --------------- |
| Credential vaulting              | A.9.2, A.12.5     | AC-6, IA-5         | Req. 8.3.6      | Art. 9, Art. 10       | Control 5       |
| Session isolation and monitoring | A.12.4, A.18.4    | AU-2, AU-12, AC-17 | Req. 10.2, 10.4 | Art. 6(1)(d), Art. 10 | Control 8, 13   |
| JIT privilege elevation          | A.9.4.1           | AC-2(5), AC-6(9)   | Req. 7.2.5      | Art. 9(2)(b)          | Control 4, 6    |
| Secret injection for apps        | A.9.3.1, A.12.6   | IA-7, SC-12        | Req. 8.6        | Art. 10               | Control 4, 7    |
| Role-based access control        | A.9.1, A.9.2      | AC-2, AC-3, AC-5   | Req. 7.1        | Art. 9(2)(a)          | Control 6       |
| MFA and identity federation      | A.9.4.2, A.13.1.1 | IA-2, IA-8         | Req. 8.3        | Art. 6(1)(c)          | Control 6       |
| Audit logs and traceability      | A.12.4, A.18.1    | AU-6, AU-12        | Req. 10.2       | Art. 6, Art. 10       | Control 8       |

---

## 4. Interpretation Notes

* **ISO/IEC controls** are focused on organizational policy enforcement, access control, and operational security. PAM helps implement these at a technical level.
* **NIST SP 800-53** provides detailed control definitions. PAM primarily maps to AC (Access Control), AU (Audit), and IA (Identification & Authentication) control families.
* **DORA and NIS2** do not mention PAM explicitly but require secure access, logging, risk management, and identity governance.
* **PCI DSS** mandates explicit control over privileged accounts and auditability of access to cardholder systems.
* **CIS Controls** use PAM to fulfill foundational principles in identity, access, and administrative privilege control.

---

## 5. CyberArk Alignment Summary

CyberArk's PAM capabilities provide high conformity with access governance and privileged session controls across all listed standards. Key features such as:

* Secure credential vaulting
* Just-in-time privilege elevation
* Secrets injection and API-based control
* Session recording and SIEM forwarding
* RBAC and MFA

... collectively enable auditable, policy-compliant control of high-risk access paths.

---

## 6. Conclusion

A properly implemented PAM solution, such as CyberArk, provides measurable support for regulatory compliance. This mapping can be used to:

* Structure internal audit checklists
* Validate technical security controls during certification processes
* Align security practices with Zero Trust principles

This document should be updated as standards evolve and should serve as a cross-reference point between architectural design and audit documentation.
