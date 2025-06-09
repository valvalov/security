# 02\_Zero Trust and Regulatory Relevance in the EU

## 1. Introduction to Zero Trust

### Definition (NIST SP 800-207)

> Zero Trust is an evolving set of cybersecurity paradigms that move defenses from static, network-based perimeters to focus on users, assets, and resources.
> "No implicit trust is granted to assets or user accounts based solely on their physical or network location."

### Core Principles

* Never trust, always verify
* Assume breach
* Enforce least privilege
* Continuous authentication and monitoring
* Microsegmentation and contextual policy enforcement

---

## 2. Standardization and Guidance

| Organization | Document                         | Scope                                     | Status        |
| ------------ | -------------------------------- | ----------------------------------------- | ------------- |
| **NIST**     | SP 800-207                       | Foundational ZTA architecture model       | Final (2020)  |
| **ENISA**    | Zero Trust Maturity Model (2023) | EU-specific guidance for critical sectors | Published     |
| **ISO/IEC**  | Draft ISO/IEC 27090              | International Zero Trust framework        | Draft (2025+) |

Although not legally binding, these documents provide authoritative guidance for ZTA implementations across industries.

---

## 3. EU Regulatory Framework and Zero Trust Alignment

### 3.1 NIS2 Directive (EU) 2022/2555

* **Scope:** Applies to essential and important entities (incl. banks, IT providers)
* **Implied Zero Trust Elements:**

  * Risk-based access control
  * Secure authentication (MFA)
  * Segmentation and supply chain security
  * Logging and traceability of access events

### 3.2 DORA (EU) 2022/2554

* **Scope:** Applies to all financial entities and ICT third-party providers
* **Implied Zero Trust Elements:**

  * Identity governance and access control
  * Secure remote access mechanisms
  * Protection and monitoring of privileged operations
  * Continuous evaluation and resilience testing

### 3.3 EBA Guidelines on ICT and Security Risk Management

* **Enforced by:** European Banking Authority (EBA)
* **Implied Zero Trust Elements:**

  * Strong internal segregation of environments
  * Secure privilege and role-based access
  * Isolation of critical systems and interfaces

---

## 4. Relevance to EU Financial Sector

| Requirement                 | ZT Principle | Regulatory Mandate (EU)    |
| --------------------------- | ------------ | -------------------------- |
| Least privilege enforcement | ✔️           | NIS2, DORA, EBA Guidelines |
| Multi-factor authentication | ✔️           | DORA, PSD2                 |
| Network segmentation        | ✔️           | NIS2, EBA Guidelines       |
| Continuous monitoring       | ✔️           | DORA                       |
| ZT architecture (by name)   | ❌            | Not mandated explicitly    |

> **Conclusion:** Zero Trust is not a named requirement in EU law, but its principles are embedded in binding regulatory texts and supervisory guidance.

---

## 5. Implementation Implications

Organizations regulated under NIS2 and DORA must:

* Apply identity- and context-based access decisions
* Enforce session controls, monitoring, and just-in-time access
* Maintain isolation between internal, external, and third-party zones
* Ensure all access is explicitly authorized and auditable

These requirements are fully compatible with Zero Trust design patterns as outlined in NIST SP 800-207.

---

## 6. Summary

Zero Trust is not a regulatory obligation per se within the EU, but it is becoming the de facto model for meeting cybersecurity expectations in regulated environments. Principles such as least privilege, continuous verification, segmentation, and secure access controls are not only good practices—they are mandated indirectly by DORA, NIS2, and EBA Guidelines.

Security programs based on Zero Trust models are better aligned with current and future supervisory expectations and provide a strategic foundation for digital resilience.

---

## References

* NIST SP 800-207: [https://doi.org/10.6028/NIST.SP.800-207](https://doi.org/10.6028/NIST.SP.800-207)
* DORA Regulation (EU) 2022/2554: [https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32022R2554](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32022R2554)
* NIS2 Directive (EU) 2022/2555: [https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32022L2555](https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=CELEX:32022L2555)
* EBA Guidelines (EBA/GL/2019/04): [https://www.eba.europa.eu/regulation-and-policy/internal-governance/guidelines-on-ict-and-security-risk-management](https://www.eba.europa.eu/regulation-and-policy/internal-governance/guidelines-on-ict-and-security-risk-management)
