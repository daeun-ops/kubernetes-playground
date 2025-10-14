# Lab 01 — Secure Tenant Setup (Multi-tenancy Hardening)

This lab demonstrates production-grade tenant isolation on OKD 4.x:
NetworkPolicies, SCC bindings, ResourceQuota, and topology-aware scheduling.

---

## Objective
Simulate a restricted namespace where developers cannot escalate privileges or overuse cluster resources.

---

## Apply All
```bash
oc apply -f namespace.yaml
oc apply -f sa-scc-binding.yaml
oc apply -f networkpolicy.yaml
oc apply -f quota-limits.yaml
oc apply -f app-deployment.yaml
