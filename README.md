# Resource Booking System

A secure RESTful **Resource Booking System** built using **Java, Spring Boot, Spring Security, JWT, JPA/Hibernate, and MySQL**.

The application allows users to authenticate using JWT, view available resources, create and manage their own reservations, while administrators have full control over resources, users, and reservations.

---

## 🚀 Features

* JWT-based authentication
* Role-Based Access Control (RBAC)
* ADMIN and USER roles
* Secure REST APIs
* Resource CRUD operations
* Reservation creation and management
* Reservation ownership validation
* Double-booking / reservation conflict prevention
* Reservation status management
* Filtering by reservation status
* Filtering by minimum and maximum price
* Pagination and sorting
* Request validation
* Global exception handling
* BCrypt password encryption
* Swagger / OpenAPI documentation
* Database initialization with sample data
* JUnit and MockMvc testing
* Postman API collection

---

## 🛠️ Technology Stack

| Technology         | Purpose                        |
| ------------------ | ------------------------------ |
| Java 17            | Programming Language           |
| Spring Boot 3.3.4  | Backend Framework              |
| Spring Security    | Authentication & Authorization |
| JWT                | Token-Based Authentication     |
| Spring Data JPA    | Database Access                |
| Hibernate          | ORM                            |
| MySQL              | Production Database            |
| H2                 | Testing Database               |
| Maven              | Build & Dependency Management  |
| Lombok             | Reduce Boilerplate Code        |
| Jakarta Validation | Request Validation             |
| Swagger / OpenAPI  | API Documentation              |
| JUnit 5            | Unit Testing                   |
| Mockito            | Mocking                        |
| MockMvc            | API Testing                    |
| Postman            | API Testing                    |

---

# 🏗️ Project Architecture

The application follows a **Layered Architecture**.

```text
                    Client / Postman
                           |
                           v
                 +-------------------+
                 |   Spring Security |
                 |    JWT Filter     |
                 +-------------------+
                           |
                           v
                 +-------------------+
                 |    Controller     |
                 +-------------------+
                           |
                           v
                 +-------------------+
                 |     Service       |
                 |  Business Logic   |
                 +-------------------+
                           |
                           v
                 +-------------------+
                 |    Repository     |
                 +-------------------+
                           |
                           v
                 +-------------------+
                 |   MySQL Database  |
                 +-------------------+
```

### Request Flow

```text
HTTP Request
     |
     v
JWT Authentication Filter
     |
     v
SecurityContext
     |
     v
Controller
     |
     v
Service
     |
     v
Repository
     |
     v
Database
```

---

# 📁 Project Structure

```text
resource-booking-system/
│
├── pom.xml
├── database.sql
├── README.md
├── .gitignore
│
├── Resource-Booking-System.postman_collection.json
│
└── src/
    │
    ├── main/
    │   │
    │   ├── java/
    │   │   └── com/
    │   │       └── example/
    │   │           └── resourcebooking/
    │   │
    │   │               ├── ResourceBookingApplication.java
    │   │               │
    │   │               ├── config/
    │   │               │   ├── DataInitializer.java
    │   │               │   └── OpenApiConfig.java
    │   │               │
    │   │               ├── controller/
    │   │               │   ├── AuthController.java
    │   │               │   ├── ResourceController.java
    │   │               │   ├── ReservationController.java
    │   │               │   └── UserController.java
    │   │               │
    │   │               ├── dto/
    │   │               │   ├── ErrorResponse.java
    │   │               │   ├── LoginRequest.java
    │   │               │   ├── LoginResponse.java
    │   │               │   ├── PageResponse.java
    │   │               │   ├── ReservationRequest.java
    │   │               │   ├── ReservationResponse.java
    │   │               │   ├── ResourceRequest.java
    │   │               │   ├── ResourceResponse.java
    │   │               │   └── UserResponse.java
    │   │               │
    │   │               ├── entity/
    │   │               │   ├── User.java
    │   │               │   ├── Resource.java
    │   │               │   └── Reservation.java
    │   │               │
    │   │               ├── enums/
    │   │               │   ├── Role.java
    │   │               │   └── ReservationStatus.java
    │   │               │
    │   │               ├── repository/
    │   │               │   ├── UserRepository.java
    │   │               │   ├── ResourceRepository.java
    │   │               │   └── ReservationRepository.java
    │   │               │
    │   │               ├── service/
    │   │               │   ├── AuthService.java
    │   │               │   ├── UserService.java
    │   │               │   ├── ResourceService.java
    │   │               │   └── ReservationService.java
    │   │               │
    │   │               ├── security/
    │   │               │   ├── JwtService.java
    │   │               │   ├── JwtAuthenticationFilter.java
    │   │               │   ├── SecurityConfig.java
    │   │               │   └── CustomUserDetailsService.java
    │   │               │
    │   │               ├── exception/
    │   │               │   ├── GlobalExceptionHandler.java
    │   │               │   ├── BadRequestException.java
    │   │               │   ├── BookingConflictException.java
    │   │               │   ├── UnauthorizedException.java
    │   │               │   ├── UserNotFoundException.java
    │   │               │   ├── ResourceNotFoundException.java
    │   │               │   └── ReservationNotFoundException.java
    │   │               │
    │   │               └── specification/
    │   │                   └── ReservationSpecification.java
    │   │
    │   ├── resources/
    │   │   └── application.properties
    │   │
    │   └── test/
    │       ├── java/
    │       │   └── com/example/resourcebooking/
    │       │       └── ResourceBookingApplicationTests.java
    │       │
    │       └── resources/
    │           └── application-test.properties
```

