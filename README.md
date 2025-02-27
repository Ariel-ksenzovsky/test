Here’s the entire content formatted in Markdown for your **README.md**:

```markdown
# Flask Catexer App with GitHub Actions

This repository contains a Flask-based application integrated with GitHub Actions for CI/CD automation.

## Features
- **Flask Web Application**: A lightweight Python web app.
- **GitHub Actions CI/CD**: Automated testing and deployment.
- **Docker Support**: Containerized for easy deployment.
- **Cloud Integration**: Ready for deployment to AWS/GCP.
- **Infrastructure as Code**: Terraform for cloud provisioning and Helm for Kubernetes deployment.
- **Monitoring & Logging**: Integrated Prometheus, Grafana, Fluentd, and Loki for observability.
  - **Prometheus**: Collects application and infrastructure metrics.
  - **Grafana**: Visualizes data through dashboards.
  - **Loki**: Collects and stores logs for easy querying and analysis.

## Prerequisites
Ensure you have the following installed:
- **Python 3.8+**
- **Docker** (optional, for containerized deployment)
- **GitHub Actions enabled**
- **Terraform** (for cloud infrastructure provisioning)
- **Helm** (for Kubernetes deployment)

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/OmriFialkov/flask-catexer-app-actions.git
cd flask-catexer-app-actions
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Run Locally
```bash
flask run
```
The app will be accessible at `http://127.0.0.1:5000/`.

## GitHub Actions CI/CD Pipeline
This repository includes a GitHub Actions workflow to automate testing and deployment:
- **Linting & Testing**: Runs on each pull request.
- **Docker Build & Push**: Builds and pushes the Docker image.
- **Deployment**: Deploys to a cloud provider (if configured).

## Infrastructure as Code (IaC)

### Terraform
Terraform is used to provision cloud infrastructure. The Terraform configuration in this repository includes:
- **EC2 instances / GCP VM instances**
- **Networking components (VPC, subnets, security groups)**
- **IAM roles and policies**

To apply the Terraform configuration:
```bash
cd terraform
terraform init
terraform apply -auto-approve
```

### Helm Deployment
Helm is used to deploy the Flask application to Kubernetes. The repository includes a Helm chart to manage application deployment.

To install the application using Helm:
```bash
helm repo add catexer-repo <your-helm-repo-url>
helm install flask-catexer catexer-repo/flask-catexer --values helm/values.yaml
```

For updates:
```bash
helm upgrade flask-catexer catexer-repo/flask-catexer --values helm/values.yaml
```

## Monitoring & Logging
This project integrates monitoring and logging to ensure observability:

### Prometheus & Grafana
- **Prometheus**: Collects application and infrastructure metrics.
- **Grafana**: Visualizes data through dashboards.

To deploy Prometheus and Grafana using Helm:
```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install monitoring prometheus-community/kube-prometheus-stack
```
Access Grafana:
```bash
kubectl port-forward svc/monitoring-grafana 3000:80 -n monitoring
```
Login credentials (default):
- **User**: admin
- **Password**: prom-operator (can be changed via Helm values)

### Fluentd (Logging)
- **Fluentd** collects logs from the application and forwards them to a centralized storage (Elasticsearch, Loki, etc.).
- Ensure Fluentd is deployed in Kubernetes:
```bash
helm repo add fluent https://fluent.github.io/helm-charts
helm install fluentd fluent/fluentd
```

## Environment Variables and Secrets
This README outlines key environment variables and secrets used for the configuration of the application and deployment processes.

### List of Variables and Secrets
#### GitHub Secrets:
- `dockeruser`: Docker username for login.
- `dockertoken`: Docker token (password) for login.
- `MYSQL_PASSWORD`: MySQL password for authentication.
- `MYSQL_ROOT_PASSWORD`: MySQL root password.
- `HELM_REPO_PAT`: Personal Access Token for Helm repository access.
- `AWS_ACCESS_KEY_ID`: AWS credentials for accessing S3 and other AWS services.
- `AWS_SECRET_ACCESS_KEY`: AWS secret key for S3 and other AWS services.
- `GCP_SA_KEY`: Google Cloud Service Account Key for GCP access.
- `GCP_PROJECT_ID`: Google Cloud Project ID.
- `GCP_CLUSTER_NAME`: Google Cloud Kubernetes cluster name.
- `GCP_ZONE`: Google Cloud zone for the Kubernetes cluster.

#### Defined in vars:
- `FLASK_ENV`: Environment for Flask (e.g., development or production).
- `MYSQL_HOST`: Host for the MySQL database.
- `MYSQL_USER`: MySQL user.
- `MYSQL_DATABASE`: The MySQL database name.
- `PORT`: Port for Flask to run on.
- `IMAGE_TAG`: Docker image tag, generated dynamically based on the GitHub run number.
- `IMAGE_NAME`: Docker image name (`crazyguy888/catexer-actions`).

## Docker Image Cleanup in CD Pipeline

To maintain a clean and efficient container registry, the CD pipeline includes an automatic cleanup of old Docker images. This process ensures that only the most recent and relevant images are stored, while outdated or unused images are removed, helping to free up storage space.

### Cleanup Process
During the deployment process, the CI/CD pipeline performs the following cleanup steps:

1. **Identifying Unused Images**: The pipeline scans for Docker images that are no longer in use, based on criteria like image age or usage frequency.
   
2. **Removing Old Images**: Any old or unused images are automatically deleted from the Docker registry.

3. **Regular Cleanup**: This cleanup is executed periodically as part of the deployment pipeline, ensuring that outdated images are removed without manual intervention.

By implementing this cleanup process, the project helps prevent the accumulation of unnecessary Docker images, ensuring a streamlined and efficient development environment.

## Contributing
Feel free to open issues or submit pull requests to improve the project.

## License
This project is licensed under the MIT License.
```

This is your **README.md** with the entire content formatted in Markdown. You can copy and paste this directly into your repository's README file. Let me know if you need anything else!
