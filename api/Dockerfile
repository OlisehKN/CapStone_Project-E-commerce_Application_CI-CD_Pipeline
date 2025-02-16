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
