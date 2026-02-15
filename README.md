---

# Flask Weather App 🌤️

A simple web application built with **Flask** that fetches and displays current weather information for any city using the **OpenWeatherMap API**.

---

## Features

* Enter any city name and get:

  * Temperature in Celsius
  * Weather description (e.g., clear sky, rain)
* Handles invalid city names gracefully
* Simple, clean web interface
* Dockerized for easy deployment
* CI/CD pipeline using **GitHub Actions** and **ArgoCD**

---

## Project Structure

```
weather-app/
│
├── venv/                  # Python virtual environment
├── src/
│   ├── app.py             # Flask application
│   ├── requirements.txt   # Python dependencies
│   └── templates/
│       └── index.html     # HTML template
├── deploy/
│   └── deployment.yaml    # Kubernetes deployment manifest
├── Dockerfile             # For containerizing the app
├── .dockerignore          # Files to ignore in Docker build
└── .github/workflows/
    └── ci-cd.yml          # GitHub Actions workflow
```

---

## Prerequisites

* Python 3.10+ installed
* `virtualenv` or `venv` module
* Docker installed locally
* Kubernetes cluster (for ArgoCD deployment)
* OpenWeatherMap API key (free API key from [OpenWeatherMap](https://openweathermap.org/api))

---

## Running Locally

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd weather-app
```

### 2. Create a virtual environment

```bash
python3 -m venv venv
```

### 3. Activate the virtual environment

```bash
# macOS / Linux
source venv/bin/activate

# Windows (PowerShell)
venv\Scripts\activate
```

### 4. Install dependencies

```bash
python3 -m pip install --upgrade pip
python3 -m pip install -r src/requirements.txt
```

### 5. Set your OpenWeatherMap API key

```bash
export WEATHER_API_KEY="your_api_key_here"  # macOS / Linux
setx WEATHER_API_KEY "your_api_key_here"    # Windows
```

### 6. Run the Flask app

```bash
cd src
python app.py
```

* Open your browser at [http://127.0.0.1:5000](http://127.0.0.1:5000)
* Enter a city name and view the weather

---

## Docker Deployment

### 1. Build the Docker image

```bash
docker build -t hagersaad329/weather-app:latest .
```

### 2. Run the Docker container

```bash
docker run -d -p 5000:5000 --name weather-app hagersaad329/weather-app:latest
```

* Open [http://localhost:5000](http://localhost:5000) to use the app in a container

---

## CI/CD with GitHub Actions & ArgoCD

This project uses GitHub Actions to:

1. Build and test the Python application
2. Run **flake8** for linting
3. Build a Docker image and push it to Docker Hub
4. Update the Kubernetes deployment manifest (`deploy/deployment.yaml`) with the new Docker image tag
5. Commit the updated manifest back to the repository
6. ArgoCD detects the change and automatically deploys the new version

### Workflow Highlights

* The image tag is automatically generated using the timestamp, e.g., `v20260215124801`
* The deployment YAML is updated with the new image tag using `sed`
* GitHub Actions pushes changes back to the `main` branch
* ArgoCD syncs the deployment to your Kubernetes cluster

---

## Kubernetes Deployment

* The `deploy/deployment.yaml` file defines a simple Deployment with:

  * 2 replicas
  * Container port 5000
  * Auto-updated image via CI/CD

* Example manifest snippet:

```yaml
containers:
- name: python-app
  image: hagersaad329/weather-app:latest
  ports:
  - containerPort: 5000
```

---

password


kubectl -n argocd get secret argocd-initial-admin-secret \
  -o jsonpath="{.data.password}" | base64 -d && echo
