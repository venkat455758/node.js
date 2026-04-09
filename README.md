# 🚀 Node.js CI/CD Project using GitHub Actions & Docker

## 📌 Project Description
This project demonstrates how to automate the build and deployment of a Node.js application using GitHub Actions and Docker.

Whenever code is pushed to GitHub, the pipeline will:
1. Build the Node.js application
2. Create a Docker image
3. Push the image to Docker Hub

This is a basic CI/CD (Continuous Integration & Continuous Deployment) workflow.

---

## 🛠️ Technologies Used
- Node.js
- Docker
- GitHub Actions
- Docker Hub

---

## 📂 Project Structure
```
nodejs-app/
│── app.js
│── package.json
│── Dockerfile
│── .github/workflows/main.yml
│── README.md
```

---

## ⚙️ Step-by-Step Implementation

### Step 1: Create Node.js Application
- Create a simple Node.js app (`app.js`)
- Add `package.json`

Example:
```js
const http = require("http");

const server = http.createServer((req, res) => {
  res.end("Hello from Node.js CI/CD Pipeline!");
});

server.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

---

### Step 2: Create Dockerfile
This file is used to containerize the application.

```dockerfile
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```

---

### Step 3: Push Code to GitHub
- Initialize git
- Push your project to GitHub repository

---

### Step 4: Add Docker Hub Credentials
Go to:
GitHub → Settings → Secrets → Actions

Add:
- DOCKER_USERNAME
- DOCKER_PASSWORD

These are used securely in the pipeline.

---

### Step 5: Create GitHub Actions Workflow
Create file:
`.github/workflows/main.yml`

```yaml
name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Login to Docker Hub
        uses: docker/login-action@v2
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build Docker Image
        run: docker build -t ${{ secrets.DOCKER_USERNAME }}/nodejs-app .

      - name: Push Docker Image
        run: docker push ${{ secrets.DOCKER_USERNAME }}/nodejs-app
```

---

## ▶️ How the Project Works

1. Developer pushes code to GitHub
2. GitHub Actions is triggered automatically
3. It logs into Docker Hub
4. Builds Docker image from Dockerfile
5. Pushes image to Docker Hub

---

## 🧪 Run Application Locally

### Build Docker Image
```bash
docker build -t nodejs-app .
```

### Run Container
```bash
docker run -d -p 3000:3000 nodejs-app
```

Open browser:
http://localhost:3000

---

## 📦 Output
- Automated CI/CD pipeline
- Docker image available in Docker Hub
- Running Node.js application in container

---

## 🎯 Key Learnings
- CI/CD automation using GitHub Actions
- Docker image creation and management
- Secure credentials using GitHub Secrets
- Real-world DevOps workflow

---

## 👨‍💻 Author
Venkatesh Pinjala
