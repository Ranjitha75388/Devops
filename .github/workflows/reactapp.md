# GitHub Action

GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline.

You can create workflows that build and test every pull request to your repository, or deploy merged pull requests to production.



### Continuous Integration (CI)
CI covers the build and test stages of the pipeline. Each change in code should trigger an automated build and test, allowing the developer of the code to get quick feedback.

### Continuous Delivery / Deployment (CD)
The CD part of a CI/CD pipeline refers to Delivery and Deployment (CI/CDD anyone?!). CD takes place after the code successfully passes the testing stage of the pipeline. Continuous delivery refers to the automatic release to a repository after the CI stage. Continuous deployment refers to the automatic deployment of the artifact that has been delivered.



The four parts of the CI/CD pipeline are:

- Build stage
- Test stage
- Deliver stage
- Deploy stage

Set Up GitHub Secrets
GitHub Actions will need access to your Docker Hub account. To avoid hardcoding credentials, we will store them as GitHub secrets.

Go to your GitHub repository and navigate to Settings > Secrets and variables > Actions > New repository secret.
Create the following secrets:
DOCKERHUB_USERNAME: Your Docker Hub username.
DOCKERHUB_TOKEN: A personal access token from Docker Hub (You can create this in Docker Hub under Account Settings > Security).




in git hub settings -->secrets and variables -->Actions
DOCKERHUB_USERNAME  :ranjithalogesh
DOCKERHUB_TOKEN :token generate in Docker-hub -->Acccount setting -->security -->personal access tokens -->generate new token.




cd ranjitha/Jumisa technology
touch Dockerfile
nano Dockerfile
```
# Use the official Node.js image as a base
FROM node:14

# Set the working directory inside the container
WORKDIR /app

# Copy package.json and package-lock.json files to the working directory
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code to the working directory
COPY . .

# Expose port 3000 for the application
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]
```
cd .github/workflows
touch docker-publish.yml
nano docker-publish.yml
```
name: Build and Push Docker Image

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      # Step 1: Checkout code from the repository
      - name: Checkout code
        uses: actions/checkout@v3

      # Step 2: Set up Docker
      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v3

      # Step 3: Log in to Docker Hub
      - name: Log in to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}

      # Step 4: Build the Docker image
      - name: Build the Docker image
        run: |
          docker build -t ${{ secrets.DOCKERHUB_USERNAME }}/my-react-app:latest .

      # Step 5: Push the Docker image to Docker Hub
      - name: Push the Docker image
        run: |
          docker push ${{ secrets.DOCKERHUB_USERNAME }}/my-react-app:latest
```

Explanation:
on: push triggers the workflow whenever there is a push to the main branch.
docker/setup-buildx-action sets up Docker’s buildx tool, which is necessary for building images in GitHub Actions.
docker/login-action logs in to Docker Hub using the secrets you added earlier.
docker build builds the Docker image using the Dockerfile.
docker push pushes the built image to Docker Hub.

git add ../../Dockerfile
git add .
git commit -m "Added react yml"
git push origin main

check in github Action
