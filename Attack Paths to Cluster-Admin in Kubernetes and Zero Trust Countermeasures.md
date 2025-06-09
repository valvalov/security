# Attack Paths to Cluster-Admin in Kubernetes and Zero Trust Countermeasures

## Overview

This document outlines the methods by which an attacker (or an overly privileged operator) may gain cluster-admin privileges in Kubernetes when they have access to the control plane. It also provides mitigation strategies aligned with Zero Trust principles.

---

## 1. Attack Pathways to `cluster-admin`

### 1.1 Static Pod Manipulation (kube-apiserver)

* **Target**: `/etc/kubernetes/manifests/kube-apiserver.yaml`
* **Impact**:

  * Modify `--authorization-mode` (e.g. add `AlwaysAllow`)
  * Result: full bypass of RBAC controls
* **Requires**: root access to control plane node
* **Example**:

  ```bash
  sudo vi /etc/kubernetes/manifests/kube-apiserver.yaml
  # Add: --authorization-mode=AlwaysAllow
  ```

### 1.2 Direct `etcd` Access

* **Target**: etcd data store
* **Impact**: Modify RBAC objects directly (e.g. inject ClusterRoleBinding YAML)
* **Requires**: access to etcd API + client certificates
* **Example**:

  ```bash
  ETCDCTL_API=3 etcdctl \
    --cacert=/etc/kubernetes/pki/etcd/ca.crt \
    --cert=/etc/kubernetes/pki/etcd/server.crt \
    --key=/etc/kubernetes/pki/etcd/server.key \
    get / --prefix --keys-only
  ```

### 1.3 TLS Certificate Abuse

* **Target**: Kubernetes CA and client certs
* **Impact**:

  * Create new client certificate signed by CA
  * Access API as arbitrary user (e.g. `kube-admin`)
* **Requires**: CA private key access
* **Example**:

  ```bash
  openssl genrsa -out hacker.key 2048
  openssl req -new -key hacker.key -out hacker.csr -subj "/CN=hacker"
  openssl x509 -req -in hacker.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out hacker.crt -days 365
  kubectl --client-certificate=hacker.crt --client-key=hacker.key get pods
  ```

### 1.4 ServiceAccount Token Hijacking

* **Target**: any pod with ServiceAccount mounted
* **Impact**: Use token to access API
* **Requires**: access to pod/container with elevated permissions
* **Example**:

  ```bash
  kubectl exec -it <pod> -- cat /var/run/secrets/kubernetes.io/serviceaccount/token
  export TOKEN=$(cat token)
  curl -H "Authorization: Bearer $TOKEN" https://kubernetes.default.svc/api
  ```

### 1.5 Malicious Admission Webhook

* **Target**: Kubernetes control over Pod admission
* **Impact**: Inject or mutate pods to escalate privileges
* **Requires**: ability to register a Mutating/Validating webhook
* **Example**:

  ```yaml
  apiVersion: admissionregistration.k8s.io/v1
  kind: MutatingWebhookConfiguration
  metadata:
    name: evil-webhook
  webhooks:
    - name: pod.mutate.evil.io
      clientConfig:
        service:
          name: evil-service
          namespace: evil-namespace
          path: "/mutate"
        caBundle: <base64-encoded-CA>
      rules:
        - operations: ["CREATE"]
          apiGroups: [""]
          apiVersions: ["v1"]
          resources: ["pods"]
  ```

### 1.6 Kubeconfig Leakage or Replacement

* **Target**: \~/.kube/config or externally stored kubeconfigs
* **Impact**: Reuse existing credentials with `cluster-admin` RoleBinding
* **Requires**: access to user device or storage
* **Example**:

  ```bash
  cat ~/.kube/config
  export KUBECONFIG=~/.kube/config
  kubectl get nodes
  ```

---

## 2. Zero Trust Countermeasures

### 2.1 Harden Control Plane Nodes

* Disable SSH/root access
* Treat nodes as immutable via IaC
* Isolate etcd from direct operator access

### 2.2 Certificate Authority Protection

* Secure CA private key in HSM or offline store
* Rotate certs regularly
* Monitor access to CA issuance processes

### 2.3 Restrict Use of `cluster-admin`

* Avoid assigning `cluster-admin` to real users
* Use `Role`/`RoleBinding` with minimal privileges
* Implement Just-In-Time (JIT) access via CyberArk or other PAM

### 2.4 Enforce Pod Security

* Disable automount of ServiceAccount tokens
* Use OPA/Gatekeeper to reject pods with `hostPath`, `privileged`, etc.
* Separate admin and application namespaces

### 2.5 Monitor and Audit

* Enable and export Kubernetes audit logs
* Detect creation of ClusterRoleBindings or abnormal API usage
* Integrate logs with SIEM/SOAR

### 2.6 Protect Kubeconfigs

* Store in secrets manager (e.g., CyberArk Conjur)
* Use token-based ephemeral kubeconfig delivery (JIT)
* Audit usage and download of kubeconfigs

---

## 3. Role of CyberArk in Mitigation

CyberArk can enforce strong access and audit controls around privileged operations:

* **Just-In-Time elevation** to cluster-admin via Central Policy Manager
* **PSM Gateway** for secure, audited `kubectl` sessions
* **Conjur/Secrets Provider** to avoid static tokens in workloads
* **SIEM integration** to alert on high-risk events

CyberArk does not protect the Kubernetes core (e.g., etcd or static pods), but it ensures that administrative access is controlled, monitored, and short-lived.

---

## 4. Limitations of CyberArk and Complementary Controls

CyberArk is not designed to secure the underlying Kubernetes infrastructure or its runtime components. The following table summarizes limitations and complementary tools:

| Problem Area                        | CyberArk Covers? | Complementary Tool/Approach              |
| ----------------------------------- | ---------------- | ---------------------------------------- |
| Root access to control plane node   | ❌                | Immutable infrastructure, restricted SSH |
| Kubernetes CA key protection        | ❌                | HSM, offline CA, SPIRE                   |
| TLS/network-level MitM threats      | ❌                | mTLS via Istio, SPIFFE                   |
| Malicious admission control         | ❌                | OPA/Gatekeeper, Kyverno                  |
| Binary replacement/rootkits         | ❌                | EDR/HIDS (e.g. Falco, Osquery)           |
| Kubelet runtime exec detection      | ❌                | Runtime tools (e.g. Tetragon, Sysdig)    |
| Intra-cluster service auth          | ❌                | Istio, SPIRE, Zero Trust PKI             |
| Audit & behavioral anomaly analysis | Partial          | SIEM (Splunk, Sentinel), UEBA platforms  |

---

## Conclusion

The control plane is the ultimate source of authority in Kubernetes. If compromised, the entire cluster is at risk. A Zero Trust architecture requires strict isolation, strong authentication, and real-time audit to ensure no implicit trust exists—even for operators. Combining native controls with CyberArk's PAM capabilities provides a resilient strategy against privilege escalation and abuse.

CyberArk alone is not sufficient to defend against physical or infrastructure-level compromise. It must be used in concert with network, runtime, and policy-based controls to establish true Zero Trust in Kubernetes environments.
