# Final Project Evaluation Checklist

## Repository Information
- **Repository URL**: `https://github.com/ZekariyasT/ci-cd-final-project.git`
- **Main Branch**: `main`

---

## Option 1: AI-Graded Submission Checklist

### ✅ Task 1: README.md with Project Name (2 points)
- **Status**: ✅ Complete
- **GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/README.md`
- **Verification**: README contains project name "ci-cd-final-project" and course details

### ✅ Task 2: GitHub Workflow with Lint and Test Steps (4 points)
- **Status**: ✅ Complete
- **GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml`
- **Required Code Snippets**:
  - **Lint Step** (Lines 26-27):
    ```yaml
    - name: Lint with ESLint
      run: npm run lint
    ```
  - **Test Step** (Lines 29-30):
    ```yaml
    - name: Run unit tests with Jest
      run: npm test
    ```

### ✅ Task 3: Tekton Tasks with Cleanup and Jest-test (4 points)
- **Status**: ✅ Complete
- **GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml`
- **Required Code Snippets**:
  - **Cleanup Task** (Lines 1-35): Complete cleanup task definition
  - **Jest-test Task** (Lines 61-83): Complete jest-test task definition

### ⚠️ Task 4: OpenShift PVC Screenshot (2 points)
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `oc-pipelines-console-pvc-details.png`
- **Instructions**:
  1. Go to OpenShift Console → Administrator perspective
  2. Navigate to **Storage** → **PersistentVolumeClaims**
  3. Click on `oc-lab-pvc`
  4. Take a screenshot showing the PVC details
  5. Save as `oc-pipelines-console-pvc-details.png`

### ⚠️ Task 5: GitHub Actions Validation Text (2 points)
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `cicd-github-validate.txt`
- **Instructions**:
  1. Install GitHub CLI: `gh auth login` (if not already done)
  2. Run: `gh run list` to see workflow runs
  3. Run: `gh run view <run-id>` to see details
  4. Copy the terminal output
  5. Paste into `cicd-github-validate.txt`
- **Alternative**: If GitHub CLI is not available, you can copy the output from the GitHub Actions web interface

### ⚠️ Task 6: OpenShift Pipeline Details Screenshot (2 points)
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `oc-pipelines-oc-final.png`
- **Instructions**:
  1. Go to OpenShift Console → **Pipelines** → **Pipelines**
  2. Click on your pipeline
  3. Take a screenshot showing all pipeline steps (cleanup, git-clone, eslint, jest-test, buildah, openshift-client)
  4. Save as `oc-pipelines-oc-final.png`

### ⚠️ Task 7: OpenShift Pipeline Success Screenshot (2 points)
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `oc-pipelines-oc-green.png`
- **Instructions**:
  1. Go to OpenShift Console → **Pipelines** → **Pipeline Runs**
  2. Click on a successful (green) pipeline run
  3. Take a screenshot showing the successful run with all steps completed
  4. Save as `oc-pipelines-oc-green.png`

### ⚠️ Task 8: OpenShift Application Logs Text (2 points)
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `oc-pipeline-app-logs.txt`
- **Instructions**:
  1. Go to OpenShift Console → **Workloads** → **Pods**
  2. Click on your application pod
  3. Go to **Logs** tab
  4. Find the log line containing `SERVICERUNNING`
  5. Copy the relevant log output
  6. Save in `oc-pipeline-app-logs.txt`
- **Alternative Terminal Command**:
  ```bash
  oc logs deployment/<app-name> | grep -i "SERVICERUNNING" > oc-pipeline-app-logs.txt
  ```

---

## Option 2: Peer-Graded Submission Checklist

### ✅ Task 1: GitHub Repository URL
- **Status**: ✅ Complete
- **URL**: `https://github.com/ZekariyasT/ci-cd-final-project.git`

### ✅ Task 2: GitHub Workflow Linting Step URL
- **Status**: ✅ Complete
- **GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L26-L27`
- **Direct Link to Lint Step**: Lines 26-27

### ✅ Task 3: GitHub Workflow Test Step URL
- **Status**: ✅ Complete
- **GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L29-L30`
- **Direct Link to Test Step**: Lines 29-30

### ✅ Task 4: Tekton Cleanup Task URL
- **Status**: ✅ Complete
- **GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml#L1-L35`
- **Direct Link to Cleanup Task**: Lines 1-35

### ✅ Task 5: Tekton Test Task URL
- **Status**: ✅ Complete
- **GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml#L61-L83`
- **Direct Link to Jest-test Task**: Lines 61-83

### ⚠️ Task 6: OpenShift PVC Screenshot
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `oc-pipelines-console-pvc-details.png`
- **Same as Option 1, Task 4**

### ⚠️ Task 7: GitHub Actions Success Screenshot
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `cicd-github-validate.png`
- **Instructions**:
  1. Go to your GitHub repository
  2. Click on **Actions** tab
  3. Click on a successful workflow run
  4. Take a screenshot showing all steps completed successfully
  5. Save as `cicd-github-validate.png`

### ⚠️ Task 8: OpenShift Pipeline Details Screenshot
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `oc-pipelines-oc-final.png`
- **Same as Option 1, Task 6**

### ⚠️ Task 9: OpenShift Pipeline Success Screenshot
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `oc-pipelines-oc-green.png`
- **Same as Option 1, Task 7**

### ⚠️ Task 10: OpenShift Application Logs Screenshot
- **Status**: ⚠️ Pending - Action Required
- **File Name**: `oc-pipeline-app-logs.png`
- **Instructions**:
  1. Go to OpenShift Console → **Workloads** → **Pods**
  2. Click on your application pod
  3. Go to **Logs** tab
  4. Find and highlight the log line containing `SERVICERUNNING`
  5. Take a screenshot
  6. Save as `oc-pipeline-app-logs.png`

---

## Quick Reference: GitHub URLs

### Main Files:
- **README.md**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/README.md`
- **Workflow.yml**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml`
- **Tasks.yml**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml`

### Direct Links to Code Snippets:
- **Lint Step**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L26-L27`
- **Test Step**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L29-L30`
- **Cleanup Task**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml#L1-L35`
- **Jest-test Task**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml#L61-L83`

---

## Notes

- All code files are committed and pushed to GitHub ✅
- Screenshots need to be taken from the OpenShift lab environment
- Text files need to be created with actual output from commands/logs
- Make sure all screenshots are clear and show the required information
- Verify all file names match exactly as specified in the requirements
