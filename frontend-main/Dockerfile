FROM node:20-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm install
RUN npm install -g @angular/cli

COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist/event-planner-frontend/browser /usr/share/nginx/html
EXPOSE 80
FROM node:20-alpine AS build

WORKDIR /app
COPY package*.json ./
RUN npm install
RUN npm install -g @angular/cli

COPY . .
RUN npm run build

FROM nginx:alpine
COPY --from=build /app/dist/event-planner-frontend/browser /usr/share/nginx/html
EXPOSE 80

