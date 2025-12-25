FROM node:20-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm install
RUN npm install -g @angular/cli

COPY . .
RUN npm run build

# Nginx image for serving the app
FROM nginx:alpine

# Copy Angular build output
COPY --from=build /app/dist/event-planner-frontend/browser /usr/share/nginx/html

# Copy custom nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 80

# Run nginx in foreground (required for OpenShift)
CMD ["nginx", "-g", "daemon off;"]

