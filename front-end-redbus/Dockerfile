# Stage 1: Build React app
FROM node:18 AS build
WORKDIR /app

# Copy package.json and package-lock.json first for caching
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the project files
COPY . .

# If your build requires env vars, you can set them like this:
# ARG REACT_APP_API_URL
# ENV REACT_APP_API_URL=$REACT_APP_API_URL

# Build the app
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:1.25-alpine
# Copy built files from previous stage
COPY --from=build /app/build /usr/share/nginx/html
# Expose port 80 for HTTP traffic
EXPOSE 80
# Start Nginx server
CMD ["nginx", "-g", "daemon off;"]
