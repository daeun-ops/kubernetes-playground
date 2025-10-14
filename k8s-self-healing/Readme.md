# 🩺 Kubernetes Self-Healing Playground

> Explore Kubernetes health probes through hands-on experiments.  
> Each folder demonstrates a different mechanism for keeping your Pods alive and responsive.

| Lab | Concept | Description |
|-----|----------|-------------|
| 01 | Liveness Probe | Automatically restart unhealthy pods |
| 02 | Readiness Probe | Control traffic flow to ready pods |
| 03 | Startup Probe | Handle slow-starting containers |
| 04 | Combined | Real-world probe configuration example |

Run each folder independently:
```bash
kubectl apply -f 01-liveness-probe/deployment.yaml
