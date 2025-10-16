
# Chatify - MERN Chat Application with RabbitMQ & Microservices

A scalable, production-ready real-time chat application built using the MERN stack with microservices architecture, RabbitMQ for asynchronous communication, Redis caching, and Socket.IO for real-time messaging.

***

## Table of Contents

- Project Overview  
- Features  
- Architecture  
- Tech Stack  
- Setup Instructions  
  - Prerequisites  
  - Clone Repository  
  - Backend Setup  
  - Frontend Setup  
  - Docker Setup  
- Environment Variables  
- Running the Application  
- Testing  
- Deployment  
- Security  
- Contributing  
- License  
- Contact  

***

## Project Overview

This chat app uses three backend microservices:  
- **User Service**: Manages authentication and user profiles  
- **Mail Service**: Handles OTP-based email authentication asynchronously using RabbitMQ  
- **Chat Service**: Manages chat rooms, messages, and real-time communication  

RabbitMQ coordinates asynchronous tasks between services. Redis is used for caching, OTP storage, and real-time presence tracking. Real-time messaging and events use Socket.IO. The frontend is built with Next.js providing server-side rendering and API routes where needed.

***

## Features

- Real-time chat and presence with Socket.IO  
- OTP-based user authentication (email verification)  
- Asynchronous service communication with RabbitMQ  
- Redis caching to improve performance and manage OTPs  
- Message delivery status (seen/unseen) and typing indicators  
- Image uploads with optional captions  
- Modular microservice architecture for scalability  

***

## Architecture

```
[Next.js Frontend] <---> [API Gateway / Load Balancer] <---> [Backend Microservices]
                           |                            |--> User Service
                           |                            |--> Mail Service
                           |                            |--> Chat Service
                           |
                      [RabbitMQ Message Broker]
                           |
                      [Redis Cache]
                           |
                      [MongoDB Atlas]
```

***

## Tech Stack

| Layer           | Technology                       |
|-----------------|--------------------------------|
| Frontend        | Next.js                        |
| Backend         | Node.js, Express.js            |
| Database        | MongoDB (Atlas)                |
| Message Broker  | RabbitMQ                      |
| Caching / PubSub| Redis                        |
| Real-Time Comm  | Socket.IO                     |
| Containerization| Docker                        |

***

## Setup Instructions

### Prerequisites

- Node.js >= 16.x  
- npm >= 8.x  
- Docker (for RabbitMQ and Redis)  
- MongoDB Atlas account  

### Clone Repository

```bash
git clone https://github.com/your-repo/mern-chat-app.git
cd mern-chat-app
```

### Backend Setup

Navigate to each microservice folder under `/backend` (user-service, mail-service, chat-service) and:

```bash
npm install
npm run build
```

Set up environment variables as described below.

### Frontend Setup

In the frontend folder:

```bash
npm install
npm run dev
```

***

### Docker Setup

Run RabbitMQ and Redis containers locally:

```bash
docker run -d --hostname rabbitmq --name rabbitmq-container -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=admin123 -p 5672:5672 -p 15672:15672 rabbitmq:3-management
docker run -d --name redis-container -p 6379:6379 redis
```

***

## Environment Variables

Create `.env` files in backend microservices with:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string

RABBITMQ_HOST=localhost
RABBITMQ_PORT=5672
RABBITMQ_USERNAME=admin
RABBITMQ_PASSWORD=admin123

REDIS_URL=redis://localhost:6379

JWT_SECRET=your_jwt_secret

EMAIL_SERVICE_API_KEY=your_email_service_api_key
```

Frontend environment variables should include backend service URLs if needed.

***

## Running the Application

- Run each backend microservice:

```bash
npm run dev
```

- Start the Next.js frontend:

```bash
npm run dev
```

- Access RabbitMQ Management UI at [http://localhost:15672](http://localhost:15672)  
- Redis runs on port 6379 by default  

***

## Testing

- Use Postman or similar to test APIs  
- Use the frontend UI to verify chat, authentication, and real-time features  
- Monitor RabbitMQ queues and Redis for cache/OTP verification  

***

## Deployment

- Backend microservices can be containerized with Docker and deployed on any server or container orchestration platform  
- Frontend can be deployed on platforms supporting Next.js such as Vercel or any Node.js-compatible host  
- MongoDB Atlas and Redis instances should be properly configured in production  

***

## Security

- JWT tokens for secure API access  
- OTP tokens stored in Redis with expiry  
- RabbitMQ secured with authentication and optional SSL  
- HTTPS enforced on frontend and backend endpoints  
- Input validation and sanitization applied  

***