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
