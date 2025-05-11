# 🛡️ AcceptorService

The **AcceptorService** is the central gateway and authentication service for the UniversalApp platform. It handles all authentication (JWT and Google OAuth), user management, and proxies authorized API and WebSocket requests to other internal microservices.

---

## 📸 Screenshots

<!-- Add system architecture image here -->
![System Architecture](screenshots/architecture.png)

<!-- Add screenshot of Swagger UI here -->
![Swagger UI](screenshots/swagger.png)

<!-- Add screenshot of Login flow or API usage here -->
![Login Flow](screenshots/login.png)

---

## 🚀 Features

- ✅ Acts as API gateway for UniversalApp
- ✅ JWT Authentication
- ✅ Google OAuth 2.0 (Authorization Code Flow)
- ✅ User Registration & Login (via OpenAPI spec)
- ✅ Role-based route authorization
- ✅ WebSocket handshake validation and proxying
- ✅ Secure reverse proxy for all backend services

---

## 🏗️ Architecture

```text
  [ React Frontend ] 
         |
         v
  [ AcceptorService (Gateway) ]
         |
   -----------------------------
   |       |       |     |     |
   v       v       v     v     v
[Chat]  [Paste] [Short] [File] [Compiler]
```

- Every HTTP/WebSocket request goes through AcceptorService
- Validates JWT token or handles Google OAuth exchange
- Forwards request to appropriate downstream service after attaching user context

---

## ⚙️ Tech Stack

| Layer         | Technology               |
|---------------|---------------------------|
| Framework     | Spring Boot 3.2+         |
| Auth          | JWT + Spring Security    |
| OAuth         | Google Identity          |
| API Docs      | OpenAPI 3.1 (contract-first) |
| Reverse Proxy | Spring Cloud Gateway (custom impl) |
| Deployment    | Docker, AWS EC2          |

---

## 📦 Modules

| Module        | Description                                   |
|---------------|-----------------------------------------------|
| `UserService` | Handles user registration/login/token         |
| `GoogleAuth`  | Google OAuth 2.0 integration                  |
| `ProxyFilter` | Proxies requests after JWT validation         |
| `WebSocketAuth` | Validates WebSocket handshakes with JWT    |

---

## 📄 OpenAPI Spec

- Fully contract-based development using OpenAPI 3.1
- Validates request/response using `springdoc-openapi`
- Jakarta Validation support enabled

📘 Swagger UI:
```
http://localhost:8080/swagger-ui/index.html
```

🗂️ OpenAPI Spec Path:
```
src/main/resources/openapi/acceptor.yaml
```

---

## 🧪 Running Locally

### Prerequisites

- Java 17+
- Maven
- Docker (for Redis if needed)

### Steps

```bash
git clone https://github.com/praveenkumarsh/UniversalAppBackend.git
cd UniversalAppBackend
./mvnw clean install
docker build -t acceptor-service .
docker run -p 8080:8080 --env-file .env acceptor-service
```

Configure `.env` with environment variables:
```env
JWT_SECRET=your_jwt_secret
GOOGLE_CLIENT_ID=your_client_id
GOOGLE_CLIENT_SECRET=your_client_secret
FRONTEND_URL=http://localhost:5173
```

---

## 🧪 API Examples

### Register User

```http
POST /api/auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "strongpass123"
}
```

### Login User

```http
POST /api/auth/login
```

### Google OAuth (Authorization Code Exchange)

```http
GET /oauth2/callback?code=xyz123
```

---

## 🔐 Security

- JWT tokens are signed and validated per request
- Stateless authentication
- CORS properly configured for frontend URL
- CSRF disabled for REST APIs

---

## 🧼 Code Quality

- Modular structure
- Layered architecture
- Integration tested with `@SpringBootTest`
- OpenAPI contract validation + runtime request validation

---

## 📜 License

This project is part of [UniversalApp](https://github.com/praveenkumarsh/UniversalAppUI) and is licensed under the MIT License.

---
