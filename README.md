# Payment Transaction Monitoring System

Enterprise-style backend platform for secure payment transaction processing, fraud-risk monitoring, audit logging, and role-based access control.

## Project Overview

The **Payment Transaction Monitoring System** is a Java/Spring Boot backend designed for financial transaction workflows where security, traceability, and controlled access are critical. The service exposes REST APIs for transaction intake, risk evaluation, and administrative monitoring while enforcing JWT-based authentication and authorization.

## Features

- Secure transaction processing APIs
- Fraud-risk scoring and rule-based monitoring workflows
- Audit logging for security and compliance traceability
- JWT-based stateless authentication
- Spring Security role-based access control (RBAC)
- MySQL-backed persistent storage
- Dockerized runtime for consistent deployment

## Tech Stack

- **Language:** Java
- **Framework:** Spring Boot 3
- **Security:** Spring Security + JWT
- **Database:** MySQL
- **Containerization:** Docker
- **API Style:** RESTful services

## System Architecture

```text
Client / Admin Console
        |
        v
REST API Layer (Controllers)
        |
        v
Service Layer (Business + Risk Logic)
        |
        v
Persistence Layer (JPA/Repository)
        |
        v
MySQL Database

Cross-cutting: JWT Auth, Spring Security RBAC, Audit Logging
```

## API Modules

- **Auth Module**
  - User login and JWT issuance
  - Token validation for protected routes
- **Transaction Module**
  - Create and query payment transactions
  - Transaction status and metadata handling
- **Fraud Monitoring Module**
  - Risk checks based on configurable rules
  - Flagging/high-risk transaction workflows
- **Audit Module**
  - Security and operational event history
  - Action traceability by user and timestamp
- **Admin Module**
  - Role-restricted operational endpoints
  - Monitoring and management utilities

## Database Design Overview

Core entities typically include:

- `users` — identity and account status
- `roles` / `user_roles` — RBAC mapping
- `transactions` — payment payload, status, amount, timestamps
- `fraud_alerts` — risk score, reason codes, alert status
- `audit_logs` — actor, action, target, timestamp, outcome

High-level relationships:

- One user can create many transactions
- One transaction can produce zero or many fraud alerts
- One user can have multiple roles
- Audit logs capture authenticated actions across modules

## Authentication & Authorization

- Authentication is handled through JWT access tokens.
- Spring Security secures API endpoints and validates bearer tokens.
- Authorization is role-driven (for example: `ADMIN`, `ANALYST`, `USER`).
- Sensitive operations are restricted to elevated roles.

## Docker Setup

Build the application image:

```bash
docker build -t payment-monitoring-system .
```

Run the application container:

```bash
docker run -d \
  --name payment-monitoring-system \
  -p 8080:8080 \
  --env-file .env \
  payment-monitoring-system
```

Optional MySQL container (for local development):

```bash
docker run -d \
  --name payment-mysql \
  -e MYSQL_ROOT_PASSWORD=root \
  -e MYSQL_DATABASE=payment_monitoring \
  -p 3306:3306 \
  mysql:8
```

## Installation & Running Locally

### Prerequisites

- Java 17+
- Maven 3.8+
- MySQL 8+
- Docker (optional)

### Steps

1. Clone the repository:

   ```bash
   git clone https://github.com/DivyanshCh39/Payment-Transaction-Monitoring-System.git
   cd Payment-Transaction-Monitoring-System
   ```

2. Configure environment variables/application properties for:
   - Database URL, username, password
   - JWT secret and expiration settings

3. Build and run the application:

   ```bash
   mvn clean install
   mvn spring-boot:run
   ```

4. Access the API locally at:

   ```text
   http://localhost:8080
   ```

## Future Enhancements

- Advanced anomaly detection using ML-assisted risk models
- Real-time monitoring with Kafka/event streaming
- Dashboarding with metrics and alert visualizations
- Multi-tenant support for enterprise clients
- Fine-grained policy engine for dynamic access rules
- OpenAPI/Swagger documentation and SDK generation

## Project Structure

```text
Payment-Transaction-Monitoring-System/
├── src/
│   ├── main/
│   │   ├── java/.../config          # Security, JWT, app configuration
│   │   ├── java/.../controller      # REST endpoints
│   │   ├── java/.../service         # Business and monitoring logic
│   │   ├── java/.../repository      # Data access layer
│   │   ├── java/.../entity          # JPA entities
│   │   └── resources/               # application.properties, SQL scripts
│   └── test/                        # Unit and integration tests
├── Dockerfile
├── pom.xml
└── README.md
```
