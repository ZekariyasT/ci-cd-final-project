# Exercise 8: OpenShift Pipeline Setup Guide

This guide provides step-by-step instructions for creating the OpenShift CD pipeline.

## Step 1: Install Tekton Tasks

In your lab terminal, run:

```bash
kubectl apply -f .tekton/tasks.yml
```

This installs the three custom tasks:
- `cleanup`
- `eslint`
- `jest-test`

Verify the tasks are installed:
```bash
kubectl get tasks
```

## Step 2: Create PVC (Persistent Volume Claim)

### Option A: Using Terminal

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

### Option B: Using OpenShift Console

1. Go to OpenShift Console → Administrator perspective
2. Navigate to **Storage** → **PersistentVolumeClaims**
3. Click **Create PersistentVolumeClaim**
4. Configure:
   - **Name**: `oc-lab-pvc`
   - **Storage class**: `skills-network-learner`
   - **Access mode**: `ReadWriteOnce`
   - **Size**: `1Gi`
5. Click **Create**

**Assessment**: Take a screenshot of the PVC details page and save as `oc-pipelines-console-pvc-details.png`

## Step 3: Create Pipeline in OpenShift Console

1. Go to OpenShift Console → **Pipelines** → **Pipelines**
2. Click **Create Pipeline**
3. Configure the pipeline:

### Pipeline Configuration:
- **Name**: (your choice, e.g., `ci-cd-pipeline`)
- **Workspace**: 
  - **Name**: `output`
  - **Type**: **PersistentVolumeClaim**
  - **PersistentVolumeClaim**: `oc-lab-pvc`

### Add Steps in Order:

1. **cleanup**
   - Task: `cleanup`
   - Workspace: `output` → `output`

2. **git-clone**
   - Task: `git-clone` (from Tekton Catalog)
   - Parameters:
     - `url`: Your GitHub repository URL
     - `revision`: `main` (or your branch)
   - Workspace: `output` → `output`

3. **eslint**
   - Task: `eslint`
   - Workspace: `output` → `source`

4. **jest-test**
   - Task: `jest-test`
   - Workspace: `output` → `source`

5. **buildah**
   - Task: `buildah` (from Tekton Catalog)
   - Parameters:
     - `IMAGE`: Your image name (e.g., `image-registry.openshift-image-registry.svc:5000/<namespace>/<app-name>:latest`)
     - `DOCKERFILE`: `./Dockerfile`
     - `CONTEXT`: `$(workspaces.source.path)`
   - Workspace: `output` → `source`

6. **openshift-client** (for deployment)
   - Task: `openshift-client` (from Tekton Catalog)
   - Parameters:
     - `SCRIPT`: 
       ```bash
       oc create deployment $(params.app-name) --image=$(params.build-image) --dry-run=client -o yaml | oc apply -f -
       ```
   - Additional Parameters:
     - `app-name`: Your application name (e.g., `counter-service`)
     - `build-image`: The image built in the buildah step

## Step 4: Test the Pipeline

1. Go to **Pipelines** → Your pipeline
2. Click **Actions** → **Start**
3. Fill in required parameters if any
4. Monitor the pipeline run

**Assessment**: 
- Take a screenshot showing all pipeline steps and save as `oc-pipelines-oc-final.png`
- Take a screenshot of successful pipeline run (green status) and save as `oc-pipelines-oc-green.png`

## Step 5: Verify Application Deployment

1. Go to **Workloads** → **Deployments**
2. Find your deployment
3. Check the pods are running
4. View application logs

**Assessment**:
- **Option 1 (AI Graded)**: Copy the output showing `SERVICERUNNING` and save in `oc-pipeline-app-logs.txt`
- **Option 2 (Peer Graded)**: Take a screenshot showing `SERVICERUNNING` and save as `oc-pipeline-app-logs.png`

## Important Notes

- Make sure you're logged into the OpenShift cluster
- Ensure you have the correct namespace selected
- The workspace must be shared across all tasks
- Image registry path format: `image-registry.openshift-image-registry.svc:5000/<namespace>/<image-name>:<tag>`
- For the deployment step, ensure the `build-image` parameter references the image built by buildah

## Troubleshooting

- If tasks don't appear, verify they're installed: `kubectl get tasks`
- If PVC issues occur, check storage class availability
- If buildah fails, verify Dockerfile path and image registry permissions
- If deployment fails, check image reference and namespace permissions
