# 🎓 Smart Campus Navigation System — UNT

A full-stack campus navigation web application built for the University of North Texas. Students can sign up, sign in, and navigate UNT's campus with an interactive map, shuttle schedules, favorites, and real-time location support.

---

## 🖥️ Live Pages

| Page | Description |
|------|-------------|
| `homepage.html` | Login / Sign Up portal with UNT branding |
| `navpage.html` | Main navigation dashboard with interactive campus map |
| `busroutes.html` | UNT shuttle and bus route viewer using Leaflet.js |

---

## ✨ Features

### 🔐 Authentication (homepage.html)
- **Sign In** — Student ID + password login connected to Spring Boot backend
- **Sign Up** — Full registration with client-side validation:
  - 10-digit phone number check
  - Minimum 8-character password enforcement
  - Email format validation
  - Duplicate student ID detection (backend)
- **Forgot Password** — Email verification via EmailJS; checks if user exists in DB before sending reset link
- **Custom Alert Modals** — Styled UNT-branded popups replacing native browser alerts
- **Dark Mode** — CSS checkbox toggle for light/dark theme switching
- **Geolocation** — Captures and stores user location on load for navigation use

### 🗺️ Navigation Dashboard (navpage.html)
- Personalized greeting using `localStorage` (username from sign-in response)
- **Campus Toggle** — Switch between Main Campus and Discovery Park map views
- **Favorites** — Save and quick-access favourite campus locations
- **Shuttle Schedule** — Built-in shuttle timetable panel
- **Session Timeout Warning** — 10-minute inactivity countdown modal with reset option
- Google Maps embed integration for location search

### 🚌 Bus Routes (busroutes.html)
- Interactive map powered by **Leaflet.js**
- Frosted glass UI panels using CSS `backdrop-filter`
- UNT campus transit route visualization

---

## 🏗️ Architecture

```
Smart Campus Navigation System
├── Frontend (HTML / CSS / JavaScript)
│   ├── homepage.html      ← Login & Sign Up
│   ├── navpage.html       ← Navigation dashboard
│   ├── busroutes.html     ← Leaflet.js bus route map
│   └── styles.css         ← Shared stylesheet
│
└── Backend (Spring Boot REST API)
    └── src/main/java/edu/smartcampus/
        ├── model/          ← Student entity (JPA)
        ├── dto/            ← LoginRequest DTO
        ├── repository/     ← StudentRepository
        └── controller/     ← AuthController
```

---

## 🔗 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/auth/signup` | Register a new student |
| `POST` | `/api/auth/signin` | Authenticate and return student object |
| `POST` | `/api/auth/verify-email?email=` | Check if email exists (password reset flow) |

---

## 🧰 Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | HTML5, CSS3, JavaScript (ES6+, async/await, Fetch API) |
| Maps | Leaflet.js, Google Maps Embed API |
| Email | EmailJS (password reset) |
| Backend | Java 17, Spring Boot |
| ORM | Spring Data JPA |
| Database | MySQL / PostgreSQL |
| Build | Maven |
| Logging | Log4j2 |
| Testing | JUnit 5 + Mockito |

---

## ✅ Test Coverage — 10 Unit Tests

| Test | Scenario |
|------|----------|
| `testRegister_Success` | New student registers successfully |
| `testRegister_UserAlreadyExists` | Duplicate ID rejected (400) |
| `testRegister_DatabaseException` | DB failure returns 500 gracefully |
| `testLogin_Success` | Valid credentials return student object (200) |
| `testLogin_InvalidCredentials` | Unknown student ID returns 401 |
| `testLogin_WrongPassword` | Correct ID, wrong password returns 401 |
| `testLogin_Failure` | Additional unauthorized path covered |
| `testLogin_DatabaseException` | DB failure returns 500 gracefully |
| `testVerifyEmail_Success` | Existing email verified (200) |
| `testVerifyEmail_NotFound` | Unknown email returns 404 |
| `testVerifyEmail_Exception` | DB error returns 500 gracefully |

---

## ⚙️ Getting Started

### Prerequisites
- Java 17+, Maven 3.8+, MySQL or PostgreSQL

### Setup

```bash
git clone https://github.com/lathasaladi36/smart-campus-navigation-system.git
cd smart-campus-navigation-system
```

Create `src/main/resources/application.properties`:
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/smartcampus_db
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.jpa.hibernate.ddl-auto=update
```

Run:
```bash
./mvnw spring-boot:run
```

Open in browser: `http://localhost:8080/homepage.html`

Run tests:
```bash
./mvnw test
```

---

## 💡 Design Highlights

- Client-side validation before every API call — no unnecessary server requests
- Custom modal alerts instead of native browser popups — consistent UNT-branded UX
- EmailJS integration — password reset without a dedicated email server
- `localStorage` — persists username and geolocation across page navigation
- Frosted glass panels using CSS `backdrop-filter` for polished, modern UI
- Session timeout protection — automatic logout warning after inactivity

---

