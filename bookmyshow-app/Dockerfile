# Step 1 — Build React App
FROM node:18-alpine AS build

WORKDIR /app

# Copy package.json files
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Copy full project
COPY . .

# Build production code
RUN npm run build


# Step 2 — Serve using NGINX (Production)
FROM nginx:stable-alpine

# Copy build output to NGINX HTML folder
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 for Kubernetes
EXPOSE 80

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]
