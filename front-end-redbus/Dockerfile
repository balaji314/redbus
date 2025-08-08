# Stage 1: Build React app
FROM node:16 AS build
WORKDIR /app

# Copy dependency files and install
COPY package*.json ./
RUN npm install --legacy-peer-deps

# Copy rest of the source code
COPY . .

# Build the app
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:1.25-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
