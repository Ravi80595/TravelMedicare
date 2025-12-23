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

 🚀 Getting Started1. PrerequisitesNode.js (v18+) or Docker Desktop installed.A MongoDB Atlas connection string (or local MongoDB).2. Environment SetupCreate a .env file in the root directory:Code snippetPORT=5000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=HARDCODED_SECRET_123
3. Installation & SeedingBash# Install dependencies
npm install

# Seed the database with Admin, Staff, and Registered Supplier users
npm run seed
4. Running the AppOption A: Standard ExecutionBashnpm start
Option B: Docker (Recommended)Bashdocker-compose up --build
🔌 API EndpointsAutomated IngestionMethodEndpointAccessDescriptionPOST/email/productsRegistered EmailSimulates incoming email with bulk product data.Inventory ManagementMethodEndpointAccessDescriptionGET/productsAdmin, StaffView all inventory items.POST/productsAdmin OnlyManually create a single product.PUT/products/:idAdmin OnlyEdit an existing product.DELETE/products/:idAdmin, StaffRemove a product from inventory.✅ Quality AssuranceThis project includes a Comprehensive Integration Test Suite that verifies all requirements in a single run.To run the test suite:Bashnpm run test
Verified Scenarios:[x] JWT Authentication & Role Identification.[x] Admin-only authorization for Product Creation/Editing.[x] Staff permissions for Viewing and Deletion.[x] Bulk Deduplication Logic (Name/Code collisions).[x] Security: Unauthorized/Unregistered email blocking (403).🧠 Architectural HighlightsDeduplication Strategy: Instead of relying solely on database errors, the service layer performs a pre-check using MongoDB $or queries to identify collisions in both name and productCode, ensuring clean data ingestion.Graceful Error Handling: A centralized middleware catches 11000 (Duplicate Key) Mongo errors and custom validation errors, returning semantic HTTP status codes.Modular Scalability: Each feature is contained within its own module, allowing for easy expansion (e.g., adding an 'Orders' or 'Customers' module) without affecting existing logic.
