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
- **[ecomera-backend](https://github.com/ecomera/ecomera-backend)** - Original monolithic Spring Boot application
  - Complete e-commerce business logic (Authentication, Products, Orders, Payments, Cart)
  - Serves as reference architecture and comparison point
  - Demonstrates well-structured modular monolith with clear domain boundaries

### Microservices
- **[ecomera-auth-service](https://github.com/ecomera/ecomera-auth-service)** - Authentication & Authorization microservice
  - User registration, login, and JWT token management
  - Secure authentication endpoints
  
- **[ecomera-product-service](https://github.com/ecomera/ecomera-product-service)** - Product Catalog microservice
  - Product CRUD operations
  - Category management
  - Inventory tracking

- **[ecomera-order-service](https://github.com/ecomera/ecomera-order-service)** - Order Management microservice
  - Order creation and processing
  - Order history and tracking
  - Order item management

- **[ecomera-payment-service](https://github.com/ecomera/ecomera-payment-service)** - Payment Processing microservice
  - Payment transaction handling
  - Payment method management
  - Transaction history

- **[ecomera-cart-service](https://github.com/ecomera/ecomera-cart-service)** - Shopping Cart microservice
  - Cart creation and management
  - Cart item operations
  - Session-based cart handling

### Infrastructure & Gateway
- **[ecomera-api-gateway](https://github.com/ecomera/ecomera-api-gateway)** - Spring Cloud Gateway
  - Unified entry point for all microservices
  - Request routing and load balancing
  - Cross-cutting concerns (logging, security)

- **[ecomera-eureka-service-registry](https://github.com/ecomera/ecomera-eureka-service-registry)** - Service Discovery
  - Dynamic service registration and discovery
  - Health monitoring and failover
  - Load balancing support

- **[ecomera-config-server](https://github.com/ecomera/ecomera-config-server)** - Configuration Management
  - Centralized configuration for all microservices
  - HashiCorp Vault integration for secrets
  - Environment-specific properties

- **[ecomera-api-config](https://github.com/ecomera/ecomera-api-config)** - Configuration Repository
  - Git-based configuration storage
  - Service-specific configuration files

### Frontend
- **[ecomera-frontend](https://github.com/ecomera/ecomera-frontend)** - Angular application
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

### Frontend
- **Angular** - Frontend framework
- **Angular Material** - UI component library
- **TypeScript** - Type-safe development
- **Tailwind CSS** - Utility-first styling
- **Karma & Jasmine** - Testing tools

### DevOps & Infrastructure
- **Docker** - Containerization for all services
- **GitHub Actions** - CI/CD automation
- **Qodana** - Code quality inspection
- **HashiCorp Vault** - Secrets management
- **Eureka** - Service discovery and registration

## 🏗️ Microservices Architecture

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
                    └─────────────────┘
                             │   
          ┌──────────────────┴─────────────────┐
          │                                    │
    ┌─────▼───────────┐                   ┌────▼──────────┐
    │ Eureka Registry │                   │ Config Server │
    │  (Port: 8761)   │                   │ (Port: 8888)  │
    └─────────────────┘                   └───────────────┘
```

### Service Communication
- **Synchronous** - REST APIs via Spring Cloud OpenFeign
- **Service Discovery** - Eureka-based dynamic service location
- **Load Balancing** - Client-side load balancing with Spring Cloud LoadBalancer
- **API Gateway** - Single entry point routing to appropriate microservices

## 💡 Key Features

### Microservices Implementation
- **Independent Services** - Each business domain is an autonomous microservice
- **Service Discovery** - Dynamic service registration and discovery with Eureka
- **API Gateway** - Centralized routing, authentication, and rate limiting
- **Distributed Configuration** - Externalized configuration management
- **Independent Deployment** - Each service can be deployed independently
- **Fault Tolerance** - Service isolation prevents cascading failures

### Technical Capabilities
- **Distributed Caching** - Redis for cross-service caching
- **Security** - JWT authentication managed by Auth service
- **Secrets Management** - HashiCorp Vault integration
- **Comprehensive Testing** - Unit and integration tests for each service
- **CI/CD Pipeline** - Automated build, test, and deployment per service
- **Containerization** - Docker images for all services
- **Code Quality** - Qodana static analysis

### Business Features
- **User Authentication** - Secure registration and login
- **Product Catalog** - Complete product management
- **Shopping Cart** - Real-time cart operations
- **Order Processing** - End-to-end order workflow
- **Payment Processing** - Secure payment handling

## 📂 Project Structure

```
ecomera/
├── ecomera-backend/              # Original monolithic reference
├── ecomera-auth-service/         # Authentication microservice
├── ecomera-product-service/      # Product catalog microservice
├── ecomera-order-service/        # Order management microservice
├── ecomera-payment-service/      # Payment processing microservice
├── ecomera-cart-service/         # Shopping cart microservice
├── ecomera-api-gateway/          # API Gateway
├── ecomera-eureka-service-registry/  # Service discovery
├── ecomera-config-server/        # Configuration server
├── ecomera-api-config/           # Configuration repository
├── ecomera-frontend/             # Angular application
└── .github/                      # CI/CD workflows
```

## 🚀 Migration Journey

This project demonstrates the complete migration from monolithic to microservices:

**Phase 1: Monolithic Foundation**
- Built complete e-commerce functionality in single application
- Established clear module boundaries
- Identified service decomposition points

**Phase 2: Infrastructure Setup**
- Deployed Eureka for service discovery
- Configured Spring Cloud Config Server
- Implemented API Gateway

**Phase 3: Service Decomposition**
- Extracted Authentication service
- Separated Product catalog service
- Isolated Order management service
- Created Payment processing service
- Deployed Cart management service

**Phase 4: Integration & Testing**
- Inter-service communication via REST APIs
- Distributed caching with Redis
- End-to-end testing across services
- CI/CD pipeline for each microservice

## 🎓 Architectural Lessons

**Why Keep the Monolith?**
- Reference for comparison and architectural decisions
- Demonstrates understanding of both approaches
- Shows migration path and decomposition strategy
- Useful for performance benchmarking

**Microservices Trade-offs**
- **Benefits**: Independent scaling, deployment, and technology choices
- **Challenges**: Distributed data management, increased complexity, network latency
- **Solution**: Proper service boundaries, API Gateway, service discovery

## 📫 Connect

This project demonstrates comprehensive full-stack development and distributed systems architecture.

- **LinkedIn**: [Youssef Ammari](https://linkedin.com/in/am-ysf) 
- **Email**: youssef.ammari.795@gmail.com
---

<div align="center">
  <strong>Complete monolithic to microservices migration project</strong>
  <br>
  <sub>Spring Boot • Spring Cloud • Angular • Docker • Redis • Eureka • API Gateway</sub>
</div>
