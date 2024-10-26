# Todo-React-Spring-App

This project demonstrates the deployment of a full-stack Todo application, with a React frontend and a Spring Boot backend, on a Kubernetes cluster. The setup includes CI/CD automation using GitHub Actions and continuous deployment through Argo CD, leveraging Helm, Kubernetes manifests, and Kustomize.

---

## Development and Deployment Workflows

### GitHub Actions Workflows

The GitHub Actions workflows are located in `.github/workflows` and handle the build, push, and vulnerability scanning of Docker images for both the React UI and Spring API.

- **todo-react-image.yaml**: Builds and pushes the Docker image for the React UI.
  - **Triggers**: Executes on `push` to tags matching `client-v*.*.*` for files under the `client` directory.
  - **Key Steps**:
    - Builds and pushes the React UI Docker image.
    - Runs a vulnerability scan using Trivy.
    - Updates image tags in Kubernetes deployment files and commits the changes.
    - Creates a pull request with the updated image tag.

- **todo-spring-image.yaml**: Builds and pushes the Docker image for the Spring Boot API.
  - **Triggers**: Executes on `push` to tags matching `server-v*.*.*` for files under the `server` directory.
  - **Key Steps**:
    - Builds and pushes the Spring Boot API Docker image.
    - Runs a vulnerability scan using Trivy.
    - Updates image tags in Kubernetes deployment files and commits the changes.
    - Creates a pull request with the updated image tag.

### Argo CD Applications

The Argo CD configurations for the application deployment are defined in the `argocd` directory.

- **helm.yaml**: Uses Helm to deploy the Todo application.
  - **Source**: Points to `Deploy/todo-helm-chart/` within the repository.
  - **Destination**: Deploys to the `dev` namespace on the Kubernetes cluster.
  - **Sync Policy**: Enables automatic self-healing and pruning of resources.

- **k8s-manifesto.yaml**: Deploys the application using Kubernetes manifest files.
  - **Source**: Points to `Deploy/k8s/` within the repository.
  - **Sync Policy**: Automates the self-healing and pruning of resources.

- **kustomize.yaml**: Uses Kustomize to manage overlays for deployment.
  - **Source**: Points to `Deploy/kustomize/overlays/prod`.
  - **Sync Policy**: Configured for automatic sync, self-healing, and pruning of resources.


## Setup Instructions

### Prerequisites

- **Docker Hub Account**: Used for storing Docker images; access provided via GitHub Secrets.
- **Kubernetes Cluster**: Required for deploying the backend API using Argo CD.
- **Argo CD**: Installed on the cluster within the `argocd` namespace for GitOps management.

### Configuration and Secrets

1. **GitHub Secrets**: Add the following secrets in your GitHub repository for the GitHub Actions workflow:
   - `DOCKER_USERNAME`: Docker Hub username.
   - `DOCKER_PASSWORD`: Docker Hub password.
   - `PAT_TOKEN`: GitHub Personal Access Token (PAT) for creating pull requests.
   
2. **Directory Structure**: Ensure the repository follows the specified structure to maintain workflow consistency.

---

## Usage

1. **Build and Push the Docker Image**:
   - Push a new Git tag (e.g., `client-v1.0.0`) to initiate the GitHub Actions workflow:
     ```bash
     git tag client-v1.0.0
     git push origin client-v1.0.0
     ```
   - This triggers the workflow to build and push the Docker image, update the Kubernetes deployment YAML, and open a pull request.

2. **Deploy with Argo CD**:
   - Clone the repository and apply the Argo CD configuration to deploy the application:
     ```bash
     git clone https://github.com/panchanandevops/Todo-React-Spring-App.git
     kubectl apply -f path/to/argo-application.yaml
     ```

---

## Observability

This application’s observability is supported by **Grafana**, **Prometheus**, and **Loki** for enhanced monitoring and troubleshooting.

- **Grafana**: Provides customizable dashboards for real-time metrics visualization and alerting.
- **Prometheus**: Collects and stores time-series data, allowing for alerting on critical metrics.
- **Loki**: Manages application logs, supporting efficient debugging and analysis.

