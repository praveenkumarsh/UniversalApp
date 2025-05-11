# 🌐 Universal App

A scalable, web-based modular platform composed of multiple Spring Boot microservices and a modern React frontend. Deployed on AWS EC2, fully containerized with Docker, and backed by robust cloud-native tools like Redis, MinIO, PostgreSQL, and Cassandra, AWS services like EC2, ECS, DynamoDB, etc.

## 📚 Readmes for Individual Services

- [UniversalApp UI](./UniversalAppUI/README.md)
- [Acceptor Service](./AcceptorService/README.md)
- [Chat App](./ChatApp/README.md)
- [ShortUrl](./ShortUrl/README.md)
- [PasteBin](./PasteBin/README.md)
- [File Manager](./FileManager/README.md)
- [Code Compiler](./OnlineCompiler/README.md)

## 🧩 Architecture Overview

Universal App is structured as a suite of independent services, each maintained in its own repository:

| Service             | Description                                      |
|---------------------|--------------------------------------------------|
| **Frontend**         | React + Vite SPA (Single Page Application)       |
| **AcceptorService**  | API Gateway, JWT Auth, OAuth, Proxy Layer        |
| **ChatAppService**   | 1:1 real-time chat using WebSockets & Redis      |
| **PasteBin**         | Paste storage with Redis caching + MinIO backend |
| **ShortURL**         | URL shortener with metadata and click tracking  |
| **FileManager**      | File storage and management with MinIO, Postgres          |
| **CodeCompiler**     | Secure code execution (Java, Python, C++) via Docker |

> All backend services are developed using **Java (Spring Boot)** and exposed through RESTful APIs and Frontend is based on React Vite. All services private APIs are secure using JWT Token.

## ⚙️ Infrastructure Stack

| Component        | Technology                       |
|------------------|----------------------------------|
| **Frontend**     | React, Vite, Tailwind CSS         |
| **Backend**      | Spring Boot, Spring Security, Google Auth      |
| **Database**     | PostgreSQL, Cassandra, DynamoDB             |
| **Cache**        | Redis                             |
| **Object Storage** | MinIO (S3-compatible)             |
| **Code Execution**| Docker-based per-language containers |
| **Deployment**   | Docker, EC2 (AWS)                 |

## 🚀 Deployment Overview

Each service is deployed on **EC2 instances** using Docker containers. Services can be orchestrated individually or via Docker Compose.

## Source Code

- [Frontend](https://github.com/praveenkumarsh/UniversalAppUI)
- [Acceptor](https://github.com/praveenkumarsh/UniversalAppBackend)
- [File Manager](https://github.com/praveenkumarsh/FileManagerBackend)
- [PasteBin](https://github.com/praveenkumarsh/PasteBin)
- [ShortUrl](https://github.com/praveenkumarsh/ShortUrl)
- [Chat App](https://github.com/praveenkumarsh/ChatAppBackend)
- [Online Compiler](https://github.com/praveenkumarsh/OnlineCompilerBackend)

### Example Deployment (ChatAppService)

```bash
git clone https://github.com/praveenkumarsh/ChatAppBackend.git
cd ChatAppService
./mvnw clean install
docker build -t chatapp-service .
docker run -d -p 8081:8081 --env-file .env chatapp-service
```

> Each service includes its own `.env` file for configuration.

## 🌐 Running Frontend (Locally)

```bash
git clone https://github.com/praveenkumarsh/UniversalAppUI.git
cd universal-frontend
npm install
npm run dev
```

> Update `.env` in `universal-frontend` with API base URLs exposed from EC2 or localhost (via Docker).

## 🔒 Authentication & Routing

- **JWT-based Authentication** handled by `AcceptorService`
- **Google OAuth** login supported
- **All client-facing routes** are funneled through `AcceptorService`, which proxies authorized requests to internal services

## 📄 API Documentation

Each service has its own OpenAPI/Swagger docs:

```text
http://<ec2-ip>:<port>/swagger-ui/index.html
```

### Example:

```text
http://ec2-xx-xx-xx-xx.compute.amazonaws.com:8081/swagger-ui/index.html  # ChatAppService
```

## 🧪 Testing

### Backend

```bash
./mvnw test
```

### Frontend

```bash
npm run test
```

## 📁 Project Directory Layout

Each service lives in its own GitHub repository:

```
universal-frontend/         # React + Vite SPA
acceptor-service/           # Auth gateway and proxy
chatapp-service/            # WebSocket-based chat
pastebin-service/           # Paste management
shorturl-service/           # URL shortening
file-manager-service/       # File upload/download
code-compiler-service/      # Docker-based code executor
```

## ✅ Feature Summary

- ✅ Web-only support via React
- ✅ Authentication (JWT, Google OAuth)
- ✅ Realtime WebSocket chat
- ✅ PasteBin with Redis & MinIO
- ✅ ShortURL with analytics
- ✅ FileManager with cloud storage
- ✅ Secure code execution (Java, Python, C++)
- ✅ EC2 + Docker-based deployment
- ✅ Redis, PostgreSQL, Cassandra, MinIO integration

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

> 📌 **Note:** Each microservice repository contains its own `README.md` with service-specific instructions, environment variables, and API details.
