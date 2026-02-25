# Exercise 8: Quick Command Reference

## 1. Install Tekton Tasks

```bash
kubectl apply -f .tekton/tasks.yml
```

Verify installation:
```bash
kubectl get tasks
```

## 2. Create PVC via Terminal

```bash
oc create -f - <<EOF
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: oc-lab-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: skills-network-learner
EOF
```

Verify PVC:
```bash
oc get pvc oc-lab-pvc
```

## 3. Verify Tasks are Available

```bash
# List all tasks
kubectl get tasks

# List cluster tasks (git-clone, buildah, openshift-client should be available)
kubectl get clustertasks
```

## 4. Check Pipeline Status (after creation)

```bash
# List pipelines
oc get pipelines

# List pipeline runs
oc get pipelineruns

# View specific pipeline run details
oc describe pipelinerun <run-name>

# View pipeline run logs
tkn pipelinerun logs <run-name>
```

## 5. Check Deployment Status

```bash
# List deployments
oc get deployments

# List pods
oc get pods

# View pod logs
oc logs <pod-name>

# View deployment logs
oc logs deployment/<app-name>
```

## 6. Useful OpenShift Console URLs

After creating resources, you can access:
- **Pipelines**: `/pipelines/ns/<namespace>/pipelines`
- **Pipeline Runs**: `/pipelines/ns/<namespace>/pipelineruns`
- **PVCs**: `/k8s/cluster/persistentvolumeclaims`
- **Deployments**: `/k8s/ns/<namespace>/deployments`

## Notes

- Replace `<namespace>` with your actual OpenShift namespace
- Replace `<app-name>` with your application name
- Replace `<run-name>` with the actual pipeline run name
- Replace `<pod-name>` with the actual pod name
