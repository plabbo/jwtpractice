# JWT Authentication Spring Boot Demo

A Spring Boot application demonstrating JWT (JSON Web Token) authentication and authorization with Spring Security.

## Features

- User registration and authentication
- JWT token generation and validation
- Secured REST endpoints
- H2 in-memory database
- Spring Security integration

## Technologies Used

- **Spring Boot 3.5.0**
- **Spring Security** - Authentication and authorization
- **Spring Data JPA** - Database operations
- **JWT (jjwt 0.11.5)** - Token generation and validation
- **H2 Database** - In-memory database
- **Lombok** - Reduce boilerplate code
- **Maven** - Dependency management

## Project Structure

```
src/main/java/com/example/jwt_demo/
├── controller/
│   ├── AuthController.java      # Authentication endpoints
│   └── TestController.java      # Test endpoints
├── model/
│   └── User.java               # User entity
├── repository/
│   └── UserRepository.java     # User data access
├── security/
│   ├── AuthEntryPointJwt.java  # Authentication entry point
│   ├── AuthTokenFilter.java    # JWT filter
│   ├── JwtUtil.java           # JWT utility methods
│   └── WebSecurityConfig.java  # Security configuration
├── service/
│   └── CustomUserDetailsService.java # User details service
└── JwtDemoApplication.java     # Main application class
```

## Prerequisites

- Java 17 or higher
- Maven 3.6+
- IDE (VS Code, IntelliJ IDEA, Eclipse)

## Installation & Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/plabbo/jwtpractice.git
   cd jwtpractice
   ```

2. **Build the project**
   ```bash
   mvn clean install
   ```

3. **Run the application**
   ```bash
   mvn spring-boot:run
   ```

The application will start on `http://localhost:8080`

## API Endpoints

### Authentication Endpoints

| Method | Endpoint | Description | Authentication |
|--------|----------|-------------|----------------|
| POST | `/api/auth/signup` | Register a new user | No |
| POST | `/api/auth/signin` | Login user and get JWT token | No |

### Test Endpoints

| Method | Endpoint | Description | Authentication |
|--------|----------|-------------|----------------|
| GET | `/api/test/all` | Public endpoint | No |
| GET | `/api/test/user` | Secured endpoint | JWT Required |

## Usage Examples

### 1. Register a New User

**Request:**
```http
POST http://localhost:8080/api/auth/signup
Content-Type: application/json

{
    "username": "testuser",
    "password": "testpass"
}
```

**Response:**
```
User registered successfully!
```

### 2. User Login

**Request:**
```http
POST http://localhost:8080/api/auth/signin
Content-Type: application/json

{
    "username": "testuser",
    "password": "testpass"
}
```

**Response:**
```
eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ0ZXN0dXNlciIsImlhdCI6MTcwNzc0MDQyNCwiZXhwIjoxNzA3NzQ0MDI0fQ.abc123...
```

### 3. Access Public Endpoint

**Request:**
```http
GET http://localhost:8080/api/test/all
```

**Response:**
```
Public Content.
```

### 4. Access Secured Endpoint

**Request:**
```http
GET http://localhost:8080/api/test/user
Authorization: Bearer eyJhbGciOiJIUzI1NiJ9...
```

**Response:**
```
User Content.
```

## Testing with Postman

1. **Import the collection** or create requests manually
2. **Register a user** using `/api/auth/signup`
3. **Login** using `/api/auth/signin` and copy the JWT token
4. **Access secured endpoints** by adding the token in Authorization header:
   - Type: `Bearer Token`
   - Token: `your-jwt-token-here`

## Configuration

### Application Properties

```properties
# JWT Configuration
jwt.secret=thisIsMySuperSecureJWTKey1234567890TokenSecretKey88
jwt.expiration=3600000

# H2 Database Configuration
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# JPA Configuration
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=create-drop
spring.h2.console.enabled=true
```

### JWT Token Details

- **Algorithm:** HS256
- **Expiration:** 1 hour (3600000 ms)
- **Secret Key:** Configurable in application.properties

## Security Features

- **Password Encoding:** BCrypt encryption
- **JWT Validation:** Token signature and expiration validation
- **Stateless Authentication:** No server-side sessions
- **CORS Disabled:** For simplicity (enable as needed)
- **CSRF Disabled:** Suitable for REST APIs

## Database

The application uses H2 in-memory database:
- **Console:** `http://localhost:8080/h2-console`
- **JDBC URL:** `jdbc:h2:mem:testdb`
- **Username:** `sa`
- **Password:** (empty)

## Common Issues & Solutions

### JWT Token Expired
- **Error:** 401 Unauthorized
- **Solution:** Login again to get a new token

### Invalid Token Format
- **Error:** "Value contains invalid newline characters"
- **Solution:** Use Postman's Authorization tab with Bearer Token type

### Dependencies Not Found
- **Error:** JWT classes cannot be resolved
- **Solution:** Run `mvn clean install` to download dependencies

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Author

Created as a learning project for JWT authentication in Spring Boot.

---

⭐ If you found this helpful, please give it a star!
