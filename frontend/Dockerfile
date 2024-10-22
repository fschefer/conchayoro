# Build Stage
FROM node:18-alpine as build-stage
WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy rest of the application files and build
COPY . .
RUN npm run build

# Production Stage
FROM nginx:1.19.3-alpine as production-stage

# Copy built application to nginx html folder
COPY --from=build-stage /app/.next/server/app /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start nginx in the foreground
CMD ["nginx", "-g", "daemon off;"]
