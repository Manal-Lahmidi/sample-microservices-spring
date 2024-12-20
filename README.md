# Microservices with Spring Boot and Spring Cloud

## Objectives

- Create microservices using **Spring Boot** and **Spring Cloud**.
- Deploy microservices on multiple instances.

---

## Tools and Versions

- **Spring Boot**: Version 3.0.0 or later ([https://spring.io/projects/spring-boot](https://spring.io/projects/spring-boot))
- **Spring Cloud**: Version 2022.0.0 or later ([https://spring.io/projects/spring-cloud](https://spring.io/projects/spring-cloud))
- **Java**: Version 17
- **Maven**: Version 4.0.0 ([https://maven.apache.org/](https://maven.apache.org/))
- **IntelliJ IDEA**: Ultimate Edition

---

## Architecture Overview

Microservices Architecture (MSA) involves designing applications as independently deployable microservices. These services:

- Are organized around business capabilities.
- Support automatic deployment.
- Include intelligent endpoints.
- Utilize decentralized control over technologies and data.

### Proposed Architecture

The goal is to build independently deployable microservices communicating via Spring Cloud and Spring Boot tools. The microservices include:

1. **Product Service**: REST API to manage products.
2. **Config Service**: Centralized configuration management.
3. **Proxy Service**: Gateway for routing requests and load balancing.
4. **Discovery Service**: Dynamic service registration and discovery.

---

## Microservices Creation

### 1. ProductService

#### Setup

- Use [Spring Initializr](https://start.spring.io/) with the following configuration:
  - **Project**: Maven
  - **Java Version**: 17
  - **Spring Boot Version**: 3.0.0+
  - **Group**: `com.ecommerce`
  - **Artifact**: `product-service`
  - **Dependencies**:
    - Spring Web
    - Rest Repositories
    - Spring Data JPA
    - H2 Database
    - Spring Boot Actuator
    - Eureka Discovery Client
    - Config Client

#### Repository

- GitHub Repository: [Product Service](https://github.com/Manal-Lahmidi/product-service.git)

#### Testing

- Access the API:
  - All Products: `http://localhost:8080/products`
  - Single Product: `http://localhost:8080/products/1`

---

### 2. ConfigService

#### Setup

- Use [Spring Initializr](https://start.spring.io/) with the following configuration:
  - **Project**: Maven
  - **Artifact**: `config-service`
  - **Dependencies**:
    - Spring Cloud Config Server

#### Configuration

- Configure the application to use a local Git repository for centralized configuration management.
- Ensure the repository contains configuration files for all microservices.

#### Repository

- GitHub Repository: [Config Service](https://github.com/Manal-Lahmidi/config-service.git)

---

### 3. DiscoveryService

#### Setup

- Use [Spring Initializr](https://start.spring.io/) with the following configuration:
  - **Project**: Maven
  - **Artifact**: `discovery-service`
  - **Dependencies**:
    - Eureka Server
    - Config Client

#### Configuration

- Set up Eureka Server for service registration and discovery.
- Link the Discovery Service to the Config Service for centralized configuration.

#### Repository

- GitHub Repository: [Discovery Service](https://github.com/Manal-Lahmidi/discovery-service.git)

---

### 4. ProxyService

#### Setup

- Use [Spring Initializr](https://start.spring.io/) with the following configuration:
  - **Project**: Maven
  - **Artifact**: `proxy-service`
  - **Dependencies**:
    - Spring Cloud Gateway
    - Config Client
    - Eureka Discovery

#### Configuration

- Set up the Proxy Service to route requests to other microservices using Spring Cloud Gateway.
- Link the Proxy Service to the Config Service and Discovery Service for dynamic routing and configuration.

#### Repository

- GitHub Repository: [Proxy Service](https://github.com/Manal-Lahmidi/proxy-service.git)

---

## Running Multiple Instances

To run multiple `ProductService` instances, use different ports:

1. Create configurations for each instance with unique ports.
2. Ensure all instances register with the Discovery Service.

Test load balancing via the Proxy Service: `http://localhost:9999/product-service/messages`

---

## References

- [Spring Boot](https://spring.io/projects/spring-boot)
- [Spring Cloud](https://spring.io/projects/spring-cloud)
- [Spring Initializr](https://start.spring.io/)
