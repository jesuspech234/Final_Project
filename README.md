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
- **feature/nueva funcionalidad:** branch where modifications will be put before going to main.

## 2. Integration and Continuous Delivery (CI/CD)

GitHub Actions is configured to automate the CI/CD pipeline. The pipeline includes the following steps:

- **Python Setup:** Sets up Python 3.12.
- **Dependency Installation:** Installs project dependencies from `requirements.txt`.
- **Testing:** Runs unit tests using `pytest`.
- **Security Analysis:** Checks for vulnerabilities using Snyk.


