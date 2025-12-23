# Auto-Parts Inventory Management System 🚗🔧

A production-ready Node.js backend designed for high-performance auto-parts inventory management. This system handles complex business logic, including automated bulk product ingestion via simulated email triggers, strict Role-Based Access Control (RBAC), and multi-field data deduplication.



## 🌟 Key Features

* **Automated Bulk Ingestion:** Processes large product datasets (1k+ rows) via a simulated email API endpoint.
* **Intelligent Deduplication:** Prevents data redundancy by filtering incoming products against existing `productCode` AND `name` records at the service layer.
* **Role-Based Access Control (RBAC):**
    * **Admin:** Full access (Create Single Product, Edit, View, Delete).
    * **Staff:** Operations access (View Product List, Delete Product).
* **Secure Authentication:** State-of-the-art JWT-based authentication with protected route middleware.
* **Security Hardening:** Implements registered-email validation for ingestion and centralized error handling for database constraints.
* **Containerized:** Fully Dockerized for seamless deployment across environments.

---

## 🛠️ Tech Stack

* **Runtime:** Node.js (v22.x)
* **Framework:** Express.js
* **Database:** MongoDB via Mongoose ODM
* **Security:** JSON Web Tokens (JWT) & Bcrypt
* **Testing:** Axios-based Automated Integration Suite
* **Infrastructure:** Docker & Docker Compose

---

## 📂 Project Structure

Following **Clean Architecture** principles, the project is divided into logical modules:

```text
src/
 ├── config/         # Database and Environment configurations
 ├── middleware/     # Auth, RBAC, and Centralized Error Handling
 ├── modules/        # Domain-driven modules (Screaming Architecture)
 │    ├── auth/      # Login & Token logic
 │    ├── email/     # Bulk ingestion & Email simulation
 │    ├── products/  # Inventory management (CRUD)
 │    └── users/     # User models and roles
 ├── utils/          # Shared helpers and loggers
 ├── app.js          # Express app setup
 └── server.js       # Entry point
