# 🔗 URL Shortener API

A production-ready URL Shortener built with **Spring Boot**, **Redis**, and **MySQL**, featuring **custom aliases**, **click analytics**, **rate limiting**, and **Docker support**.

> Generate short, shareable URLs with high performance and protection against abuse.

---

## 🚀 Features

* ✅ Shorten long URLs
* ✅ Custom short aliases
* ✅ Automatic redirect to original URL
* ✅ Click tracking & analytics
* ✅ URL expiration support
* ✅ Rate limiting using Redis
* ✅ Dockerized application
* ✅ RESTful APIs
* ✅ MySQL database
* ✅ Production-ready configuration

---

## 🛠️ Tech Stack

| Technology      | Purpose                 |
| --------------- | ----------------------- |
| Java 17         | Backend                 |
| Spring Boot     | REST API                |
| Spring Data JPA | Database access         |
| MySQL           | Persistent storage      |
| Redis           | Rate limiting & caching |
| Bucket4j        | API rate limiting       |
| Maven           | Dependency management   |
| Docker          | Containerization        |

---

# 📁 Project Structure

```
src
 ├── controller
 ├── service
 ├── repository
 ├── entity
 ├── dto
 ├── config
 ├── rateLimiter
 ├── exception
 └── UrlShortenerApplication
```

---

# ⚡ API Endpoints

## Create Short URL

```
POST /api/urls
```

Request

```json
{
    "originalUrl":"https://www.google.com",
    "customAlias":"google"
}
```

Response

```json
{
    "shortUrl":"http://localhost:8080/google"
}
```

---

## Redirect

```
GET /{shortCode}
```

Redirects the user to the original URL.

---

## Get Analytics

```
GET /api/urls/{shortCode}/analytics
```

Example Response

```json
{
    "originalUrl":"https://www.google.com",
    "clickCount":25,
    "createdAt":"2026-06-28T10:00:00",
    "expiresAt":"2026-07-28T10:00:00"
}
```

---

# 🛡️ Rate Limiting

This project uses:

* Redis
* Bucket4j
* Spring MVC Interceptor

Each client IP is allowed a limited number of requests within a configurable time window.

If the limit is exceeded:

```
HTTP 429 Too Many Requests
```

---

# ⚙️ Running Locally

## Clone Repository

```bash
git clone https://github.com/Kartik-exe/url-shortener.git
cd url-shortener
```

---

## Configure Database

Update:

```
application.properties
```

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/url_shortener
spring.datasource.username=root
spring.datasource.password=your_password
```

---

## Configure Redis

```properties
spring.data.redis.host=localhost
spring.data.redis.port=6379
```

Or use your Upstash credentials.

---

## Build

```bash
mvn clean install
```

---

## Run

```bash
mvn spring-boot:run
```

Application starts on

```
http://localhost:8080
```

---

# 🐳 Docker

Build image

```bash
docker build -t url-shortener .
```

Run container

```bash
docker run -p 8080:8080 url-shortener
```

---

# 📊 Future Improvements

* User Authentication (JWT)
* QR Code Generation
* Password Protected URLs
* Custom Domains
* Admin Dashboard
* Swagger/OpenAPI Documentation
* URL Deletion
* Detailed Analytics
* Kafka-based Click Tracking

---

# 📷 Sample Flow

```
Long URL
      │
      ▼
POST /api/urls
      │
      ▼
Generate Short Code
      │
      ▼
Store in MySQL
      │
      ▼
Return Short URL
      │
      ▼
GET /abc123
      │
      ▼
Lookup Original URL
      │
      ▼
Increment Click Count
      │
      ▼
Redirect (302)
```

---

# 👨‍💻 Author

**Kartik Nigam**
