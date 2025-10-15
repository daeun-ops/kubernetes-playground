###  `02-bluegreen-route/README.md`
```markdown
# Lab 02 — Blue/Green Deployment with Route Weights

Perform zero-downtime deployment on OKD by leveraging Route alternateBackends with traffic weights.

---

## Objective
Shift production traffic from `web-blue` to `web-green` gradually with instant rollback capability.

---

##  Deploy Both Versions
```bash
oc apply -f deployments.yaml
oc apply -f route.yaml
