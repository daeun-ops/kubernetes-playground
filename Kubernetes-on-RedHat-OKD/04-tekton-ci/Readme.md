

###  `04-tekton-ci/README.md`
```markdown
#  Lab 04 — CI/CD with Tekton & Buildah

Containerize, build, and deploy workloads using OpenShift Pipelines (Tekton).

---

##  Objective
Build OCI image inside OKD cluster using Buildah — no Docker daemon required.

---

##  Apply
```bash
oc apply -f sa.yaml
oc apply -f task-buildah.yaml
oc apply -f pipeline.yaml
oc apply -f pipelinerun.yaml
