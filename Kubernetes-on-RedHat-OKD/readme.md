# OKD Cloud-Native Advanced Labs (Kubernetes on Red Hat OKD)

> Opinionated, production-leaning labs that showcase senior-level Kubernetes/OKD skills:
> multi-tenancy hardening, weighted blue/green via Routes, GitOps with Argo CD, Tekton CI,
> and event-driven autoscaling with KEDA — all in OKD 4.x.

## Prerequisites
- OKD 4.x cluster (cluster-admin or project-admin where required)
- `oc` CLI logged in (`oc whoami` OK)
- Optional:
  - Argo CD installed in `openshift-gitops` (or change namespace in manifests)
  - OpenShift Pipelines (Tekton) Operator installed
  - KEDA Operator installed
  - User Workload Monitoring enabled (for ServiceMonitor)

##  Labs
| # | Lab | What you’ll prove |
|---|-----|--------------------|
| 01 | **Secure Tenant** | Multi-tenancy hardening (Namespace policy set: NetworkPolicy default deny, SCC binding, ResourceQuota, LimitRange, PDB, topologySpreadConstraints) |
| 02 | **Blue/Green with Route Weights** | Zero-downtime weighted traffic shifting using **OpenShift Route alternate backends** |
| 03 | **GitOps (Argo CD)** | Declarative app delivery into OKD with **Argo CD Application** |
| 04 | **CI with Tekton** | Build & push container using **Buildah** in Tekton, deploy to OKD |
| 05 | **Event Autoscaling (KEDA)** | Scale on external events (Kafka length / Prometheus metrics), not just CPU |

---

##  How to Run

```bash
# 01 Secure Tenant
oc apply -f 01-secure-tenant/

# 02 Blue/Green with Route Weights
oc apply -f 02-bluegreen-route/
# shift traffic by editing weights in route.yaml and re-apply

# 03 GitOps (Argo CD)
oc apply -f 03-gitops-argocd/

# 04 Tekton CI
oc apply -f 04-tekton-ci/
# Then trigger PipelineRun:
oc create -f 04-tekton-ci/pipelinerun.yaml

# 05 KEDA Autoscaling
oc apply -f 05-keda-autoscale/



okd-cloud-native-labs/
├── README.md
├── 01-secure-tenant/
│   ├── namespace.yaml
│   ├── sa-scc-binding.yaml
│   ├── networkpolicy.yaml
│   ├── quota-limits.yaml
│   └── app-deployment.yaml
├── 02-bluegreen-route/
│   ├── deployments.yaml
│   └── route.yaml
├── 03-gitops-argocd/
│   ├── argocd-namespace.yaml
│   └── application.yaml
├── 04-tekton-ci/
│   ├── sa.yaml
│   ├── task-buildah.yaml
│   ├── pipeline.yaml
│   └── pipelinerun.yaml
└── 05-keda-autoscale/
    ├── deployment.yaml
    ├── scaledobject-prom.yaml
    ├── scaledobject-kafka.yaml
    └── servicemonitor.yaml





