# Stage 1: Build the React application
FROM node:18-alpine AS build

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json (or yarn.lock)
COPY package*.json ./
# If using yarn, uncomment the next line and comment out the npm ci line
# COPY yarn.lock ./

# Install dependencies
# If using yarn, use 'yarn install --frozen-lockfile'
RUN npm ci

# Copy the rest of the application code
COPY . .

# Build the application
# If using yarn, use 'yarn build'
RUN npm run build

# Stage 2: Serve the application with Nginx
FROM nginx:1.25-alpine

# Copy the build output from the build stage to Nginx's html directory
COPY --from=build /app/build /usr/share/nginx/html

# (Optional) Copy a custom Nginx configuration if needed
# COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80 for Nginx
EXPOSE 80

# Start Nginx when the container launches
CMD ["nginx", "-g", "daemon off;"]
