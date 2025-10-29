![Logo](https://app.jitumessage.com/media/logos/logo.png)

# JituMessage

**JituMessage** is a multi-channel communication platform built with a microservices architecture, supporting **SMS, WhatsApp, Email, and RCS**.

---

## 🚀 Setup Instructions

### 1. Prepare the `dist` Folder

Create the `dist` directory at the root of the project:

```bash
mkdir dist
```

Move the `messagehubctl.py and .sec` file into the `dist` directory:

```bash
mv messagehubctl.py ./dist && mv .sec ./dist
```

> Update variables inside the file to match your environment.

---

### 2. Import Databases

#### **MySQL**

1. Dump the SQL file from the production database.
2. Check *System Config* on the dashboard for connection details.
3. Import the dump into your local server.

#### **PostgreSQL**

1. Ensure **PostgreSQL** and **PgBouncer** services are available.
2. Import `messagehubposgres.sql` into your local PostgreSQL instance.
3. Update and verify `pgbouncer.ini` configuration.

#### **MongoDB**

1. Make sure **MongoDB service** is running.
2. Adjust the configuration to match your MongoDB setup.

#### **Redis**

1. Ensure **Redis service** is active.
2. Adjust the configuration to match your Redis setup.

---

### 3. Initial Configuration

Move `gohee.conf` into the `./dist` folder.
This file is required to establish the first MySQL connection and load configurations.

---

### 4. Verify Configuration

Check the `config` table to ensure service keys are aligned with your local connections:

```sql
SELECT * FROM config WHERE name = 'services';
```

Update the values if needed so they match your environment.

---

### 5. Build All Services

Build executables, frontend public files, and required directories:

```bash
./gheen.py build all
```

---

### 6. SSL Configuration (Optional)

If SSL is enabled, create a `certs` folder inside `dist`:

```bash
mkdir ./dist/certs
```

Place your certificate and key files inside:

```bash
ls ./dist/certs
```

---

### 7. Start the Dashboard

Run the dashboard application:

```bash
./dist/messagehubctl.py start dashboard
```

Access the login page in your browser:

```bash
curl -X GET 'localhost:3000'
```

> Use the username and password generated during the database import (Step #2).

---

### 8. Build Microservices

Navigate to the service handlers directory and build all microservices:

```bash
./service_handlers.py build all
```

---

### 9. Start Microservices

Navigate to the services directory inside `dist`:

```bash
cd ./dist/services
```

Start all microservices:

```bash
./servicectl.py start all
```

Check logs to confirm microservices are running correctly.

---

## 🏗️ Architecture

This project is composed of several microservices:

* **🚀 Blast Engine** (`src/service_handlers/`)
  Core messaging engine with an async worker pool.

* **🔐 OTP Engine** (`src/service_handlers/otpservice`)
  Core OTP service (🚧 under construction 🚧).

* **🐘 Postgres Utils** (`src/service_handlers/otpservice`)
  Uses PostgreSQL functions for automatic partitioning.

* **📊 Dashboard** (`src/dashboard/`)
  Web dashboard for monitoring and management.

---

## 🛠️ Tech Stack

* **Backend**: Go 1.24+
* **Frontend**: Vue.js 3 + TypeScript
* **Databases**: PostgreSQL, MariaDB/MySQL, MongoDB
* **Cache**: Redis
* **Queue**: RabbitMQ

---

## 📋 Prerequisites

* Go **1.24+**
* Node.js **18+** and **npm**
* VueJs **3+**
* PostgreSQL **13+**
* MariaDB/MySQL **8+**
* Redis **6+**
* RabbitMQ **3.8+**
* MongoDB **7.0.2+**

---

## 🤝 Contributing

1. Fork this repository

2. Create a feature branch:

   ```bash
   git checkout -b feature/AmazingFeature
   ```

3. Commit your changes:

   ```bash
   git commit -m 'Add some AmazingFeature'
   ```

4. Push to the branch:

   ```bash
   git push origin feature/AmazingFeature
   ```

5. Open a Pull Request

---

## ⚡ Built with **MessageHub Engine x GoHee v3.0**

---

## 👨‍💻 Authors

* [@fuadsyah](https://github.com/fuadsyah)

---

## 📎 Appendix

[![Static Badge](https://img.shields.io/badge/Engine_ORCHESTRA-brightgreen)](https://github.com/fuadsyah/messagehub/tree/main/src/service_handlers/services/blast_engine)


## Related Docs
- [Email Config Documentation](README.email_config.md)