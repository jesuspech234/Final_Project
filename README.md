# Password Manager - Final Project

## Overview

This project is the final task for the DevSecOps course. It involves the development of a Password Manager application, integrating version control, CI/CD, containerization, testing, code quality, and security practices using Python 3.12.

## Project Structure

- **ci.yml:** GitHub Actions workflow for CI/CD pipeline.
- **Dockerfile:** Configuration file to build the Docker image for the application.
- **docker-compose.yml:** Configuration for Docker Compose to orchestrate the application and database services.
- **requirements.txt:** List of dependencies required by the project.
- **.flake8:** Configuration for Flake8 to ensure code quality.
- **test_app.py:** Unit test for the application's home page.

## 1. Source Code Management

The project uses Git for version control with the following branch structure:
- **main:** Production-ready code.
- **development:** Active development branch.

## 2. Integration and Continuous Delivery (CI/CD)

GitHub Actions is configured to automate the CI/CD pipeline. The pipeline includes the following steps:

- **Python Setup:** Sets up Python 3.12.
- **Dependency Installation:** Installs project dependencies from `requirements.txt`.
- **Testing:** Runs unit tests using `pytest`.
- **Security Analysis:** Checks for vulnerabilities using Snyk.

### CI/CD Configuration (`ci.yml`)

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main
      - development
  pull_request:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Set up Python 3.12
      uses: actions/setup-python@v4
      with:
        python-version: '3.12'

    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt

    - name: Run tests
      run: |
        pytest

    - name: Run Snyk to check vulnerabilities
      run: snyk test

### Containerization
The application is containerized using Docker with the following configurations:

Dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]

### Docker Compose (docker-compose.yml)

version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    environment:
      FLASK_ENV: production
  db:
    image: postgres:alpine
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydatabase
    ports:
      - "5432:5432"

### 4. Testing and Code Quality
The project uses pytest for testing and flake8 for code quality. The configurations are as follows:

Flake8 Configuration (.flake8)

[flake8]
max-line-length = 88

### Unit Test (test_app.py)

from app import app

def test_home_page():
    response = app.test_client().get('/')
    assert response.status_code == 200
    assert b"Welcome" in response.data

## Security
Snyk is integrated into the CI/CD pipeline to check for vulnerabilities in dependencies.

## Installation
To set up the project locally, follow these steps:

### Clone the Repository:

git clone https://github.com/yourusername/your-repository.git
cd your-repository
Build and Run the Application with Docker Compose:

bash
Copy code
docker-compose up --build
Access the Application:
The application should be accessible at http://localhost:5000
