**Challenge  – GitHub Actions Self-Hosted Runner & Docker Push Failed**

* **Issue:** GitHub Actions workflow failed while:

  * Creating a **self-hosted runner**
  * Uploading Docker image to **Docker Hub**
* **Root Cause:** I hadn’t added required **GitHub Secrets** (`DOCKER_USERNAME`, `DOCKER_PASSWORD`).
* **Resolution:** After adding the secrets securely in the repository settings, the workflow completed successfully with Docker image pushed.
