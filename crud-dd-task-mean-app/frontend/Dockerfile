# Stage 1: Build Angular app
FROM node:18-alpine AS build

WORKDIR /app

COPY . .

RUN npm install
RUN npm run build

# Stage 2: Serve with nginx
FROM nginx:alpine AS production

# Remove default nginx assets
#RUN rm -rf /usr/share/nginx/html/*

# Copy Angular build
COPY --from=build /app/dist/angular-15-crud /usr/share/nginx/html

# Copy custom nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
