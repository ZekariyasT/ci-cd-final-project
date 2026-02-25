# Code Snippets Reference for Submission

This document shows the exact code snippets you need to reference in your submission.

---

## GitHub Workflow (.github/workflows/workflow.yml)

### Lint with ESLint Step
**Lines 26-27**
```yaml
      - name: Lint with ESLint
        run: npm run lint
```

**Direct GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L26-L27`

### Run unit tests with Jest Step
**Lines 29-30**
```yaml
      - name: Run unit tests with Jest
        run: npm test
```

**Direct GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L29-L30`

### Full Workflow File
**URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml`

---

## Tekton Tasks (.tekton/tasks.yml)

### Cleanup Task
**Lines 1-35**
```yaml
---
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: cleanup
spec:
  description: This task will clean up a workspace by deleting all the files.
  workspaces:
    - name: source
  steps:
    - name: remove
      image: alpine:3
      env:
        - name: WORKSPACE_SOURCE_PATH
          value: $(workspaces.source.path)
      workingDir: $(workspaces.source.path)
      securityContext:
        runAsNonRoot: false
        runAsUser: 0
      script: |
        #!/usr/bin/env sh
        set -eu
        echo "Removing all files from ${WORKSPACE_SOURCE_PATH} ..."
        # Delete any existing contents of the directory if it exists.
        #
        # We don't just "rm -rf ${WORKSPACE_SOURCE_PATH}" because ${WORKSPACE_SOURCE_PATH} might be "/"
        # or the root of a mounted volume.
        if [ -d "${WORKSPACE_SOURCE_PATH}" ] ; then
          # Delete non-hidden files and directories
          rm -rf "${WORKSPACE_SOURCE_PATH:?}"/*
          # Delete files and directories starting with . but excluding ..
          rm -rf "${WORKSPACE_SOURCE_PATH}"/.[!.]*
          # Delete files and directories starting with .. plus any other character
          rm -rf "${WORKSPACE_SOURCE_PATH}"/..?*
        fi
```

**Direct GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml#L1-L35`

### Jest-test Task
**Lines 61-83**
```yaml
---
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: jest-test
spec:
  workspaces:
    - name: source
  params:
    - name: args
      description: Arguments to pass to jest
      type: string
      default: "-v"
  steps:
    - name: jest
      image: node:20-alpine
      workingDir: $(workspaces.source.path)
      script: |
        #!/bin/sh
        set -e
        echo "Installing dependencies..."
        npm ci
        echo "Running Jest tests..."
        npm test $(params.args)
```

**Direct GitHub URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml#L61-L83`

### Full Tasks File
**URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml`

---

## README.md

**URL**: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/README.md`

Contains project name: "ci-cd-final-project" and course details.

---

## How to Use These URLs

1. **For Option 1 (AI-Graded)**: Submit the full file URLs
2. **For Option 2 (Peer-Graded)**: Submit the direct line-specific URLs for code snippets

### Example Submission Format:

**Option 1:**
- Workflow URL: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml`
- Tasks URL: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml`

**Option 2:**
- Lint Step: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L26-L27`
- Test Step: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.github/workflows/workflow.yml#L29-L30`
- Cleanup Task: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml#L1-L35`
- Jest-test Task: `https://github.com/ZekariyasT/ci-cd-final-project/blob/main/.tekton/tasks.yml#L61-L83`
