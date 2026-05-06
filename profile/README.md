# Welcome to Ecomera 🛍️

> Full-stack e-commerce platform demonstrating monolithic to microservices migration

## About This Project

Ecomera is a full-stack e-commerce platform that demonstrates the complete journey from monolithic architecture to microservices. This project showcases both architectural approaches: the original monolithic application and its decomposed microservices implementation, providing a comprehensive view of service-oriented architecture evolution.

## 🎯 Project Objectives

- Demonstrate monolithic to microservices migration strategy
- Implement complete microservices infrastructure with service discovery and configuration management
- Build production-ready distributed system with independent, scalable services
- Showcase enterprise patterns: API Gateway, distributed caching, CI/CD, and containerization

## 📦 Repositories

### Monolithic Reference

- **[ecomera-backend](https://github.com/ecomera-ecosystem/ecomera-backend)** - Original monolithic Spring Boot application
  - Complete e-commerce business logic (Authentication, Products, Orders, Payments, Cart)
  - Serves as reference architecture and comparison point
  - Demonstrates well-structured modular monolith with clear domain boundaries

### Microservices

- **[ecomera-auth-service](https://github.com/ecomera-ecosystem/ecomera-auth-service)** - Authentication & Authorization microservice
  - User registration, login, and JWT token management
  - Secure authentication endpoints

- **[ecomera-product-service](https://github.com/ecomera-ecosystem/ecomera-product-service)** - Product Catalog microservice
  - Product CRUD operations
  - Category management
  - Inventory tracking

- **[ecomera-order-service](https://github.com/ecomera-ecosystem/ecomera-order-service)** - Order Management microservice
  - Order creation and processing
  - Order history and tracking
  - Order item management

- **[ecomera-payment-service](https://github.com/ecomera-ecosystem/ecomera-payment-service)** - Payment Processing microservice
  - Payment transaction handling
  - Payment method management
  - Transaction history

- **[ecomera-cart-service](https://github.com/ecomera-ecosystem/ecomera-cart-service)** - Shopping Cart microservice
  - Cart creation and management
  - Cart item operations
  - Session-based cart handling

- **[ecomera-notification-service](https://github.com/ecomera-ecosystem/ecomera-notification-service)** - Notification microservice
  - Event-driven notifications via Apache Kafka
  - Email notification delivery
  - MongoDB for notification history storage

### Infrastructure & Gateway

- **[ecomera-api-gateway](https://github.com/ecomera-ecosystem/ecomera-api-gateway)** - Spring Cloud Gateway
  - Unified entry point for all microservices
  - Request routing and load balancing
  - Cross-cutting concerns (logging, security)

- **[ecomera-eureka-service-registry](https://github.com/ecomera-ecosystem/ecomera-eureka-service-registry)** - Service Discovery
  - Dynamic service registration and discovery
  - Health monitoring and failover
  - Load balancing support

- **[ecomera-config-server](https://github.com/ecomera-ecosystem/ecomera-config-server)** - Configuration Management
  - Centralized configuration for all microservices
  - HashiCorp Vault integration for secrets
  - Environment-specific properties

- **[ecomera-api-config](https://github.com/ecomera-ecosystem/ecomera-api-config)** - Configuration Repository
  - Git-based configuration storage
  - Service-specific configuration files

### Identity & Access Management

- **[ecomera-keycloak](https://github.com/ecomera-ecosystem/ecomera-keycloak)** - Identity Provider
  - Centralized authentication and authorization
  - OAuth2 / OpenID Connect support
  - User federation and role-based access control

### Frontend

- **[ecomera-frontend](https://github.com/ecomera-ecosystem/ecomera-frontend)** - Angular application
  - Angular Material UI components
  - TypeScript with reactive programming
  - Communicates with microservices via API Gateway
  - Karma-Jasmine testing
  - Tailwind CSS styling

## 🛠️ Technology Stack

### Backend

- **Java** - Core programming language
- **Spring Boot** - Microservice framework
- **Spring Cloud** - Microservices ecosystem (Eureka, Config Server, Gateway)
- **Maven** - Build automation and dependency management
- **Redis** - Distributed caching layer
- **JUnit & Mockito** - Testing framework

### Identity & Security

- **Keycloak** - Identity and access management (OAuth2 / OIDC)
- **HashiCorp Vault** - Secrets management
- **JWT** - Token-based authentication

### Messaging & Storage

- **Apache Kafka** - Event-driven messaging and notification streaming
- **MongoDB** - Document database for notification history
- **PostgreSQL** - Relational database for core business data

### Frontend

- **Angular** - Frontend framework
- **Angular Material** - UI component library
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling
- **Karma & Jasmine** - Testing tools

### DevOps & Infrastructure

- **Docker** - Containerization for all services
- **GitHub Actions** - CI/CD automation
- **SonarQube** - Code quality and static analysis
- **HashiCorp Vault** - Secrets management
- **Eureka** - Service discovery and registration

## Microservices Architecture

The platform implements a fully distributed microservices architecture:

```
                     ┌─────────────────┐
                     │  Angular UI     │
                     └────────┬────────┘
                              │
                     ┌────────▼────────┐
                     │  API Gateway    │
                     │  (Port: 8080)   │
                     └────────┬────────┘
                              │
           ┌──────────────────┼─────────────────┐
           │                  │                 │
     ┌─────▼─────┐     ┌──────▼─────┐     ┌─────▼─────┐
     │   Auth    │     │  Product   │     │   Order   │
     │  Service  │     │  Service   │     │  Service  │
     └─────┬─────┘     └─────┬──────┘     └─────┬─────┘
           │                 │                 │
           │         ┌───────▼─────────┐       │
           │         │    Payment      │       │
           └─────────┤    Service      ├───────┘
                     └────────┬────────┘
                              │
                     ┌────────▼────────┐
                     │      Cart       │
                     │    Service      │
                     └────────┬────────┘
                              │
                     ┌────────▼────────┐
                     │  Notification   │
                     │    Service      │
                     └────────┬────────┘
                              │
              ┌───────────────┼───────────────┐
              │               │               │
        ┌─────▼──────┐ ┌──────▼─────┐  ┌──────▼─────┐
        │   Kafka    │ │  MongoDB   │  │   Email    │
        │  Broker    │ │   Store    │  │   SMTP     │
        └────────────┘ └────────────┘  └────────────┘

           ┌──────────────────────────────────────┐
           │            Infrastructure             │
           ├──────────────────┬───────────────────┤
           │ Eureka Registry  │  Config Server    │
           │  (Port: 8761)    │  (Port: 8888)     │
           │                  │                   │
           │ Keycloak (OIDC)  │ HashiCorp Vault   │
           │                  │                   │
           │ SonarQube        │ Redis Cache       │
           └──────────────────┴───────────────────┘
```

### Service Communication

- **Synchronous** - REST APIs via Spring Cloud OpenFeign
- **Asynchronous** - Apache Kafka for event-driven notifications
- **Service Discovery** - Eureka-based dynamic service location
- **Load Balancing** - Client-side load balancing with Spring Cloud LoadBalancer
- **API Gateway** - Single entry point routing to appropriate microservices
- **Identity Provider** - Keycloak for centralized OAuth2/OIDC authentication

## Key Features

### Microservices Implementation

- **Independent Services** - Each business domain is an autonomous microservice
- **Service Discovery** - Dynamic service registration and discovery with Eureka
- **API Gateway** - Centralized routing, authentication, and rate limiting
- **Distributed Configuration** - Externalized configuration management
- **Independent Deployment** - Each service can be deployed independently
- **Fault Tolerance** - Service isolation prevents cascading failures

### Technical Capabilities

- **Distributed Caching** - Redis for cross-service caching
- **Identity Management** - Keycloak OAuth2/OIDC for centralized authentication
- **Event-Driven Architecture** - Kafka-based messaging for notifications
- **Secrets Management** - HashiCorp Vault integration
- **Code Quality** - SonarQube static analysis and quality gates
- **Comprehensive Testing** - Unit and integration tests for each service
- **CI/CD Pipeline** - Automated build, test, and deployment per service
- **Containerization** - Docker images for all services

### Business Features

- **User Authentication** - Secure registration and login via Keycloak
- **Product Catalog** - Complete product management
- **Shopping Cart** - Real-time cart operations
- **Order Processing** - End-to-end order workflow
- **Payment Processing** - Secure payment handling
- **Notifications** - Kafka-driven email notifications for order updates

## 📂 Project Structure

```
ecomera/
├── ecomera-backend/                  # Original monolithic reference
├── ecomera-auth-service/             # Authentication microservice
├── ecomera-product-service/          # Product catalog microservice
├── ecomera-order-service/            # Order management microservice
├── ecomera-payment-service/          # Payment processing microservice
├── ecomera-cart-service/             # Shopping cart microservice
├── ecomera-notification-service/     # Notification microservice (Kafka + MongoDB)
├── ecomera-api-gateway/              # API Gateway
├── ecomera-eureka-service-registry/  # Service discovery
├── ecomera-config-server/            # Configuration server
├── ecomera-api-config/               # Configuration repository
├── ecomera-keycloak/                 # Identity provider (OAuth2/OIDC)
├── ecomera-frontend/                 # Angular application
└── .github/                          # CI/CD centralized workflows

```

## 🚀 Migration Journey

This project demonstrates the complete migration from monolithic to microservices:

**Phase 1: Monolithic Foundation**

- Built complete e-commerce functionality in single application
- Established clear module boundaries
- Identified service decomposition points

**Phase 2: Infrastructure Setup**

- Deployed Eureka for service discovery
- Configured Spring Cloud Config Server with HashiCorp Vault
- Implemented API Gateway
- Set up Keycloak for centralized identity management

**Phase 3: Service Decomposition**

- Extracted Authentication service
- Separated Product catalog service
- Isolated Order management service
- Created Payment processing service
- Deployed Cart management service

**Phase 4: Event-Driven Notifications**

- Implemented notification service with Apache Kafka
- MongoDB for notification history storage
- Email, SMS, and push notification delivery

**Phase 5: Integration & Testing**

- Inter-service communication via REST APIs and Kafka events
- Distributed caching with Redis
- End-to-end testing across services
- CI/CD pipeline for each microservice with SonarQube quality gates

## 📫 Connect

This project demonstrates comprehensive full-stack development and distributed systems architecture.

- **LinkedIn**: [Youssef Ammari](https://linkedin.com/in/am-ysf)
- **Email**: youssef.ammari.795@gmail.com

---

<div align="center">
  <strong>Complete monolithic to microservices migration project</strong>
  <br>
  <sub>Spring Boot • Spring Cloud • Angular • Docker • Redis • Eureka • API Gateway • Keycloak • Vault • Kafka • MongoDB • SonarQube</sub>
</div>
