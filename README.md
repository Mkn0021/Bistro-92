# Bistro92 - High Concurrency Smart Restaurant Ordering System 🚀

![Docker](https://img.shields.io/badge/Docker-Containerized-blue?logo=docker)
![Node.js](https://img.shields.io/badge/Node.js-Backend-green?logo=node.js)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-blue?logo=postgresql)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-Queue-orange?logo=rabbitmq)

---

# 📚 Case Study - Problem Description

The project solves the following real-world challenges presented in the Techathon Preliminary Case:

- Customers order digitally in the restaurant.
- Hundreds to thousands of customers ordering **at the same time**.
- **Estimated wait time** must be shown dynamically to customers.
- **Backend must not crash** under heavy load.
- **Data consistency** must be maintained (no wrong orders or stock loss).
- **Scalable architecture** for future growth.
- **Backend source code must be protected** (only share Docker image).

---

# ✅ Our Solution Strategy

| Problem | How We Solved It |
|:--------|:-----------------|
| High Concurrent Orders | Used **Sequelize Transactions** + **RabbitMQ Async Processing** |
| API Crash Prevention | Non-critical tasks moved to **RabbitMQ Queues** |
| Dynamic Waiting Time | Average preparation time fetched from system load |
| Source Code Protection | Backend API **Dockerized** and pulled from **Docker Hub** |
| Scalability | Microservices style - DB, API, Queue separate containers |
| Lightweight Frontend | Pure HTML, CSS, JavaScript (no React/Angular overhead) |

✅ The solution is **production-ready**, **scalable**, and **very fast**.

---

# 🛠 Backend API - Node.js Architecture

Although backend source code is not shared (only Docker image),  
the backend Node.js architecture is organized like this:

| Folder/File | Purpose |
|:------------|:--------|
| `app.js` | Express App Setup |
| `routes/` | API Endpoints (`menuRoutes.js`, `orderRoutes.js`, etc.) |
| `controllers/` | API Logic Controllers |
| `models/` | Sequelize Models (Branch, Table, MenuItem, Order, OrderItem) |
| `services/` | Business Logic (Order Service, Payment Service) |
| `workers/` | RabbitMQ Worker Consumers |
| `config/` | Database Configuration and Connection |

✅ Built using **Express.js**, **PostgreSQL** with **Sequelize ORM**, and **RabbitMQ** for async messaging.

✅ Protected inside a **Docker Image** `mkn0021/bistro92-api`.

---

# 📦 Project Directory Structure

```plaintext
bistro92-final-project/
├── frontend/
│   ├── index.html
│   ├── AdminDashboard.css
├── docker-compose.yml
├── README.md ( this file )

```

# 🚀 How to Run Bistro92 (Step-by-Step)


## Step 1️⃣: Install Docker and Docker Compose

Make sure you have:
- [Docker](https://docs.docker.com/get-docker/) installed
- [Docker Compose](https://docs.docker.com/compose/install/) installed

To check installation:

```bash
docker --version
docker-compose --version
```
## Step 2️⃣: Start Backend Services

Run the following command to start all backend services:

```bash
docker-compose up --build
```

✅ This will:
- Start **PostgreSQL** database
- Start **RabbitMQ** server
- Pull and start **Bistro92 Backend API** from Docker Hub

> ⚡ The backend source code is hidden inside a secure Docker image (`mkn0021/bistro92-api`).

---

## Step 4️⃣: Verify Backend is Running

After running `docker-compose up`, check the following:

- **API Base URL** (Backend API):

```plaintext
http://localhost:3000/api
```

- **RabbitMQ Management Dashboard**:

```plaintext
http://localhost:15672
Username: guest
Password: guest
```

✅ Both should be accessible if containers are running correctly.

---

## Step 5️⃣: Run the Frontend

1. Go inside the `frontend/` folder.
2. Open `index.html` manually in your browser (double click).

✅ Frontend will automatically connect to:

```plaintext
http://localhost:3000/api
```

✅ You can now:
- Browse Menu
- Place Orders
- See Estimated Wait Times

---

## 📚 API Endpoints Table

| Method | Endpoint | Description |
|:-------|:---------|:------------|
| GET | `/api/menu/:branchId` | Get menu items of a specific branch |
| POST | `/api/menu` | Add a new menu item to a branch |
| GET | `/api/orders/:orderId` | Get order details and status |
| POST | `/api/orders` | Place a new customer order |
| GET | `/api/estimated-wait-time` | Get current average estimated wait time |
| GET | `/api/branches` | Get list of all restaurant branches |
| POST | `/api/branches` | Add a new restaurant branch |
| GET | `/api/tables/:branchId` | Get tables for a specific branch |
| POST | `/api/tables` | Add a new table in a branch |
| POST | `/api/payments` | Simulate order payment (optional) |
| GET | `/api/admin/orders` | Get all orders (Admin access) |
| PATCH | `/api/admin/orders/:orderId` | Update order status (Admin access) |

✅ All APIs must include API key in request headers:
```http
x-api-key: 835cf0faa598693992deb0cdd41f1142164a4f1b9f9014ba7fd4af4e8d9fa1d9
```

✅ Otherwise, the server will reject unauthorized requests for security reasons.