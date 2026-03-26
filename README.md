# LUXE — Java Full Stack E-Commerce Platform

A production-ready, full-stack ecommerce application built with **Spring Boot** (backend) and **Vanilla JS / HTML5** (frontend), featuring a premium editorial UI design.

---

## 🏗️ Architecture

```
ecommerce/
├── backend/                  # Spring Boot REST API
│   ├── pom.xml               # Maven dependencies
│   └── src/main/
│       ├── java/com/shop/
│       │   ├── ShopApplication.java        # Entry point
│       │   ├── model/                      # JPA Entities
│       │   │   ├── Product.java
│       │   │   ├── User.java
│       │   │   ├── Order.java
│       │   │   └── OrderItem.java
│       │   ├── repository/                 # Spring Data JPA
│       │   │   ├── ProductRepository.java
│       │   │   ├── UserRepository.java
│       │   │   └── OrderRepository.java
│       │   ├── service/                    # Business Logic
│       │   │   ├── ProductService.java
│       │   │   ├── UserService.java
│       │   │   └── OrderService.java
│       │   ├── controller/                 # REST Endpoints
│       │   │   ├── ProductController.java
│       │   │   ├── AuthController.java
│       │   │   └── OrderController.java
│       │   ├── dto/
│       │   │   └── OrderRequest.java
│       │   └── config/
│       │       ├── SecurityConfig.java     # Spring Security
│       │       └── DataInitializer.java    # Seed data
│       └── resources/
│           └── application.properties
│
└── frontend/
    └── index.html             # Complete SPA frontend
```

---

## 🚀 Tech Stack

| Layer       | Technology               |
|-------------|--------------------------|
| Backend     | Spring Boot 3.2, Java 17 |
| ORM         | Spring Data JPA / Hibernate |
| Database    | H2 (dev) / MySQL (prod)  |
| Security    | Spring Security + BCrypt |
| Auth        | JWT-ready structure      |
| Frontend    | Vanilla JS ES6+ SPA      |
| Fonts       | Cormorant Garamond + DM Sans |
| Styling     | Pure CSS (no framework)  |
| Build       | Maven                    |

---

## 🔌 REST API Endpoints

### Products
| Method | Endpoint                        | Description              |
|--------|---------------------------------|--------------------------|
| GET    | `/api/products`                 | Paginated product list   |
| GET    | `/api/products/{id}`            | Single product           |
| GET    | `/api/products/search`          | Search + filter          |
| GET    | `/api/products/featured`        | Featured products        |
| GET    | `/api/products/categories`      | All categories           |
| GET    | `/api/products/brands`          | All brands               |
| POST   | `/api/products`                 | Create product (admin)   |
| PUT    | `/api/products/{id}`            | Update product (admin)   |
| DELETE | `/api/products/{id}`            | Delete product (admin)   |

### Auth
| Method | Endpoint              | Description       |
|--------|-----------------------|-------------------|
| POST   | `/api/auth/register`  | Register user     |
| POST   | `/api/auth/login`     | Login + token     |

### Orders
| Method | Endpoint                      | Description         |
|--------|-------------------------------|---------------------|
| POST   | `/api/orders/user/{userId}`   | Create order        |
| GET    | `/api/orders/user/{userId}`   | User's orders       |
| GET    | `/api/orders/{orderId}`       | Order details       |
| PATCH  | `/api/orders/{orderId}/status`| Update status       |

---

## ⚙️ Running the Backend

### Prerequisites
- Java 17+
- Maven 3.8+

### Start the server
```bash
cd backend
mvn spring-boot:run
```

The API will be live at: **http://localhost:8080**

H2 console (dev): http://localhost:8080/h2-console
- JDBC URL: `jdbc:h2:mem:shopdb`
- Username: `sa` | Password: *(blank)*

---

## 🌐 Running the Frontend

Simply open `frontend/index.html` in any modern browser.

**How it works:**
- The frontend tries to connect to `http://localhost:8080/api`
- If the backend is offline, it gracefully falls back to **16 rich mock products**
- All features (cart, wishlist, auth, filtering, search) work in both modes

---

## 🗃️ Switch to MySQL (Production)

1. Update `application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/shopdb
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.jpa.database-platform=org.hibernate.dialect.MySQLDialect
spring.jpa.hibernate.ddl-auto=update
spring.h2.console.enabled=false
```

2. Create the MySQL database:
```sql
CREATE DATABASE shopdb CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

---

## 🔑 Key Features

### Backend
- **RESTful API** with full CRUD for products, users, orders
- **Spring Security** with BCrypt password hashing
- **JPA Entities** with relationships (OneToMany, ManyToOne)
- **Custom JPQL queries** for search and filtering
- **Data seeding** with 17 realistic products on startup
- **CORS configured** for frontend access
- **Pagination & sorting** on all list endpoints
- **Input validation** and error handling

### Frontend
- **Single Page Application** — no page reloads
- **Responsive design** — mobile, tablet, desktop
- **Product catalog** with grid, search, filter, sort
- **Category browsing** with visual cards
- **Product detail** page with quantity selector
- **Cart drawer** — add, remove, update quantities
- **Wishlist** — save favorite products
- **Auth modal** — login + register with tab switching
- **User profile** — orders, wishlist, account details
- **Toast notifications** for user feedback
- **Loading screen** on first visit
- **Sticky header** with scroll effect
- **Graceful API fallback** to mock data

---

## 🎨 Design System

- **Color Palette**: Deep ink (#0d0d0d) · Warm paper (#faf9f7) · Aged gold (#b8924a)
- **Typography**: Cormorant Garamond (display) + DM Sans (body) + DM Mono (prices)
- **Style**: Editorial luxury — refined minimalism with warm tones
- **Animations**: CSS-only page transitions, hover effects, cart/modal slides

---

## 🛡️ Security Notes

For production deployment, add:
1. **JWT filter** in `SecurityConfig` for token validation
2. **Rate limiting** on auth endpoints
3. **HTTPS** only
4. **Environment variables** for secrets (never hardcode passwords)
5. **Role-based access** for admin endpoints (`@PreAuthorize("hasRole('ADMIN')")`)

---

## 📦 Dependencies (pom.xml)

- `spring-boot-starter-web` — REST API
- `spring-boot-starter-data-jpa` — ORM
- `spring-boot-starter-security` — Auth
- `spring-boot-starter-validation` — Bean validation
- `h2` — In-memory DB (dev)
- `mysql-connector-j` — MySQL (prod)
- `jjwt-api/impl/jackson` — JWT tokens
- `lombok` — Boilerplate reduction
