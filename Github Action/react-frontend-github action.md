# React frontend github action

Step1: cd ranjitha/Jumisa technology

Step2: touch Dockerfile

Step3: nano Dockerfile

```bash  

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
Step4: cd .github/workflows

Step5: touch docker-publish.yml

Step6: nano docker-publish.yml

```bash
name: Build and Push Docker Frontend Image

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

      # Step 2: Set up Node.js
      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '14'  # Specify the Node.js version you want to use

      # Step 3: Install Dependencies
      - name: Install Dependencies
        run: |
          cd react-hooks-frontend
          npm install

      # Optional: List files to verify contents (for debugging)
      - name: List the files
        run: |
          cd react-hooks-frontend
          ls

      # Step 4: Log in to Docker Hub
      - name: Log in to Docker Hub
        uses: docker/login-action@v1
        with:
          username: ${{ secrets.DOCKERHUB_USERNAME }}
          password: ${{ secrets.DOCKERHUB_TOKEN }}


      # Step 5: Build and push the Docker image using Buildx
      - name: Build and Push the Docker image
        uses: docker/build-push-action@v4  # Use the official build-push-action
        with:
          context: ./react-hooks-frontend  # Set the context to the directory containing the Dockerfile
          file: ./react-hooks-frontend/Dockerfile  # Specify the Dockerfile location
          push: true  # Push the image to Docker Hub after building
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/my-reactapp:latest

```

Step7: git add .

Step8: git commit -m "Added react yml"

Step9: git push origin main

Step10: check github Action.

   Added react yml workflow starts running
   
   ![Screenshot from 2024-12-04 22-46-25](https://github.com/user-attachments/assets/967ec3ad-f3c1-469b-b2c8-030456a084ad)

   
  
   After process completed image added in dockkerhub account.
   
   ![Screenshot from 2024-12-04 22-52-27](https://github.com/user-attachments/assets/4d8a4a36-8c0d-47f7-bc71-c0dda9e07720)



