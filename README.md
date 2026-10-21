# CI/CD Pipeline with GitHub Actions and Docker

## Project Overview

This project demonstrates how to build a Continuous Integration and Continuous Deployment (CI/CD) pipeline using GitHub Actions and Docker. The pipeline automatically tests the application, builds a Docker image, and pushes the image to Docker Hub. The published image can then be pulled and deployed locally using Docker.

The project is designed to run without AWS or any other cloud infrastructure.

## Objectives

- Automate application testing using GitHub Actions.
- Build a Docker image for a Flask web application.
- Push the Docker image to Docker Hub.
- Deploy the application locally using Docker.
- Understand the CI/CD workflow and containerization.

## Technologies Used

- **Git:** Version control
- **GitHub:** Source code repository
- **GitHub Actions:** CI/CD automation
- **Docker:** Application containerization
- **Docker Hub:** Docker image registry
- **Python:** Application programming language
- **Flask:** Web application framework
- **Pytest:** Automated testing
- **Docker Compose:** Local container management

## Project Structure

```text
cicd-docker-project/
├── app.py
├── test_app.py
├── requirements.txt
├── Dockerfile
├── docker-compose.yml
└── .github/
    └── workflows/
        └── ci-cd.yml
```

## CI/CD Pipeline Workflow

1. A developer pushes code to the `main` branch of GitHub.
2. GitHub Actions checks out the source code.
3. Python and application dependencies are installed.
4. Automated tests are executed using Pytest.
5. If the tests pass, the Docker image is built.
6. GitHub Actions authenticates with Docker Hub using GitHub Secrets.
7. The Docker image is pushed to Docker Hub with the `latest` tag.
8. The published image is pulled and run locally using Docker.

## Prerequisites

Install or create the following:

- Git for Windows / Git Bash
- Docker Desktop
- GitHub account
- Docker Hub account
- Python 3.12 or compatible Python version (for local testing)

## Application Endpoints

| Endpoint | Description |
|---|---|
| `/` | Displays the application home page |
| `/health` | Returns the application health status |

The health endpoint returns:

```json
{
  "status": "healthy"
}
```

## Setup and Execution

### 1. Clone the Repository

```bash
git clone https://github.com/sreeja1628/cicd-docker-project.git
cd cicd-docker-project
```

### 2. Run Tests Locally

```bash
python -m pip install -r requirements.txt
python -m pip install pytest
python -m pytest -v
```

### 3. Build the Docker Image

```bash
docker build -t cicd-docker-app:local .
```

### 4. Run the Application Using Docker Compose

```bash
docker compose up -d
```

Open the application in your browser:

http://localhost:5000

Check the health endpoint:

http://localhost:5000/health

### 5. Configure GitHub Secrets

In your GitHub repository, navigate to:

**Settings → Secrets and variables → Actions → New repository secret**

Create the following secrets:

| Secret Name | Value |
|---|---|
| `sreejakambathula` | Your Docker Hub username |
| `DOCKERHUB_TOKEN` | Your Docker Hub access token |

Never commit access tokens or passwords to your repository.

### 6. Run the CI/CD Pipeline

Push a change to the `main` branch:

```bash
git add .
git commit -m "Update application"
git push origin main
```

Open the **Actions** tab in your GitHub repository to monitor the workflow.

The pipeline runs the tests first. The Docker image is published only after the tests succeed.

### 7. Pull and Deploy the Published Image

```bash
docker pull sreeja1628/cicd-docker-app:latest
```

Run the container:

```bash
docker run -d --name cicd-demo -p 5000:5000 sreeja1628/cicd-docker-app:latest
```

Verify the running container:

```bash
docker ps
```

Access the application:

http://localhost:5000

### 8. Stop the Application

For the Docker Compose deployment:

```bash
docker compose down
```

For the container created using `docker run`:

```bash
docker stop cicd-demo
docker rm cicd-demo
```

## GitHub Actions Workflow

The workflow is located at:

`.github/workflows/ci-cd.yml`

It contains two jobs:

- **Run Tests:** Installs dependencies and runs automated tests.
- **Build and Push Docker Image:** Builds and publishes the Docker image after the test job succeeds.

Pull requests run the test job but do not publish an image.

## Expected Results

After completing the project, you should have:

- A GitHub repository containing the application source code and CI/CD workflow.
- Successful automated test results in GitHub Actions.
- A Docker image published to Docker Hub.
- A locally deployed Flask application accessible through a web browser.
- Screenshots demonstrating the successful pipeline and deployment.

## Deliverables

1. GitHub repository URL.
2. Docker Hub image URL.
3. Screenshot of the successful GitHub Actions workflow.
4. Screenshot of the Docker Hub repository and image tag.
5. Screenshot of the application running locally.

## Conclusion

This project demonstrates how GitHub Actions can automate testing, Docker image creation, and publishing to Docker Hub. It provides practical experience with CI/CD, version control, containerization, automated testing, and local application deployment without requiring cloud infrastructure.

