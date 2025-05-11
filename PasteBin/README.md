# 📋 PasteBin Service

The **PasteBin Service** is a lightweight text storage microservice within the **UniversalApp** ecosystem. It allows users to create, retrieve, and manage pastes (text snippets), optionally with expiration settings and visibility control (public/private).

---

## 📸 Screenshots

> _Add UI screenshots from UniversalAppUI showing paste creation, paste viewing, and list display._

---

## 🚀 Features

- 📝 Create and retrieve text pastes
- ⏳ Support for expiration (1 hour, 1 day, 1 week, never)
- 🔒 Public and private visibility
- ⚡ Redis caching for fast reads
- ☁️ Paste content stored in **MinIO** (S3-compatible)
- 📑 Metadata stored in **PostgreSQL**
- 🔐 Authenticated via JWT (proxied via AcceptorService)

---

## ⚙️ Tech Stack

| Component         | Technology                   |
|------------------|------------------------------|
| Backend           | Java, Spring Boot            |
| Cache             | Redis                        |
| Object Storage    | MinIO                        |
| Metadata Store    | PostgreSQL                   |
| Auth              | JWT via AcceptorService      |
| Deployment        | Docker, AWS EC2              |

---

## 📁 Project Structure

```bash
PasteBin/
├── src/
│   ├── main/
│   │   ├── java/com/universal/pastebin/
│   │   │   ├── controller/         # Paste APIs
│   │   │   ├── model/              # Paste metadata models
│   │   │   ├── service/            # Logic to handle cache/storage
│   │   │   └── PasteBinApp.java
│   └── resources/
│       └── application.yml
├── .env
├── Dockerfile
└── README.md
````

---

## 🌐 API Overview

### POST `/api/pastes`

Create a new paste.

**Request:**

```json
{
  "title": "Sample",
  "content": "This is a test paste.",
  "visibility": "PUBLIC",
  "expiresIn": "1_DAY"
}
```
```

**Response:**

```json
{
  "id": "abc123",
  "shortUrl": "https://app.com/p/abc123"
}
```

---

### GET `/api/pastes/{id}`

Retrieve a paste by ID.

---

### GET `/api/pastes/user`

List all pastes created by the current authenticated user.

> Requires `Authorization: Bearer <JWT>` header.

---

## 🧪 Running Locally

```bash
git clone https://github.com/praveenkumarsh/PasteBin.git
cd PasteBin
./mvnw clean install
docker build -t pastebin-service .
docker run -d -p 8082:8082 --env-file .env pastebin-service
```

> Requires Redis, MinIO, and PostgreSQL containers or services running.

---

## 🧪 Testing

```bash
./mvnw test
```

---

## 🔐 Security

* Paste visibility: `PUBLIC` or `PRIVATE`
* Paste access only allowed if:

  * Public
  * Or matches JWT user ID
* JWT validated via `AcceptorService` proxy

---

## 🔧 Environment Variables (`.env`)

```env
REDIS_HOST=localhost
REDIS_PORT=6379
MINIO_ENDPOINT=http://localhost:9000
MINIO_BUCKET=pastebin
MINIO_ACCESS_KEY=minioadmin
MINIO_SECRET_KEY=minioadmin
POSTGRES_URL=jdbc:postgresql://localhost:5432/pastebin
POSTGRES_USER=postgres
POSTGRES_PASSWORD=password
```

---

## 📄 API Documentation

Swagger is available at:

```
http://<ec2-ip>:8082/swagger-ui/index.html
```

---

## 🔄 Integration

* Used by [UniversalAppUI](../UniversalAppUI/README.md) for UI
* Authentication handled by [AcceptorService](../AcceptorService/README.md)

---

## 📜 License

Licensed under the [MIT License](../LICENSE).