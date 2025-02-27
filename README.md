# Flask Catexer App with GitHub Actions

This repository contains a Flask-based application integrated with GitHub Actions for CI/CD automation.

## Features
- **Flask Web Application**: A lightweight Python web app.
- **GitHub Actions CI/CD**: Automated testing and deployment.
- **Docker Support**: Containerized for easy deployment.
- **Cloud Integration**: Ready for deployment to AWS/GCP/Azure.

## Prerequisites
Ensure you have the following installed:
- **Python 3.8+**
- **Docker** (optional, for containerized deployment)
- **GitHub Actions enabled**

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

## Environment Variables
Configure the following variables for local or production use:
```bash
FLASK_APP=app.py
FLASK_ENV=production
DOCKER_USERNAME=<your_dockerhub_username>
DOCKER_PASSWORD=<your_dockerhub_password>
```

## Contributing
Feel free to open issues or submit pull requests to improve the project.

## License
This project is licensed under the MIT License.