---

# 📦 Package Explanation

## 1. `controller`

The Controller layer handles incoming HTTP requests and returns HTTP responses.

### `AuthController`

Responsible for:

* User login
* Authentication request
* Generating JWT token

Example:

```text
POST /auth/login
```

### `ResourceController`

Responsible for:

* Create resource
* Get resources
* Get resource by ID
* Update resource
* Delete resource

### `ReservationController`

Responsible for:

* Create reservation
* Get reservations
* Get reservation by ID
* Update reservation
* Delete reservation

### `UserController`

Responsible for ADMIN operations related to users.

---

# 2. `service`

The Service layer contains the application's **business logic**.

```text
Controller
    ↓
Service
    ↓
Repository
```

### `AuthService`

Handles:

* Authentication
* Password verification
* JWT generation

### `UserService`

Handles:

* User retrieval
* Current authenticated user
* User-related business logic

### `ResourceService`

Handles:

* Resource creation
* Resource retrieval
* Resource update
* Resource deletion

### `ReservationService`

Handles:

* Reservation creation
* Reservation update
* Reservation deletion
* Ownership validation
* Double-booking prevention
* Reservation filtering
* Pagination

---

# 3. `repository`

The Repository layer communicates with the database using Spring Data JPA.

### `UserRepository`

Handles User database operations.

### `ResourceRepository`

Handles Resource database operations.

### `ReservationRepository`

Handles Reservation database operations.

```text
Service
   ↓
Repository
   ↓
Hibernate / JPA
   ↓
MySQL
```

---

# 4. `entity`

Entity classes represent database tables.

### `User`

Represents application users.

```text
User
 ├── id
 ├── username
 ├── password
 └── role
```

### `Resource`

Represents bookable resources.

Examples:

* Room
* Vehicle
* Equipment

### `Reservation`

Represents a booking made for a resource.

```text
Reservation
 ├── id
 ├── resource
 ├── user
 ├── startTime
 ├── endTime
 ├── price
 └── status
```

---

# 5. `dto`

DTO stands for **Data Transfer Object**.

DTOs are used to control the data sent between the client and server instead of exposing entity objects directly.

### Request DTOs

```text
LoginRequest
ResourceRequest
ReservationRequest
```

Used when the client sends data to the API.

### Response DTOs

```text
LoginResponse
ResourceResponse
ReservationResponse
UserResponse
```

Used when the server sends data back to the client.

### Other DTOs

```text
ErrorResponse
PageResponse
```

Used for standardized error and pagination responses.

---

# 6. `security`

This package handles application security.

### `SecurityConfig`

Configures:

* Spring Security
* Public endpoints
* Protected endpoints
* Role-based authorization
* Password encoder
* Authentication configuration

### `JwtService`

Responsible for:

* Creating JWT tokens
* Validating JWT tokens
* Extracting username
* Extracting role
* Checking token expiration

### `JwtAuthenticationFilter`

Runs for every secured request.

It:

1. Reads the `Authorization` header.
2. Extracts the Bearer token.
3. Validates the JWT.
4. Extracts the username and role.
5. Sets authentication in `SecurityContext`.

Example:

```text
Authorization: Bearer <JWT_TOKEN>
```

### `CustomUserDetailsService`

Loads user information from the database during authentication.

---

# 7. `exception`

Contains custom exceptions and centralized exception handling.

Examples:

```text
UserNotFoundException
ResourceNotFoundException
ReservationNotFoundException
BookingConflictException
BadRequestException
UnauthorizedException
```

