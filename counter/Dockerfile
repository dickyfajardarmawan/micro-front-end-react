FROM node:14 as builder
# Set the working directory to /app inside the container
WORKDIR /src
# Copy app files
COPY package.json ./
COPY . .
RUN npm cache verify
RUN npm install
# Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)
# Build the app
RUN npm run build

FROM nginx:1.19

COPY nginx.conf /etc/nginx/conf.d/default.conf

COPY --from=builder ./src/dist /usr/share/nginx/html

# Bundle static assets with nginx
# FROM nginx:1.21.0-alpine as production
# ENV NODE_ENV production
# Copy built assets from `builder` image
# COPY /dist /usr/share/nginx/html
# Add your nginx.conf
# COPY nginx.conf /etc/nginx/conf.d/default.conf
# Expose port
# EXPOSE 3002
# Start nginx
# CMD ["nginx", "-g", "daemon off;"]