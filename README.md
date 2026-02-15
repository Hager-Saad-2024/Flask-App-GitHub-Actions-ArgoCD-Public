# Flask Weather App 🌤️

A simple web application built with **Flask** that fetches and displays current weather information for any city using the **OpenWeatherMap API**.

---

## Features

- Enter any city name and get:
  - Temperature in Celsius
  - Weather description (e.g., clear sky, rain)
- Handles invalid city names gracefully
- Simple, clean web interface

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
├── Dockerfile             # For containerizing the app
└── .dockerignore          # Files to ignore in Docker build

````

---

## Prerequisites

- Python 3.10+ installed
- `virtualenv` or `venv` module
- OpenWeatherMap API key (free API key from [OpenWeatherMap](https://openweathermap.org/api))

---

## Running Locally

### 1. Clone the repository

```bash
git clone <your-repo-url>
cd weather-app
````

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

```
