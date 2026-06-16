# Catering Service

Microservices-based catering platform built using Spring Boot and Spring Cloud. The platform enables end-to-end management of catering events - from initial client inquiry and menu personalization, through payment and partner coordination, to real-time delivery tracking. It supports four user roles: clients, employees, partner businesses and administrator.

## Architecture

All client requests enter the system through a single API Gateway, which routes them to the appropriate microservice based on Eureka service discovery. Authentication is handled by a dedicated Auth Service using JWT tokens, which every microservice validates independently.

Inter-service communication is handled in two ways:
- **REST API** for synchronous calls between services
- **RabbitMQ** for asynchronous event-driven communication - used between the User & Event service and the Logistics & Partner service when a partner is invited to participate in an event organization

Real-time features (client-employee chat and post-login notifications) are powered by **WebSocket** connections managed through the User & Event service.

Each microservice owns its own isolated **PostgreSQL** database following the Database-per-Service pattern.

### Services

- [Frontend App](https://github.com/Catering-service/frontend) - React + Vite SPA
- [API Gateway](https://github.com/Catering-service/gateway-service) - Spring Cloud Gateway, single entry point for all HTTP requests
- [Service Discovery](https://github.com/Catering-service/eureka-server) - Eureka Server, dynamic service registry
- [Auth Service](https://github.com/Catering-service/auth-service) - JWT authentication, Spring Security, sends credentials via email on account creation
- Microservices
  - [User & Event Management Service](https://github.com/Catering-service/user-event-service) - clients, employees, events, tickets, menus, locations, chat, loyalty program
  - [Finance Service](https://github.com/Catering-service/finance-service) - invoices, proforma invoices, payments (Stripe), email delivery of invoices
  - [Logistics & Partner Service](https://github.com/Catering-service/logistics-partner-service) - partner management, service offerings, delivery tracking, partner email notifications
  - [Analytics & Admin Service](https://github.com/Catering-service/analytics-admin-service) - business analytics, employee performance, AI chatbot interaction logging, admin panel

### External Integrations

| Integration | Used by | Purpose |
|---|---|---|
| Stripe | Finance Service | Card payment processing |
| Gmail SMTP (JavaMailSender) | Auth, Finance, Logistics | Account credentials, invoices, partner notifications |
| Groq API (LLaMA) | Frontend (direct) | AI chatbot on the public landing page |

## Tech Stack

### Frontend
- React
- Vite

### Backend
- Java 21
- Spring Boot 4.0.x
- Spring Cloud (Gateway, Eureka)
- Maven
- WebSocket (STOMP)
- RabbitMQ

### Data
- PostgreSQL (per-service isolated databases)

### DevOps
- Docker
- Docker Compose

## Getting Started

The entire platform is containerised - every microservice, database, and infrastructure component (RabbitMQ, Eureka) runs as a Docker container. To build the application follow the instruction provided in [deployment repository](https://github.com/Catering-service/deployment).

## Video presentation of key concepts and UI
[Link to the video]()

## Team

- [Merjem Gutošić](https://github.com/GutosicMerjem)
- [Ivona Jozić](https://github.com/ijozic1)
- [Kanita Kadušić](https://github.com/kanitakadusic)
- [Ismar Muslić](https://github.com/imuslic1)
