# Build step
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . ./
ARG VITE_API_URL  # Define the build argument
ENV VITE_API_URL=$VITE_API_URL
RUN npm run build

# Serve with nginx
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
