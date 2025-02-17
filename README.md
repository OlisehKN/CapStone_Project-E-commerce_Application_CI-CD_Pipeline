# CapStone Project - E-commerce Application CI/CD Pipeline

## <ins>Project Tasks:</ins>

### <ins>Task 1: Project Setup</ins>

  - Create a new GitHub repository named **ecommerce-platform**
    
![Screenshot (328)](https://github.com/user-attachments/assets/c870d5f6-a148-425d-af45-6d90c8150ace)
    
  - Inside the repository, create two directories: **api** for the backend and **webapp** for the frontend

![Screenshot (329)](https://github.com/user-attachments/assets/cf4cf2b3-90f7-4494-b68b-54efa12dc0e3)

### <ins>Task 2: Initialize GitHub Actions</ins>

  - Initialize a Git repository and add your initial project structure

      - This can be done by using the command "git init" to initialize the repository on gitbash

  - Create **.github/workflows** directory in your repository for GitHub Actions.

      - This can be done by using the command line "mkdir .github/workflows" on the terminal

![Screenshot (330)](https://github.com/user-attachments/assets/b8781591-ac3c-4f78-b1de-730f01a3a0dd)

### <ins>Task 3: Backend API Setup</ins>

  - In the **api** directory, set up a simple Node.js/Express application that handles basic e-commerce operations.

      - First, I change into change into the "api" directory and initialize the directory with the following commands on the terminal.

            cd api
            npm init -y

![Screenshot (331)](https://github.com/user-attachments/assets/4896eb72-5e94-4fda-8578-d978c769de1a)

  - Secondly, I install express and other dependencies on the backend directory with the following command

        npm install express

![Screenshot (332)](https://github.com/user-attachments/assets/71cd84c8-7284-471e-bcb0-5c8a146edb51)

  - Thridly, i created an Index.js file on the directory with the touch command.

  - Lastly, I installed and implemented unit testing on the API with the following command

        npm install --save-dev jest

![Screenshot (352)](https://github.com/user-attachments/assets/4c8d3b3a-ddfe-457f-affc-2693e0fc82d8)

### <ins>Task 4: Frontend Web Application Setup</ins>

  - In the **webapp** directory, create a simple React application that interacts with the backend API.

      - In the webapp directory, i created a react application with the following command on the terminal.

            npx create-react-app webapp

![Screenshot (335)](https://github.com/user-attachments/assets/0014654e-0d72-4af7-8f2e-6a636e18635b)

  - Then, I started the server for the application with the following

        npm start

![Screenshot (336)](https://github.com/user-attachments/assets/c7e61d7c-a866-42bd-9425-fa5845684219)
![Screenshot (337)](https://github.com/user-attachments/assets/b2f3518b-7f1e-420e-9895-e075fa64b08b)

  - Lastly, on VS Code, I implemented basic features like a product list, user login and order placement.

### <ins>Task 5: Continuous Integration Workflow</ins>

  - Write a Github Actions workflow for the backend and frontend that:

      - Installs dependencies

            name: Install
            
            on:
              push:
                branches:
                  - main
              pull_request:
                branches:
                  - main
            
            jobs:
              install_dependencies:
                runs-on: ubuntu-latest
            
                steps:
                  # Checkout the code
                  - name: Checkout repository
                    uses: actions/checkout@v2
            
                  # Set up Node.js for both backend and frontend
                  - name: Set up Node.js (backend)
                    uses: actions/setup-node@v3
                    with:
                      node-version: '16'  # You can change the Node.js version based on your project
            
                  # Install backend dependencies
                  - name: Install backend dependencies
                    run: |
                      cd api
                      npm install
            
                  # Set up Node.js for frontend
                  - name: Set up Node.js (frontend)
                    uses: actions/setup-node@v3
                    with:
                      node-version: '16'  # You can change the Node.js version based on your project
            
                  # Install frontend dependencies
                  - name: Install frontend dependencies
                    run: |
                      cd webapp
                      npm install

![Screenshot (338)](https://github.com/user-attachments/assets/ca30a940-54c3-4a19-b5b0-f76370a9b496)
![Screenshot (339)](https://github.com/user-attachments/assets/6d73a127-cbb0-48c2-8731-4fd7713790b1)

  - Runs Tests

                name: Test
                      
                      on:
                        push:
                          branches:
                            - main
                        pull_request:
                          branches:
                            - main
                      
                      jobs:
                        backend:
                          runs-on: ubuntu-latest
                          name: Backend CI
                          steps:
                            - name: Checkout Code
                              uses: actions/checkout@v2
                            
                            - name: Set up Node.js for Backend
                              uses: actions/setup-node@v2
                              with:
                                node-version: '14'
                      
                            - name: Install Backend Dependencies
                              run: |
                                cd api
                                npm install
                      
                            - name: Run Backend Tests
                              run: |
                                cd api
                                npm int-test
                      
                        frontend:
                          runs-on: ubuntu-latest
                          name: Frontend CI
                          steps:
                            - name: Checkout Code
                              uses: actions/checkout@v2
                      
                            - name: Set up Node.js for Frontend
                              uses: actions/setup-node@v2
                              with:
                                node-version: '14'
                      
                            - name: Install Frontend Dependencies
                              run: |
                                cd webapp
                                npm install
                      
                            - name: Run Frontend Tests
                              run: |
                                cd webapp
                                npm int-test

      - Builds the application

              name: Build

              on:
                push:
                  branches:
                    - main
                pull_request:
                  branches:
                    - main
              
              jobs:
                backend:
                  runs-on: ubuntu-latest
                  name: Backend Build
                  steps:
                    - name: Checkout Code
                      uses: actions/checkout@v2
                    
                    - name: Set up Node.js for Backend
                      uses: actions/setup-node@v2
                      with:
                        node-version: '14'
              
                    - name: Install Backend Dependencies
                      run: |
                        cd api
                        npm install
              
                    - name: Build Backend Application
                      run: |
                        cd api
                        npm run build
              
                frontend:
                  runs-on: ubuntu-latest
                  name: Frontend Build
                  steps:
                    - name: Checkout Code
                      uses: actions/checkout@v2
              
                    - name: Set up Node.js for Frontend
                      uses: actions/setup-node@v2
                      with:
                        node-version: '14'
              
                    - name: Install Frontend Dependencies
                      run: |
                        cd webapp
                        npm install
              
                    - name: Build Frontend Application
                      run: |
                        cd webapp
                        npm run build

![Screenshot (341)](https://github.com/user-attachments/assets/f2b1e336-ff70-4310-ab3b-9ee7fc84df55)

### <ins>Task 6: Docker Integration</ins>

  - Create Dockerfiles for both the frontend and backend.

      - <ins>Frontend</ins>

            # Step 1: Set up the base image with Node.js
            FROM node:14 AS build
            
            # Step 2: Set the working directory inside the container
            WORKDIR /app
            
            # Step 3: Copy the package.json and package-lock.json (or yarn.lock) to install dependencies first
            COPY package.json package-lock.json ./
            
            # Step 4: Install dependencies
            RUN npm install
            
            # Step 5: Copy the rest of the application code
            COPY . .
            
            # Step 6: Build the React app
            RUN npm run build
            
            # Step 7: Set up the final image for serving the build
            FROM nginx:alpine
            
            # Step 8: Copy the build output from the previous step to NGINX's default public directory
            COPY --from=build /app/build /usr/share/nginx/html
            
            # Step 9: Expose port 80
            EXPOSE 80
            
            # Step 10: Start the NGINX server
            CMD ["nginx", "-g", "daemon off;"]

![Screenshot (343)](https://github.com/user-attachments/assets/be830f92-c44c-4b41-bb95-2e964ff21a87)

  - <ins>Backend</ins>

          # Step 1: Use official Node.js image as base
          FROM node:14
          
          # Step 2: Set the working directory inside the container
          WORKDIR /usr/src/app
          
          # Step 3: Copy the package.json and package-lock.json (or yarn.lock) to install dependencies first
          COPY package.json package-lock.json ./
          
          # Step 4: Install dependencies
          RUN npm install
          
          # Step 5: Copy the rest of the application code into the container
          COPY . .
          
          # Step 6: Expose the port that the application will run on
          EXPOSE 3000
          
          # Step 7: Run the application
          CMD ["npm", "start"]

![Screenshot (342)](https://github.com/user-attachments/assets/e42b343c-59d0-47a3-b60e-7e2d9fb5c239)

  - Modify my GitHub Actions workflows to build Docker images

            name: Build Docker Images for Frontend and Backend
        
        on:
          push:
            branches:
              - main
          pull_request:
            branches:
              - main
        
        jobs:
          build-api:
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@v2
              - name: Build Docker Image
                run: docker build -t api-image ./api
        
          build-webapp:
            runs-on: ubuntu-latest
            steps:
              - uses: actions/checkout@v2
              - name: Build Docker Image
                run: docker build -t webapp-image ./webapp
                
          
![Screenshot (344)](https://github.com/user-attachments/assets/45b1c13e-0099-4217-829a-56d046ece045)

### <ins>Task 7: Deploy to Cloud</ins>

  - Choose a cloud platform for deployment (AWS, Azure or GCP)
       Answer: The preferred cloud platform chosen was Amazon's AWS Platform

  - Configure GitHub Actions to deploy the Docker images to the chosen cloud platform.

        deploy:
                    runs-on: ubuntu-latest
                    name: Deploy to AWS EC2
                    needs: build-api
                    steps:
                      - name: Checkout Code
                        uses: actions/checkout@v2
                
                      - name: Cache Docker layers for frontend
                        uses: actions/cache@v3
                        with:
                          path: ~/.cache/docker
                          key: ${{ runner.os }}-docker-frontend-${{ github.sha }}
                          restore-keys: |
                            ${{ runner.os }}-docker-frontend-
                
                      - name: Cache Docker layers for backend
                        uses: actions/cache@v3
                        with:
                          path: ~/.cache/docker
                          key: ${{ runner.os }}-docker-backend-${{ github.sha }}
                          restore-keys: |
                            ${{ runner.os }}-docker-backend-
                            
                      - name: Set up AWS CLI
                        uses: aws-actions/configure-aws-credentials@v1
                        with:
                          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
                          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
                          aws-region: ${{ secrets.AWS_REGION }}
                
                      - name: SSH into EC2 instance and deploy
                        uses: appleboy/ssh-action@v0.1.5
                        with:
                          host: ${{ secrets.EC2_PUBLIC_IP }}
                          username: ${{ secrets.EC2_USERNAME }}
                          key: ${{ secrets.EC2_SSH_PRIVATE_KEY }}
                          script: |
                            # Stop existing containers
                            docker stop frontend backend || true
                            docker rm frontend backend || true
                
                            # Pull the latest Docker images
                            docker pull ${{ secrets.DOCKER_USERNAME }}/frontend:${{ github.sha }}
                            docker pull ${{ secrets.DOCKER_USERNAME }}/backend:${{ github.sha }}
                
                            # Run the frontend and backend containers
                            docker run -d --name frontend -p 80:80 ${{ secrets.DOCKER_USERNAME }}/frontend:${{ github.sha }}
                            docker run -d --name backend -p 3000:3000 ${{ secrets.DOCKER_USERNAME }}/backend:${{ github.sha }}
                
                            echo "Deployment successful!"

![Screenshot (345)](https://github.com/user-attachments/assets/82ef0969-491d-49eb-bd32-c9bcbcd74de9)
![Screenshot (346)](https://github.com/user-attachments/assets/b2c21d1c-617a-4bac-a22b-3d4ee154d8c8)

  - Use GitHub Secrets to securely store and access cloud credentials
      Answer: Within the code, To access the Instance's Host name, Username and key, they will be stored in the secrets file of the application.

### <ins>Task 8: Continuous Deployment</ins>

  - Configure my workflows to deploy updates automatically to the cloud environmentwhen changes are pushed to the main branch.

            name: Auto Deploy to AWS EC2 on Push to Main
            
            on:
              push:
                branches:
                  - main
            
            jobs:
              build-and-push:
                runs-on: ubuntu-latest
                name: Build Docker Images and Push to Docker Hub
                steps:
                  - name: Checkout Code
                    uses: actions/checkout@v2
            
                  - name: Set up Docker Buildx
                    uses: docker/setup-buildx-action@v2
            
                  - name: Build Docker image for frontend
                    run: |
                      docker build -f frontend/Dockerfile -t ${{ secrets.DOCKER_USERNAME }}/frontend:${{ github.sha }} .
                  
                  - name: Build Docker image for backend
                    run: |
                      docker build -f backend/Dockerfile -t ${{ secrets.DOCKER_USERNAME }}/backend:${{ github.sha }} .
            
                  - name: Log in to Docker Hub
                    uses: docker/login-action@v2
                    with:
                      username: ${{ secrets.DOCKER_USERNAME }}
                      password: ${{ secrets.DOCKER_PASSWORD }}
            
                  - name: Push Docker image for frontend
                    run: |
                      docker push ${{ secrets.DOCKER_USERNAME }}/frontend:${{ github.sha }}
                  
                  - name: Push Docker image for backend
                    run: |
                      docker push ${{ secrets.DOCKER_USERNAME }}/backend:${{ github.sha }}
            
              deploy:
                runs-on: ubuntu-latest
                name: Deploy to AWS EC2
                needs: build-and-push
                steps:
                  - name: Set up AWS CLI
                    uses: aws-actions/configure-aws-credentials@v1
                    with:
                      aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
                      aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
                      aws-region: ${{ secrets.AWS_REGION }}
            
                  - name: SSH into EC2 instance and deploy
                    uses: appleboy/ssh-action@v0.1.5
                    with:
                      host: ${{ secrets.EC2_PUBLIC_IP }}
                      username: ${{ secrets.EC2_USERNAME }}
                      key: ${{ secrets.EC2_SSH_PRIVATE_KEY }}
                      script: |
                        # Stop existing containers
                        docker stop frontend backend || true
                        docker rm frontend backend || true
            
                        # Pull the latest Docker images from Docker Hub
                        docker pull ${{ secrets.DOCKER_USERNAME }}/frontend:${{ github.sha }}
                        docker pull ${{ secrets.DOCKER_USERNAME }}/backend:${{ github.sha }}
            
                        # Run the frontend container (make sure to expose the correct ports)
                        docker run -d --name frontend -p 80:80 ${{ secrets.DOCKER_USERNAME }}/frontend:${{ github.sha }}
            
                        # Run the backend container (make sure to expose the correct ports)
                        docker run -d --name backend -p 3000:3000 ${{ secrets.DOCKER_USERNAME }}/backend:${{ github.sha }}
            
                        echo "Deployment successful!"

![Screenshot (347)](https://github.com/user-attachments/assets/7e78766b-07fc-4cdb-9661-e8a8123e6ec5)
![Screenshot (348)](https://github.com/user-attachments/assets/d0e6c171-9cb0-4141-aaf7-2bd6de6aa5a4)
![Screenshot (349)](https://github.com/user-attachments/assets/daa693a4-fe04-4fb8-b2d6-2f5e3aad959e)

### <ins>Task 9: Performance and Security</ins>

  - Implement caching in your workflows to optimize build times.

                      - name: Cache Docker layers for frontend
                                        uses: actions/cache@v3
                                        with:
                                          path: ~/.cache/docker
                                          key: ${{ runner.os }}-docker-frontend-${{ github.sha }}
                                          restore-keys: |
                                            ${{ runner.os }}-docker-frontend-
                
                      - name: Cache Docker layers for backend
                        uses: actions/cache@v3
                        with:
                          path: ~/.cache/docker
                          key: ${{ runner.os }}-docker-backend-${{ github.sha }}
                          restore-keys: |
                            ${{ runner.os }}-docker-backend-

![Screenshot (350)](https://github.com/user-attachments/assets/f1cd740d-b2c3-47fd-a1ee-3d3fd2376a48)

### <ins>Task 10: Project Documentation</ins>

  - Document my project setup, workflow details and instructions for local development in a **README.md** file.

**END**


