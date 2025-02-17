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

  