### `GlobalExceptionHandler`

Provides centralized handling of exceptions and returns consistent API error responses.

Example:

```json
{
  "status": 404,
  "message": "Resource not found"
}
```

---

# 8. `specification`

Contains dynamic database filtering logic.

### `ReservationSpecification`

Used for filtering reservations by:

```text
status
minPrice
maxPrice
```

Example:

```text
GET /reservations?status=CONFIRMED
```

or:

```text
GET /reservations?minPrice=1000&maxPrice=5000
```

Multiple filters can also be combined.

---

# 9. `enums`

Contains predefined application values.

### `Role`

```text
ADMIN
USER
```

### `ReservationStatus`

```text
PENDING
CONFIRMED
CANCELLED
```

Using enums prevents invalid values from being stored in the application.

---

# 10. `config`

Contains application configuration classes.

### `DataInitializer`

Automatically creates initial users and sample data when the application starts.

### `OpenApiConfig`

Configures Swagger / OpenAPI documentation.

---

# 🔐 Authentication & Authorization

The project uses **JWT-based stateless authentication**.

### Login Flow

```text
User
 |
 | POST /auth/login
 v
AuthController
 |
 v
AuthService
 |
 v
Spring Security
 |
 v
Validate Username + Password
 |
 v
Generate JWT
 |
 v
Return Token
```

The client then sends the token with every secured request:

```text
Authorization: Bearer <JWT_TOKEN>
```

---

# 👥 Role-Based Access Control

The system has two roles:

| Feature                | ADMIN | USER |
| ---------------------- | :---: | :--: |
| Login                  |   ✅   |   ✅  |
| View Resources         |   ✅   |   ✅  |
| Create Resource        |   ✅   |   ❌  |
| Update Resource        |   ✅   |   ❌  |
| Delete Resource        |   ✅   |   ❌  |
| Create Reservation     |   ✅   |   ✅  |
| View Own Reservations  |   ✅   |   ✅  |
| View All Reservations  |   ✅   |   ❌  |
| Manage Any Reservation |   ✅   |   ❌  |
| View Users             |   ✅   |   ❌  |

---

# 🔒 Reservation Ownership

A major security feature of this project is **reservation ownership enforcement**.

A USER cannot provide another user's ID and access their reservation.

The authenticated user is identified from the JWT.

```text
JWT
 ↓
Username
 ↓
Current User
 ↓
Reservation Ownership Check
```

Therefore:

```text
USER → Own Reservation → Allowed
USER → Another User's Reservation → Forbidden
ADMIN → Any Reservation → Allowed
```

---

# 🚫 Double Booking Prevention

The application checks whether a resource already has a reservation for the requested time period.

If an overlapping reservation exists:

```text
409 CONFLICT
```

is returned instead of allowing the booking.

Example:

```text
Resource: Meeting Room A

Existing:
10:00 AM → 12:00 PM

New Request:
11:00 AM → 01:00 PM

Result:
❌ Booking Conflict
```

---

# 📄 Pagination

Reservation APIs support pagination.

Example:

```http
GET /reservations?page=0&size=10
```

Example response:

```json
{
  "content": [],
  "page": 0,
  "size": 10,
  "totalElements": 25,
  "totalPages": 3
}
```

---

# 🔎 Reservation Filtering

Reservations can be filtered using:

### Status

```http
GET /reservations?status=CONFIRMED
```

### Minimum Price

```http
GET /reservations?minPrice=1000
```

### Maximum Price

```http
GET /reservations?maxPrice=5000
```

### Combined Filters

```http
GET /reservations?status=CONFIRMED&minPrice=1000&maxPrice=5000
```

Filtering is implemented using **JPA Specifications**.

---

# 🌐 API Endpoints

## Authentication

| Method | Endpoint      | Access |
| ------ | ------------- | ------ |
| POST   | `/auth/login` | Public |

## Resources

| Method | Endpoint          | Access       |
| ------ | ----------------- | ------------ |
| POST   | `/resources`      | ADMIN        |
| GET    | `/resources`      | ADMIN / USER |
| GET    | `/resources/{id}` | ADMIN / USER |
| PUT    | `/resources/{id}` | ADMIN        |
| DELETE | `/resources/{id}` | ADMIN        |

## Reservations

| Method | Endpoint             | Access       |
| ------ | -------------------- | ------------ |
| POST   | `/reservations`      | ADMIN / USER |
| GET    | `/reservations`      | ADMIN / USER |
| GET    | `/reservations/{id}` | ADMIN / USER |
| PUT    | `/reservations/{id}` | ADMIN / USER |
| DELETE | `/reservations/{id}` | ADMIN / USER |

