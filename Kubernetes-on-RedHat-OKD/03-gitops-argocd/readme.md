

###  `03-gitops-argocd/README.md`
```markdown
#  Lab 03 — GitOps Delivery with Argo CD

Demonstrate declarative app delivery and self-healing synchronization on OKD.

---

##  Objective
Deploy workloads automatically from Git, ensuring drift correction via Argo CD automation.

---

##  Apply
```bash
oc apply -f argocd-namespace.yaml
oc apply -f application.yaml
