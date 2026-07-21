# Secure LAMP Stack Blogging Platform

A full-stack web application and security audit project built using a **LAMP** (Linux, Apache, MySQL, PHP) architecture. This project demonstrates relational database design (normalized to 2NF+), full-stack web development, and application security—specifically identifying, exploiting, and mitigating common vulnerabilities such as SQL Injection (SQLi).

---

## Key Features

* **User Authentication:** Secure user registration and login functionality.
* **Content Management:** Create, store, and display dynamic blog posts.
* **Search Functionality:** Query blog posts dynamically from the database.
* **Normalized Relational Database:** Engineered database schema conforming to 2nd Normal Form (2NF) rules.
* **Security & Vulnerability Mitigation:** Hardened application scripts against SQL Injection and server-level vulnerabilities.

---

## Tech Stack

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Operating System** | Linux (Ubuntu Server) | Environment hosting application services and firewall settings |
| **Web Server** | Apache HTTP Server | Web server managing HTTP requests and directory indexes |
| **Database** | MySQL | Relational database handling users, posts, and comments |
| **Backend** | PHP | Server-side script handling business logic and DB communication |
| **Frontend** | HTML5 / CSS3 | Web interface and input forms |

---

## Project Architecture & Structure

```text
.
├── config/
│   └── db_connect.php     # MySQL database connection configuration
├── sql/
│   ├── schema.sql         # Table definitions and constraints
│   └── seed.sql           # Initial seed data for users/posts
├── public/
│   ├── index.php          # Main blog feed
│   ├── login.php          # User login handling
│   ├── register.php       # User registration
│   ├── create_post.php    # Form and handler for adding new posts
│   └── search.php         # Search functionality
├── docs/
│   └── Security_Report.pdf # Detailed analysis of vulnerabilities and remediations
└── README.md
```

---

## Database Design

The relational database was designed and normalized to **2nd Normal Form (2NF)** to eliminate redundant data and maintain data integrity.

### Primary Entities & Relationships
* **Users:** Stores authentication credentials and user profile info.
* **Posts:** Contains blog post content linked via foreign key to the `Users` table.
* **Comments:** (If implemented) Stores discussion entries tied to specific `Posts` and `Users`.

---

## Application Security & Hardening

As part of this project, a security assessment was conducted to identify common web vulnerabilities and harden the platform:

### 1. SQL Injection (SQLi) Remediation
* **Vulnerability:** Unsanitized user input concatenated directly into SQL queries allowed for authentication bypass and unauthorized data access.
* **Mitigation:** Replaced dynamic string concatenation with **Prepared Statements** (`PDO` or `mysqli_stmt`) to separate SQL logic from data inputs.

### 2. Server & Environment Security
* **UFW Firewall:** Restricted unnecessary external access while explicitly exposing required ports (Apache, SSH, MySQL over SSH tunnel).
* **Access Management:** Enforced least-privilege principles and strong authentication across user accounts.

---

## Getting Started & Setup

### Prerequisites
* A Linux environment (Ubuntu 22.04 LTS recommended)
* Apache2
* MySQL Server
* PHP 8.x with `php-mysql` extension enabled

### Setup Instructions

1. **Clone the Repository**
   ```bash
   git clone [https://github.com/your-username/your-repo-name.git](https://github.com/your-username/your-repo-name.git)
   cd your-repo-name
   ```

2. **Configure Database**
   Log into MySQL and run the setup scripts:
   ```bash
   mysql -u root -p < sql/schema.sql
   mysql -u root -p < sql/seed.sql
   ```

3. **Update Connection Parameters**
   Edit `config/db_connect.php` with your local database credentials:
   ```php
   $host = 'localhost';
   $dbname = 'your_db_name';
   $username = 'your_db_user';
   $password = 'your_secure_password';
   ```

4. **Deploy Web Files**
   Copy web interface files to Apache’s root directory:
   ```bash
   sudo cp -r public/* /var/www/html/
   ```

5. **Configure Apache Directory Index**
   Ensure `index.php` is prioritized in `/etc/apache2/mods-enabled/dir.conf`:
   ```apache
   <IfModule mod_dir.c>
       DirectoryIndex index.php index.html
   </IfModule>
   ```
   Restart Apache to apply changes:
   ```bash
   sudo systemctl restart apache2
   ```

---
