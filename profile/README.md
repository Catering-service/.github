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
[Link to the video](https://drive.google.com/file/d/1egPoPEA1NdjF01ibEGCmnuYkKpQHGDM4/view?usp=sharing)

## Video presentation Walkthrough

### Backend

- **00:00** - BE Tests
- **02:08** - Asynchronous Communication
- **05:44** - Synchronous Communication

### Security

- **07:52** - Security Overview
- **10:27** - Security Examples

### Frontend

- **11:56** - Frontend Overview

### Registration & Account Management

- **13:20** - Registration
- **14:56** - Account Settings
- **15:33** - Registration (User-Event Service Down)

### Partner

- **15:50** - Partner

### Client

- **16:51** - Client
  - **17:09** - Creating and Editing a Reservation
  - **18:09** - Menu Personalization

### Client & Employee Communication

- **19:51** - Ticketing and Communication
  - **20:24** - Partner Offerings Overview
  - **20:36** - Communication (WebSocket)
  - **21:51** - Contacting a Partner
  - **22:18** - Partner Response to Request

### Ratings, Tracking & Payments

- **23:30** - Employee Rating
- **24:01** - Delivery Tracking (Client)
- **24:36** - Payment (Client)
  - **25:15** - Invoice Creation and Delivery
  - **26:55** - Card Payment

### Employee

- **27:29** - Employee
  - **28:02** - Employee Dashboard
  - **28:56** - Proforma Invoice Creation
  - **30:23** - Sending Proforma Invoice via Chat

### Authentication

- **31:09** - Password Reset on First Login (Employee, Admin, and Partner)

### Administration

- **31:54** - Admin Panel
  - Events
  - Menu Items
  - Locations
  - Price per Person
  - Loyalty Categories
  - Clients
  - Administrators
  - Employees
  - Partners
  - Partner Offerings
  - AI Interaction Log

- **36:29** - Admin Analytics
- **37:42** - Session Management

### Testing & Greetings

- **38:28** - Frontend Testing
- **40:47** - Greetings
## Team

- [Merjem Gutošić](https://github.com/GutosicMerjem)
- [Ivona Jozić](https://github.com/ijozic1)
- [Kanita Kadušić](https://github.com/kanitakadusic)
- [Ismar Muslić](https://github.com/imuslic1)