## Users

| Method | Endpoint      | Access |
| ------ | ------------- | ------ |
| GET    | `/users`      | ADMIN  |
| GET    | `/users/{id}` | ADMIN  |

---

# 🗄️ Database

The application uses **MySQL**.

Main tables:

```text
users
resources
reservations
```

Relationship:

```text
User
 |
 | 1
 |
 | *
Reservation
 |
 | *
 |
 | 1
Resource
```

A user can have multiple reservations.

A resource can have multiple reservations at different time periods.

---

# ⚙️ Configuration

Update:

```text
src/main/resources/application.properties
```

Example:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/resource_booking_db
spring.datasource.username=root
spring.datasource.password=root
```

For security, sensitive values such as database passwords and JWT secrets should be provided through environment variables in real deployments.

---

# ▶️ How to Run

## Prerequisites

Make sure you have:

* Java 17+
* Maven
* MySQL
* Git
* Postman (optional)

---

## 1. Clone Repository

```bash
git clone https://github.com/YOUR_USERNAME/resource-booking-system.git
```

```bash
cd resource-booking-system
```

---

## 2. Configure MySQL

Create the database:

```sql
CREATE DATABASE resource_booking_db;
```

Update your database credentials in:

```text
src/main/resources/application.properties
```

---

## 3. Build Project

```bash
mvn clean install
```

---

## 4. Run Application

```bash
mvn spring-boot:run
```

Application will start at:

```text
http://localhost:8080
```

---

# 🧪 Testing

The project includes tests using:

* JUnit 5
* Mockito
* Spring Boot Test
* MockMvc
* H2 in-memory database

Run tests:

```bash
mvn test
```

The test environment does not require a MySQL database.

---

# 📮 Postman

A Postman collection is included in the repository:

```text
Resource-Booking-System.postman_collection.json
```

Import the collection into Postman and test the APIs.

Recommended testing flow:

```text
1. Login
   ↓
2. Get JWT Token
   ↓
3. Authorize requests
   ↓
4. Create Resource
   ↓
5. View Resources
   ↓
6. Create Reservation
   ↓
7. View Reservations
   ↓
8. Update / Cancel Reservation
```

---

# 📚 Swagger API Documentation

After starting the application, Swagger UI can be accessed at:

```text
http://localhost:8080/swagger-ui/index.html
```

Swagger can be used to:

* View API endpoints
* View request/response models
* Authorize using JWT
* Execute APIs directly from the browser

---

# 🔑 Sample Users

The application initializes sample users.

| Username | Password | Role  |
| -------- | -------- | ----- |
| admin    | admin123 | ADMIN |
| user     | user123  | USER  |

> These credentials are for local development/testing only. Change them before using the application in any real environment.

---

# 📂 Important Files

| File                                              | Purpose                                      |
| ------------------------------------------------- | -------------------------------------------- |
| `pom.xml`                                         | Maven dependencies and project configuration |
| `application.properties`                          | Application and database configuration       |
| `database.sql`                                    | Database setup/reference SQL                 |
| `ResourceBookingApplication.java`                 | Spring Boot application entry point          |
| `SecurityConfig.java`                             | Spring Security configuration                |
| `JwtService.java`                                 | JWT creation and validation                  |
| `JwtAuthenticationFilter.java`                    | JWT request authentication                   |
| `GlobalExceptionHandler.java`                     | Centralized exception handling               |
| `ReservationSpecification.java`                   | Dynamic reservation filtering                |
| `Resource-Booking-System.postman_collection.json` | API testing collection                       |

---

# 🎯 Project Objective

The objective of this project is to demonstrate the development of a secure, scalable RESTful backend application using modern Java and Spring Boot practices.

The project demonstrates:

* REST API development
* Layered architecture
* Spring Boot
* Spring Security
* JWT authentication
* Role-based authorization
* JPA/Hibernate
* MySQL database integration
* DTO-based API design
* Exception handling
* Validation
* Pagination
* Dynamic filtering
* Business rule implementation
* Automated testing
* API documentation

---

# 👨‍💻 Author

**Onkar Karande**

Java Full Stack Developer

GitHub: https://github.com/onkarkarande77

**Primary Technologies:**

```text
Java | Spring Boot | Spring Security | JWT |
Hibernate | JPA | MySQL | REST APIs |
React.js | JavaScript | Git | GitHub
```

---


# ⭐ Support

If you found this project useful, please consider giving it a ⭐ on GitHub.

It motivates me to build more full-stack projects and continue learning.
