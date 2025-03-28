FROM public.ecr.aws/docker/library/node:18-alpine AS build
WORKDIR /app

# Copy only package.json and package-lock.json first to leverage Docker caching
COPY package.json package-lock.json ./
RUN npm install

# Copy the rest of the application files
COPY . .

# Ensure correct permissions
RUN chmod +x node_modules/.bin/react-scripts

# Build the frontend application
RUN npm run build

# Use Nginx to serve the React app
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
CMD ["nginx", "-g", "daemon off;"]

