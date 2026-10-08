# vpn
A risk-adaptive enterprise file-sharing MVP built with PHP, Java Spring Boot, and MySQL, featuring AES-GCM file encryption, SHA-256 integrity checks, multi-level approvals, audit logging, and WireGuard VPN deployment guidance.
# SecureShare Enterprise 🔐

### Risk-Adaptive Secure Enterprise File Sharing System

SecureShare Enterprise is a secure file-sharing project designed to help organizations share confidential files among employees while maintaining access control, data confidentiality, integrity verification, and security monitoring.

The system combines a PHP frontend, Java Spring Boot backend, and MySQL database with multi-level authorization, risk-based security checks, encrypted file storage, and audit logging.

## ✨ Key Features

* **Role-Based Access Control (RBAC):** Employee, Manager, and Admin roles.
* **Three-Level File Classification:** Normal, Confidential, and Highly Confidential.
* **Multi-Level Approval:** Manager approval for confidential files and Manager + Admin approval for highly confidential files.
* **AES-GCM Encryption:** Protects files stored by the application.
* **SHA-256 Integrity Verification:** Checks file integrity before release.
* **Risk Assessment:** Basic rule-based checks for suspicious download activity.
* **Secure File Sharing:** Upload, share, receive, download, and revoke future access.
* **Audit Logging:** Records important system activities.
* **Notifications:** Supports user and approval notifications.
* **WireGuard VPN Guidance:** Documents the separate VPN configuration and network restrictions.
* **Admin Monitoring:** Provides basic system metrics and audit information.

## 🛠️ Technology Stack

* **Frontend:** PHP, HTML, CSS
* **Backend:** Java 21, Spring Boot
* **Database:** MySQL 8
* **Encryption:** AES-GCM
* **Integrity Verification:** SHA-256
* **VPN:** WireGuard
* **Build Tool:** Apache Maven

## 🏗️ System Architecture

```text
       Employee / Manager / Admin
                  |
                  v
           PHP Frontend
                  |
                  v
       Java Spring Boot Backend
           /             \
          v               v
       MySQL        Encrypted File Storage
                     AES-GCM + SHA-256

        WireGuard VPN Layer
        Configured Separately
```

## 🔒 File Security Levels

| Security Level      | Authorization                                             |
| ------------------- | --------------------------------------------------------- |
| Normal              | No additional approval required, subject to access checks |
| Confidential        | Manager approval required                                 |
| Highly Confidential | Manager approval followed by Admin approval               |

Employees can act as both senders and receivers. Manager and Admin are additional approval and administrative roles.

## 📂 Project Structure

```text
secure-enterprise-file-sharing/
├── frontend/
│   └── index.php
├── backend/
│   ├── pom.xml
│   └── src/
│       └── main/
│           ├── java/
│           └── resources/
├── database/
│   └── schema.sql
├── deploy/
│   └── wireguard/
├── docs/
├── scripts/
└── tests/
```

## ⚙️ Installation and Setup

### Prerequisites

Install the following software:

* Java JDK 21
* Apache Maven
* MySQL 8
* PHP 8.2 or later
* PHP cURL extension

WireGuard must be installed and configured separately to enable VPN connectivity.

### Step 1: Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/secure-enterprise-file-sharing.git
cd secure-enterprise-file-sharing
```

Replace `YOUR_USERNAME` with your GitHub username.

### Step 2: Set Up the Database

Open MySQL Workbench and execute the SQL script:

```text
database/schema.sql
```

Configure the database credentials in the backend environment.

### Step 3: Configure the Encryption Key

Generate a secure development key in PowerShell:

```powershell
$key = [Convert]::ToBase64String(
    [Security.Cryptography.RandomNumberGenerator]::GetBytes(32)
)
$env:APP_MASTER_KEY = $key
$env:DB_USER = "root"
$env:DB_PASSWORD = "YOUR_MYSQL_PASSWORD"
```

Keep the key private and stable while encrypted test files exist. Never upload passwords or encryption keys to GitHub.

### Step 4: Start the Java Backend

```powershell
cd backend
mvn spring-boot:run
```

### Step 5: Start the PHP Frontend

Open another PowerShell terminal:

```powershell
cd frontend
php -S localhost:8081
```

Open the following address in your browser:

```text
http://localhost:8081
```

Follow the project's setup instructions to create the first administrator account.

## 🛡️ Security Considerations

The project demonstrates multiple security mechanisms, but additional work is necessary before production use.

* Configure WireGuard routes and firewall rules to enforce VPN-only access where required.
* Use HTTPS, CSRF protection, secure session cookies, and multi-factor authentication for privileged users.
* Implement enterprise-grade key management.
* Add malware scanning and comprehensive file-sensitivity analysis.
* Complete automated approval expiry and concurrency-safe download restrictions.
* Protect audit logs against tampering.
* Perform integration testing and a professional security review.

**Note:** The current MVP uses HTTP API endpoints for file transfers. A dedicated Java Socket transfer service and complete production VPN enforcement are not yet implemented. Basic risk checks are a prototype, not a validated AI security model.

## 🔬 Research and Future Enhancements

* Intelligent risk-adaptive authorization.
* Advanced confidential-data detection.
* Automated approval expiry and notifications.
* Dedicated authenticated Java Socket file transfer.
* Enterprise key management and key rotation.
* Advanced security analytics and anomaly detection.
* Comprehensive integration and performance testing.

## 🎯 Project Objective

To develop a user-friendly enterprise file-sharing platform that combines encryption, integrity verification, multi-level authorization, and risk-aware security controls to improve the protection of confidential organizational files.

## ⚠️ Disclaimer

This project is intended for educational and research purposes. It is a development MVP and has not been certified for production use with real confidential company data.
