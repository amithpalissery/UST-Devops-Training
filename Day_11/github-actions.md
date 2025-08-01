Study Log - July 28, 2025
#  **Day 11: GitHub Actions, YAML, CI/CD Basics & Microservice Pipelines**

---

## 1. **YAML Syntax Basics**

* YAML: “YAML Ain’t Markup Language”
* Used for writing configuration files in GitHub Actions, Kubernetes, Docker Compose, etc.

### Key YAML Syntax:

```yaml
# Key-Value Pairs
name: CI Pipeline

# Lists
steps:
  - name: Checkout code
    uses: actions/checkout@v2

# Nested Structure (indentation matters)
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Run script
        run: echo "Hello"
```

> **Note:** Use 2 spaces for indentation. No tabs allowed.

---

## 2. **GitHub Actions Overview**

* Automates workflows like building, testing, and deploying code
* Key Concepts:

  * **Workflow:** Entire automation process (YAML file under `.github/workflows/`)
  * **Job:** A group of steps that run on the same runner
  * **Step:** Individual command or action (e.g., `run`, `uses`)
  * **Runner:** Machine where jobs are executed (GitHub-hosted or self-hosted)

---

## 3. **Workflow Triggers**

| Trigger             | Description                         |
| ------------------- | ----------------------------------- |
| `push`              | Triggered on `git push`             |
| `pull_request`      | Triggered on PR creation or updates |
| `schedule`          | Runs on a schedule (cron syntax)    |
| `workflow_dispatch` | Manual trigger                      |

### Sample Trigger:

```yaml
on:
  push:
    branches:
      - main
```

---

## 4. **Writing First CI Job (Spring Boot Example)**

```yaml
name: Build Spring Boot App

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Java
        uses: actions/setup-java@v3
        with:
          java-version: '17'

      - name: Build with Maven
        run: mvn clean install
```

---

## 5. **CI/CD in GitHub**

* **CI (Continuous Integration):** Lint, build, test when code is pushed
* **CD (Continuous Delivery/Deployment):** Automate artifact uploads or deployment to servers/clusters

---

## 6. **Microservice Pipelines**

* Create separate workflows per microservice

```
/.github/workflows/auth-service.yml
/.github/workflows/order-service.yml
```

Each pipeline can have different build steps:

```yaml
name: Build Auth Service
on:
  push:
    paths:
      - 'auth-service/**'
```

---
