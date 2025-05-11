# 🔗 ShortURL Service

The **ShortURL Service** is a high-performance URL shortening microservice within the **UniversalApp** ecosystem. It provides short, unique aliases for long URLs with redirection support, tracking, and custom alias capabilities.

---

## 📸 Screenshots

> _🖼 Add screenshots from the UI showing URL shortening form, result view, and My URLs list._

---

## 🚀 Features

- 🔗 Generate short URLs from long links
- 🧑‍💼 Authenticated users get a personalized "My URLs" list
- 📊 Track click count, expiration, and creation time
- 🆔 Custom alias support (optional)
- 💨 Fast redirect via Redis caching
- 🧠 Metadata persistence in PostgreSQL or Cassandra
- 🛡 Secured using JWT auth, proxied by AcceptorService

---

## ⚙️ Tech Stack

| Component          | Technology                      |
|-------------------|----------------------------------|
| Backend            | Java, Spring Boot               |
| Cache              | Redis                           |
| Primary Database   | PostgreSQL / Cassandra (configurable) |
| Authentication     | JWT (via AcceptorService)       |
| Deployment         | Docker, AWS EC2                 |

---

## 📁 Project Structure

```bash
ShortUrl/
├── src/
│   ├── main/java/com/universal/shorturl/
│   │   ├── controller/       # URL APIs
│   │   ├── model/            # URL metadata
│   │   ├── service/          # Core logic
│   │   └── ShortUrlApp.java
│   └── resources/
│       └── application.yml
├── .env
├── Dockerfile
└── README.md
````

---

## 🌐 API Overview

### POST `/api/shorten`

Shorten a new URL.

**Request:**

```json
{
  "originalUrl": "https://example.com/article?id=123",
  "customAlias": "article123",  // Optional
  "expireInDays": 7             // Optional
}
```
```

**Response:**

```json
{
  "shortUrl": "https://app.com/s/article123"
}
```

---

### GET `/s/{alias}`

Redirect to original URL. Tracked with click count.

---

### GET `/api/urls/user`

List all short URLs created by the authenticated user.

---

## 🧪 Running Locally

```bash
git clone https://github.com/praveenkumarsh/ShortUrl.git
cd ShortUrl
./mvnw clean install
docker build -t shorturl-service .
docker run -d -p 8083:8083 --env-file .env shorturl-service
```

---

## ⚙️ `.env` Configuration

```env
REDIS_HOST=localhost
REDIS_PORT=6379

DB_TYPE=postgres  # or cassandra
POSTGRES_URL=jdbc:postgresql://localhost:5432/shorturl
POSTGRES_USER=postgres
POSTGRES_PASSWORD=secret

CASSANDRA_CONTACT_POINTS=localhost
CASSANDRA_KEYSPACE=shorturl
```

---

## 🔐 Security

* All APIs require JWT-based authentication (handled by `AcceptorService`)
* Redirect (`/s/{alias}`) is publicly accessible

---

## 📄 API Documentation

Swagger UI:

```
http://<ec2-ip>:8083/swagger-ui/index.html
```

---

## 🔄 Integration

* UI integration: [UniversalAppUI](../UniversalAppUI/README.md)
* Auth & routing: [AcceptorService](../AcceptorService/README.md)

---

## 📜 License

Licensed under the [MIT License](../LICENSE).