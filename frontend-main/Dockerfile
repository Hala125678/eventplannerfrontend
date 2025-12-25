# Stage 1: Build Angular app
FROM node:20-alpine AS build

# Set working directory
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Install Angular CLI globally
RUN npm install -g @angular/cli

# Copy all source files
COPY . .

# Build Angular app in production mode
RUN npm run build -- --output-path=dist

# Stage 2: Serve with Nginx
FROM nginx:alpine

# Copy built Angular files to Nginx html folder
COPY --from=build /app/dist /usr/share/nginx/html

# Copy nginx.conf if it exists; use default if not
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
