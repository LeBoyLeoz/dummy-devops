# Multi-stage build for production
FROM node:25-alpine AS builder

WORKDIR /app

# Build argument for API URL
ARG API_URL=http://localhost:3000

COPY package.json .

RUN npm install

COPY . .

# Pass API URL as environment variable for build
ENV VITE_API_URL=${API_URL}

RUN npm run build

# Production stage with nginx
FROM nginx:alpine

COPY --from=builder /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]