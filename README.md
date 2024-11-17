# Object Detection API with YOLOv8 and FastAPI 🚀

Welcome to the **Object Detection API** built with **YOLOv8** and **FastAPI**. This API allows real-time object detection in images and is designed to be deployed on the cloud using **DigitalOcean**, with automated deployment through **GitHub Actions**.

## Table of Contents
- [Description](#description)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Configuration](#configuration)
- [Usage](#usage)
- [Deployment](#deployment)
- [Automation with GitHub Actions](#automation-with-github-actions)
- [Contributing](#contributing)
- [License](#license)

## Description
This API uses **YOLOv8** for object detection in images via a simple FastAPI endpoint. It's ideal for computer vision applications such as surveillance, image analysis, and more.

## Prerequisites
Before starting, make sure you have:
- Python 3.8 or higher
- Git
- Docker (for deployment on DigitalOcean)
- A [DigitalOcean account](https://m.do.co/c/eddc62174250) (with $200 free credit upon registration)

## Installation
1. **Clone the repository**:
    ```bash
    git clone https://github.com/iamdgarcia/yolo-fastapi.git
    cd object-detection-api
    ```

2. **Create and activate a virtual environment**:
    ```bash
    python -m venv myenv
    source myenv/bin/activate  # For macOS/Linux
    myenv\Scripts\activate     # For Windows
    ```

3. **Install Poetry and dependencies**:
    ```bash
    pip install poetry
    poetry install
    ```

## Configuration
Before running the API, ensure that YOLOv8 is installed:
```bash
poetry add ultralytics
```

## Usage
1. **Run the FastAPI app locally**:
    ```bash
    uvicorn main:app --reload
    ```

2. **Test the endpoint**:
   - Access `http://127.0.0.1:8000` to see the welcome page.
   - Use tools like `curl` or Postman to test the detection endpoint:
     ```bash
     curl -X POST -F "file=@image.jpg" http://127.0.0.1:8000/detect/
     ```

## Deployment
### Deploying to DigitalOcean
Follow these steps to deploy the API on DigitalOcean:
1. **Sign up** on DigitalOcean using [this referral link](https://m.do.co/c/your-referral-link) to get $200 in free credit.
2. **Create a Droplet** (virtual server) and install Docker and other necessary tools.
3. **Copy your project** to the server:
    ```bash
    git clone https://github.com/your-username/object-detection-api.git
    cd object-detection-api
    poetry install
    ```

## Automation with GitHub Actions
This repository includes a GitHub Actions workflow file to automate deployment to DigitalOcean whenever you push changes to the `main` branch.

### `.github/workflows/deploy.yml` file:
```yaml
name: Deploy to DigitalOcean

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.x'

    - name: Install Poetry and dependencies
      run: |
        pip install poetry
        poetry install

    - name: Deploy to DigitalOcean
      env:
        HOST: ${{ secrets.DIGITALOCEAN_HOST }}
        USER: ${{ secrets.DIGITALOCEAN_USER }}
      run: |
        scp -r . $USER@$HOST:/path/to/project
        ssh $USER@$HOST "cd /path/to/project && poetry install && pm2 restart all"
```

## Contributing
Contributions are welcome! If you'd like to contribute, feel free to open an issue or submit a pull request.

## License
This project is licensed under the MIT License. See the `LICENSE` file for more details.

---

Thank you for visiting this repository! If you find this project helpful, don't forget to give it a ⭐ on GitHub.