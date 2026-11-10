# demo — GitHub Actions + Docker Hub CI

A basic CI workflow that builds a Docker image and publishes it to Docker Hub
whenever code is pushed to the `main` branch.

## Repository contents

- `Dockerfile` — packages a small static HTML page with Nginx.
- `index.html` — demo application page.
- `.github/workflows/docker-publish.yml` — GitHub Actions build-and-push pipeline.
- `.dockerignore` — excludes Git metadata and workflow files from the build context.

## Configure GitHub Secrets

Create a Docker Hub access token in Docker Hub, then add these repository
secrets in **Settings → Secrets and variables → Actions → New repository secret**:

- `DOCKERHUB_USERNAME` — your Docker Hub username.
- `DOCKERHUB_TOKEN` — your Docker Hub access token (do not use your account password).

## Create and push the GitHub repository

Create a new GitHub repository named `demo`, then run these commands from this
project directory:

```bash
git init
git add .
git commit -m "Add Docker Hub CI workflow"
git branch -M main
git remote add origin https://github.com/YOUR_GITHUB_USERNAME/demo.git
git push -u origin main
```

Replace `YOUR_GITHUB_USERNAME` with your GitHub username.

## Verify the workflow

1. Open the repository's **Actions** tab.
2. Open the **Build and Push Docker Image** workflow.
3. Confirm all steps complete successfully.
4. Open Docker Hub and verify that the `demo` repository contains the `latest` tag.

The published image will be:

```text
YOUR_DOCKERHUB_USERNAME/demo:latest
```

## Run the published image

```bash
docker pull YOUR_DOCKERHUB_USERNAME/demo:latest
docker run --rm -p 8080:80 YOUR_DOCKERHUB_USERNAME/demo:latest
```

Open http://localhost:8080 in your browser.
# workdflows
