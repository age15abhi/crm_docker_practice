# -----------------------
# Stage 1: Builder
# -----------------------
FROM node:21-alpine AS builder

# set working directory
WORKDIR /app

# copy the package files
COPY package*.json ./
# install dependencies
RUN npm install

# copy all source code
COPY . .
# build the app
RUN npm run build
# -----------------------
# Stage 2: Production
# -----------------------
FROM nginx:alpine AS production

# Remove default NGINX website
RUN rm -rf /usr/share/nginx/html/*

# copy the build to the nginx html folder
COPY --from=builder /app/dist /usr/share/nginx/html


# Expose port 80 for HTTP
EXPOSE 80

# Optional: copy custom nginx config (if you have one)
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Start NGINX server
# this will keep running in the foreground
CMD ["nginx", "-g", "daemon off;"]