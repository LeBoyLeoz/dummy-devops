# dummy devops

The goal of this project is to showcase the ecosystem of a web application using modern tooling.

## dev

### backend

```
cd backend
npm i
docker compose up -d
npm run init-db
npm run dev
```

### frontend

```
cd frontend
npm i
npm run dev
```

## prod

### Build Docker Images

#### Backend

```bash
docker build -t dummy-backend:latest ./backend
```

#### Frontend

```bash
# With default API URL (http://localhost:3000)
docker build -t dummy-frontend:latest ./frontend

# Or with custom API URL (e.g., http://api.example.com)
docker build --build-arg API_URL=http://api.example.com -t dummy-frontend:latest ./frontend
```

### Run Individual Containers

#### Backend

```bash
docker run -d \
  --name dummy-backend \
  -e ELASTICSEARCH_URL=http://dummy-elasticsearch:9200 \
  -p 3000:3000 \
  --network dummy-network \
  dummy-backend:latest
```

#### Frontend

```bash
docker run -d \
  --name dummy-frontend \
  -p 8080:80 \
  --network dummy-network \
  dummy-frontend:latest
```

### View Application

- Frontend: http://localhost:8080
- Backend API: http://localhost:3000
- Health check: http://localhost:3000/health
