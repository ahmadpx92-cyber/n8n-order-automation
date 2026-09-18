# n8n-order-automation
# 🛒 E-Commerce Order Automation Pipeline (n8n, Docker & MySQL)

A robust backend automation workflow built to ingest, process, and securely store e-commerce customer orders in real-time. This project serves as a practical demonstration of integrating workflow automation tools with containerized databases for a **Junior Automation Developer** application.

---

## 🏗️ Architecture & Tech Stack

* **Workflow Automation:** [n8n](https://n8n.io/) (Self-hosted via Docker)
* **Containerization & Networking:** Docker, Docker Compose (`host.docker.internal` network bridge configuration)
* **Database:** MySQL 8.0 (Custom relational schema for order tracking)
* **Data Transformation:** JavaScript (Custom payload mapping and validation)

---

## 🔄 Workflow Pipeline Flow

1. **Webhook Ingestion:** 
   * Receives incoming order payloads (Customer details, requested items, and order metadata) via a secure local test webhook endpoint (`/webhook-test/...`).
2. **JavaScript Transformation Node:** 
   * Extracts raw JSON payloads, sanitizes the data structure, handles mapping rules, and formats data objects to precisely match the target relational database schema.
3. **MySQL Database Storage Node:** 
   * Executes dynamic SQL `INSERT` statements to persistently record transaction data into a normalized `orders` table.

---

## 📊 Database Schema (`store_db`)

The relational database uses an `orders` table structured as follows:

```sql
CREATE DATABASE store_db;

USE store_db;

CREATE TABLE orders (
    id INT AUTO_INCREMENT PRIMARY KEY,
    customer_name VARCHAR(255) NOT NULL,
    product_name VARCHAR(255) NOT NULL,
    quantity INT NOT NULL,
    total_price DECIMAL(10, 2) NOT NULL,
    order_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
