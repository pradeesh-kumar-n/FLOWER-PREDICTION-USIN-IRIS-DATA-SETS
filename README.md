# Iris Flower Prediction API

A machine learning-powered REST API for predicting Iris flower species based on sepal and petal measurements. This project uses a Random Forest classifier trained on the classic Iris dataset and exposes a simple Flask-based API for inference and health checks.

## Overview

This project demonstrates a complete end-to-end ML workflow:

- Loading the Iris dataset
- Training a classification model
- Saving the trained model to disk
- Serving predictions via a REST API
- Containerizing the application with Docker

The system predicts one of the three Iris species:

- Setosa
- Versicolor
- Virginica

## Features

- Predicts Iris flower species from four numeric features
- Exposes health and prediction endpoints
- Uses a trained `RandomForestClassifier`
- Includes a test script to validate API behavior
- Docker-ready deployment configuration

## Tech Stack

- Python 3.9
- Flask
- scikit-learn
- NumPy
- Docker

## Project Structure

```text
FLOWER-PREDICTION-USIN-IRIS-DATA-SETS/
├── my-api/
│   ├── app.py                 # Flask API application
│   ├── train_model.py         # Model training and serialization
│   ├── iris.pkl              # Trained model artifact
│   ├── requirements.txt      # Python dependencies
│   ├── dockerfile            # Docker build instructions
│   ├── .dockerignore         # Files excluded from Docker context
│   ├── test_api.py           # Example API test script
│   └── README.md             # Project-level usage guide (optional)
└── README.md                 # Repository overview
```

## Model Details

The application trains a `RandomForestClassifier` using the `sklearn.datasets.load_iris()` dataset. The dataset contains four input features:

- Sepal length
- Sepal width
- Petal length
- Petal width

The model is trained using a random 80/20 split and serialized to `iris.pkl` for reuse by the API.

## Getting Started

### Prerequisites

- Python 3.9+
- pip
- Virtual environment tool (optional but recommended)

### Installation

1. Clone the repository:

```bash
git clone https://github.com/pradeesh-kumar-n/FLOWER-PREDICTION-USIN-IRIS-DATA-SETS.git
cd FLOWER-PREDICTION-USIN-IRIS-DATA-SETS/my-api
```

2. Create and activate a virtual environment:

```bash
python -m venv venv
source venv/bin/activate   # Linux/macOS
# venv\Scripts\activate   # Windows
```

3. Install dependencies:

```bash
pip install -r requirements.txt
```

### Train the Model

Run the training script to generate the model artifact:

```bash
python train_model.py
```

This creates the `iris.pkl` file used by the API.

### Run the API

Start the Flask application:

```bash
python app.py
```

By default, the application runs on:

- Host: `0.0.0.0`
- Port: `5000`

## API Endpoints

### 1) Health Check

- Endpoint: `GET /health`
- Description: Verifies the API is running and the model is loaded.

Example response:

```json
{
  "status": "healthy",
  "model": "loaded"
}
```

### 2) Prediction

- Endpoint: `POST /predict`
- Description: Returns the predicted species and class probabilities.

Request body:

```json
{
  "features": [5.1, 3.5, 1.4, 0.2]
}
```

Example response:

```json
{
  "prediction": "setosa",
  "probability": {
    "setosa": 0.93,
    "virginica": 0.04,
    "versicolor": 0.03
  }
}
```

## Example Request using Python

```python
import requests

url = "http://localhost:5000/predict"
payload = {
    "features": [5.1, 3.5, 1.4, 0.2]
}

response = requests.post(url, json=payload)
print(response.json())
```

## Docker Deployment

Build the Docker image:

```bash
docker build -t iris-prediction-api .
```

Run the container:

```bash
docker run -p 5000:5000 iris-prediction-api
```

## Testing

This project includes a simple API validation script in `test_api.py`.

Run it with:

```bash
python test_api.py
```

The script sends requests to the local API and prints the health status and prediction result.

## Notes

- The trained model is stored in `iris.pkl` and loaded at runtime.
- The application is intentionally simple and easy to extend for more advanced deployment scenarios.
- The project is suitable as a foundation for ML API development, demo deployment, or classroom learning.

## Future Improvements

Potential enhancements include:

- Input validation for feature ranges and dimensions
- Enhanced error handling and logging
- Model versioning
- CI/CD automation
- Front-end interface for user interaction
- Database integration for prediction history

## Summary

This repository provides a lightweight and practical example of how to build a machine learning inference service using Python, Flask, and scikit-learn. It is a strong starting point for understanding model training, serialization, REST API development, and deployment.

