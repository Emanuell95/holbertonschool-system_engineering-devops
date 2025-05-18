# Web Infrastructure Design Project

This project explores the evolution of a web infrastructure from a simple single-server stack to a secure, scalable, and highly available architecture that supports `www.foobar.com`.

---

## 🌐 Overview

The goal is to design, document, and whiteboard different stages of infrastructure used to host a website:

- Basic LAMP-like stack on one server
- Load-balanced, redundant architecture
- Secure infrastructure with HTTPS and firewall rules
- Fully scaled-out deployment with separated components (web, app, DB)
- Monitoring for performance and availability

---

## ✅ Tasks Breakdown

### 0. Simple Web Stack

**Components**:
- 1 domain name `foobar.com` (`www` record → IP 8.8.8.8)
- 1 server containing:
  - Nginx (web server)
  - Application server (e.g., PHP, Python)
  - Application files
  - MySQL (database)

📸 [Diagram](https://imgur.com/your_simple_stack_screenshot)

---

### 1. Redundant Web Stack

**Added**:
- 1 load balancer (HAProxy)
- 2 servers (each with web server, app, DB)

📸 [Diagram](https://imgur.com/your_redundant_stack_screenshot)

**Benefits**:
- Load distribution
- Higher availability
- Redundancy

---

### 2. Secured Web Stack

**Added**:
- 3 firewalls (one per server)
- HTTPS via SSL certificate (e.g., Let’s Encrypt)
- 3 monitoring clients (e.g., for Sumo Logic)

📸 [Diagram](https://imgur.com/your_secure_stack_screenshot)

**Why?**:
- 🔐 Firewalls protect access to services
- 🔒 HTTPS encrypts user-server communication
- 📈 Monitoring enables health, alerting, and analytics

---

### 3. Scaled-Up Architecture

**Added**:
- 1 new load balancer (HAProxy) for clustering
- Infrastructure split:
  - **Web Server**: Only Nginx
  - **App Server**: Only business logic
  - **Database Server**: Only MySQL
- Each with their own firewall and monitoring agent

📸 [Diagram](https://imgur.com/your_scaled_up_stack_screenshot)

**Why?**:
- 🧱 Separation of concerns improves performance and scaling
- ⚖️ Load balancer clustering eliminates SPOF at the front
- 🛡️ Better isolation and security
- 🔄 Each component can now scale independently

---

## 🔍 Key Concepts Explained

### What Is a Server?
A physical or virtual machine that hosts services or applications users interact with.

### What Is the Role of a Domain Name?
Translates human-readable names (e.g., `www.foobar.com`) into IP addresses via DNS.

### What Type of DNS Record Is `www`?
An **A record** pointing to the server’s IP (e.g., `8.8.8.8`).

### What Do Each of These Do?
| Component        | Role                                                                 |
|------------------|----------------------------------------------------------------------|
| Web Server       | Serves static content and routes dynamic requests to the app server |
| Application Server | Executes business logic and processes user requests               |
| Database         | Stores persistent data (users, posts, etc.)                          |
| Load Balancer    | Distributes requests between multiple backend servers               |
| SSL Certificate  | Enables encrypted HTTPS connections                                  |
| Firewall         | Restricts network access by port and IP                              |
| Monitoring Client| Tracks system and app metrics, logs, and alerts                     |

---

## ⚠️ Infrastructure Limitations & Risks

| Risk Area                     | Explanation                                                                                      |
|------------------------------|--------------------------------------------------------------------------------------------------|
| SPOF (Single Point of Failure) | If one HAProxy fails without clustering, traffic cannot reach servers                          |
| SSL Termination at Load Balancer | Traffic between LB and backend is unencrypted unless re-encrypted or proxied securely       |
| Single Writable MySQL Server  | If it fails, no writes are possible. Should use master-replica or clustering                  |
| Combined Components on One Host | Web + app + DB together creates security, scaling, and resource contention problems           |
| No Monitoring or Alerting    | Cannot detect failures or performance degradation                                              |

---

## ✅ Final Scaled Architecture

- 🔁 Clustered HAProxy load balancers
- 🔗 HTTPS-enabled with SSL certificates
- 🔥 Firewalls on all component servers
- 📦 Split roles into isolated servers:
  - Web: Nginx
  - App: Application server
  - DB: MySQL
- 📈 Monitoring clients on all servers

---

## 🧠 Key Takeaways

- Infrastructure evolves in complexity as needs grow (performance, traffic, fault tolerance)
- Security and monitoring are essential at every level
- Splitting services across hosts improves scalability and maintainability
- Load balancing and failover mechanisms reduce downtime

---

## ✍️ Author

**Emanuel Mendoza**

Project for Full Stack Web Development Program  