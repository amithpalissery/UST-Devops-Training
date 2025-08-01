Study Log - July 29, 2025

#  **Day 12: Linting, Docker, Artifacts, DevSecOps & Kubernetes Deployment**

---

## 1. **GitHub Actions – Extended CI Pipeline**

### Includes:

* **Linting**
* **Unit Tests**
* **Docker Build**
* **Upload Artifacts**

```yaml
jobs:
  build:
    steps:
      - uses: actions/checkout@v2

      - name: Run Linter
        run: ./gradlew checkstyleMain

      - name: Unit Test
        run: ./gradlew test

      - name: Build Docker Image
        run: docker build -t my-app .

      - name: Upload Jar Artifact
        uses: actions/upload-artifact@v3
        with:
          name: app
          path: build/libs/*.jar
```

---

## 2. **CD Pipeline Stages**

| Stage           | Description                     |
| --------------- | ------------------------------- |
| Build           | Compile source code             |
| Test            | Unit & integration tests        |
| Package         | Create JAR/Docker image         |
| Artifact Upload | Save output (.jar/.zip)         |
| Deploy          | Push to server/kubernetes/cloud |

---

## 3. **Artifact, Caching, & Reporting**

* **Artifact:** Output from a job (e.g., JAR, reports)
* **Cache:** Store dependencies for faster builds

```yaml
- name: Cache Maven Repo
  uses: actions/cache@v3
  with:
    path: ~/.m2/repository
    key: ${{ runner.os }}-maven-${{ hashFiles('**/pom.xml') }}
```

* **Test Reports Badge (e.g., using Codecov):**

```yaml
- name: Upload coverage to Codecov
  uses: codecov/codecov-action@v3
```

---

## 4. **DevSecOps Integration**

### Security Stages:

| Stage   | Tool / Method                | Description                  |
| ------- | ---------------------------- | ---------------------------- |
| Linting | ESLint, Checkstyle           | Syntax & styling errors      |
| SCA     | OWASP Dependency-Check, Snyk | Detect known vulnerabilities |
| SAST    | SonarQube, Semgrep           | Static code analysis         |
| DAST    | OWASP ZAP                    | Runtime security testing     |

### Sample for OWASP ZAP:

```yaml
- name: ZAP Scan
  uses: zaproxy/action-full-scan@v0.8.0
  with:
    target: 'http://localhost:8080'
```

---

## 5. **Self-Hosted Runner**

* Used for heavier or on-prem workloads
* Registered in GitHub repo → Settings → Actions → Runners
* Installed on local/K8s VM

### Runner Setup:

```bash
./config.sh --url https://github.com/org/repo --token <token>
./run.sh
```

---

## 6. **Deploy to Kubernetes Cluster using GitHub Actions**

### Prerequisites:

* Kubeconfig access
* Docker image built & pushed (e.g., to Docker Hub or ECR)
* kubectl + context configured

### Example:

```yaml
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Setup kubectl
        uses: azure/setup-kubectl@v3
        with:
          version: '1.26.0'

      - name: Apply Manifests
        run: |
          kubectl apply -f k8s/deployment.yaml
          kubectl apply -f k8s/service.yaml
```

---

## Summary Table

| Feature                        | Tool / Command                      |
| ------------------------------ | ----------------------------------- |
| Linting                        | ESLint, Checkstyle                  |
| Unit Testing                   | JUnit, pytest                       |
| Dockerization                  | `docker build`, `docker push`       |
| Artifact Upload                | `actions/upload-artifact`           |
| Caching                        | `actions/cache`                     |
| Security Scans (SCA/SAST/DAST) | Snyk, OWASP ZAP, Semgrep            |
| Self-hosted Runner             | GitHub-hosted agent on local/K8s VM |
| Kubernetes Deployment          | `kubectl apply` via GitHub Actions  |

---

