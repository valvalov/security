# 06\_Kubernetes Zero Trust Deployment in DMZ

## 1. Objective

This document presents a reference architecture and design principles for deploying Kubernetes clusters in a Demilitarized Zone (DMZ), integrated with CyberArk Privileged Access Management (PAM) components, following Zero Trust security models.

---

## 2. Security Principles

### Zero Trust Tenets Applied to Kubernetes in DMZ

* **No implicit trust across zones**: All access must be explicitly authorized and monitored.
* **Least privilege enforcement**: All identities and workloads operate with the minimum required permissions.
* **Segmentation**: Logical separation of workloads using Kubernetes namespaces and network policies.
* **Egress-only design**: DMZ workloads must not initiate internal connections unless explicitly permitted.
* **Auditable communication paths**: All secrets, sessions, and operations must be logged and traceable.

---

## 3. Architecture Overview

### Security Zones

| Zone                 | Description                                       |
| -------------------- | ------------------------------------------------- |
| **DMZ**              | Public-facing Kubernetes workloads and interfaces |
| **Internal/Trusted** | Core CyberArk components and control systems      |

### Key Components

| Component                | Zone     | Function                                                                 |
| ------------------------ | -------- | ------------------------------------------------------------------------ |
| EPV (Vault)              | Internal | Central credential storage                                               |
| CPM                      | Internal | Automated credential rotation                                            |
| PVWA                     | Internal | Web portal for PAM access; optionally via proxy/jump host                |
| PSM Gateway              | DMZ      | Session broker for privileged access to targets in DMZ or internal zones |
| Conjur Follower          | DMZ      | Read-only replica pulling secrets from internal Conjur Master            |
| Secrets Provider for K8s | DMZ      | Sidecar or CSI driver to inject secrets into Kubernetes workloads        |
| SIEM/SOAR                | Internal | Receives logs and alerts from CyberArk and Kubernetes                    |

---

## 4. Deployment Guidelines

### 4.1 Kubernetes Network Architecture

* **Single-homed worker nodes** in DMZ only (no dual interfaces)
* **Control plane** options:

  * Fully in DMZ (isolated clusters)
  * Internal (centralized control)
* **Kubernetes Network Policies** for intra-cluster segmentation

### 4.2 Communication Flows

| Source           | Destination     | Protocol     | Direction      | Purpose               |
| ---------------- | --------------- | ------------ | -------------- | --------------------- |
| Secrets Provider | Conjur Follower | Local socket | Internal       | Secret injection      |
| Conjur Follower  | Conjur Master   | HTTPS        | DMZ → Internal | Read-only secret sync |
| PSM Gateway      | PVWA            | HTTPS        | DMZ → Internal | Session brokering     |
| PSM Gateway      | Target Systems  | SSH/RDP      | Outbound       | Privileged access     |

All communication is firewall-controlled and authenticated via TLS and mutual verification.

---

## 5. Integration Patterns

### Pattern A: Secret Injection via Conjur

* **Use case**: Applications in DMZ require secure DB/API credentials
* **Mechanism**: Sidecar container fetches secret via Conjur Follower
* **Control**: Kubernetes RBAC + Conjur policy enforcement

### Pattern B: PSM Gateway Access to DMZ Targets

* **Use case**: Admins access DMZ servers through PAM with full session monitoring
* **Mechanism**: Session initiated from PVWA or API → PSM Gateway → Target

### Pattern C: Outbound API Calls from DMZ Workloads

* **Use case**: Workloads require CyberArk API (e.g., secret rotation)
* **Mechanism**: Mutual TLS, egress proxy, and fine-grained API permissions

---

## 6. Compliance Alignment

| Standard               | Compliance Aspect                                                   |
| ---------------------- | ------------------------------------------------------------------- |
| **NIST SP 800-207**    | Identity-aware routing, session control, trust enforcement          |
| **ISO/IEC 27001:2022** | A.9 (Access), A.13 (Segmentation), A.12 (Operations)                |
| **PCI DSS v4.0**       | DMZ isolation, session logs, outbound restrictions                  |
| **DORA / NIS2**        | Access traceability, segmentation, control of privileged operations |

---

## 7. Enhancements and Best Practices

* **Egress proxy/API gateway** (e.g., Envoy) to restrict outbound traffic
* **Mutual TLS authentication** between workloads and PAM endpoints
* **Runtime admission controllers** (OPA, Kyverno) for policy enforcement
* **Kubernetes audit logging** with forwarding to CyberArk and SIEM
* **Dynamic secrets** via CyberArk APIs (vaultless Just-in-Time access)

---

## 8. Summary

Running Kubernetes in a DMZ under Zero Trust principles is viable and secure with CyberArk integration. All communication must be explicitly allowed, identity-aware, and auditable. CyberArk components such as PSM Gateway, Conjur, and Secrets Provider enable strong access control and secrets delivery without violating segmentation boundaries or exposing privileged systems.
