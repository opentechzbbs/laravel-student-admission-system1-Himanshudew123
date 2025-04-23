[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/ONVnRM3z)

# 🎓 Student Admission and Management System

A full-stack Laravel mini-project crafted for 5-hour developer assessment to evaluate real-world development proficiency in modern web application design.

---

## 🎯 Objective

To assess a candidate's capability in using Laravel to design and develop a production-ready application integrating modern backend, frontend, and DevOps practices.

---

## 📖 Project Description

This application allows administrators to manage student admissions, departments, courses, and document handling. Students can register, upload documents, and view their admission status. Admin users have the ability to manage courses, approve students, and view analytical charts with options for exports and reports.

---

## 🧩 Database Table Relationships (7 Core Tables)

| Table         | Relationships                                    |
|---------------|--------------------------------------------------|
| users         | One-to-Many → applications, documents            |
| roles         | Many-to-Many → users (via role_user pivot)       |
| students      | One-to-One with users, One-to-Many → documents   |
| departments   | One-to-Many → courses, students                  |
| courses       | Belongs to departments                           |
| applications  | Belongs to students and courses                  |
| documents     | Belongs to students                              |

---
## Table Queries

### 🧱 roles Table
```sql
CREATE TABLE roles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    description TEXT,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL
);
```
### 🧱 users Table
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    remember_token VARCHAR(100),
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL
);
```

### 🔁 role_user Pivot Table
```sql
CREATE TABLE role_user (
    role_id INT,
    user_id INT,
    PRIMARY KEY (role_id, user_id),
    FOREIGN KEY (role_id) REFERENCES roles(id) ON DELETE CASCADE,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```
### 🧱 departments Table
```sql
CREATE TABLE departments (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL
);
```

### 🧱 courses Table
```sql
CREATE TABLE courses (
    id INT AUTO_INCREMENT PRIMARY KEY,
    department_id INT,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL,
    FOREIGN KEY (department_id) REFERENCES departments(id) ON DELETE CASCADE
);
```

### 🧱 applications Table
```sql
CREATE TABLE applications (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    course_id INT,
    application_status ENUM('pending', 'approved', 'rejected') DEFAULT 'pending',
    submitted_at TIMESTAMP NULL,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL,
    FOREIGN KEY (student_id) REFERENCES students(id) ON DELETE CASCADE,
    FOREIGN KEY (course_id) REFERENCES courses(id) ON DELETE CASCADE
);
```

### 🧱 documents Table
```sql
CREATE TABLE documents (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id INT,
    user_id INT,
    document_type VARCHAR(50),
    file_path VARCHAR(255),
    uploaded_at TIMESTAMP NULL,
    created_at TIMESTAMP NULL,
    updated_at TIMESTAMP NULL,
    FOREIGN KEY (student_id) REFERENCES students(id) ON DELETE CASCADE,
    FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```
## 📦 Tech Stack

- **Backend**: Laravel 10, PHP 8+
- **Database**: MySQL
- **Frontend**: Blade, Tailwind CSS or Bootstrap
- **JS Libraries**: Alpine.js / jQuery / AJAX
- **Charting**: Chart.js / Laravel Charts
- **Exports**: DomPDF, Maatwebsite Excel
- **Security**: spatie/laravel-permission, Google reCAPTCHA
- **Other**: Livewire (optional), Laravel Echo, Pusher, Laravel Scout

---



## 🗃️ Project Folder Structure

```bash
/app
  /Http/Controllers
  /Models
  /Middleware
/config
/database
  /migrations
  /seeders
  /stored_procedures
/resources
  /views
  /js
  /css
/routes
  web.php, api.php
/public
  /uploads
/tests
  /Feature, /Unit

```

## ✅ Feature List with Assessment Task Breakdown

| Module                     | Tasks to Implement                                                                 |
|---------------------------|-------------------------------------------------------------------------------------|
|✅  Authentication            | Login, Registration, Laravel UI or Breeze, Role-based Access with Middleware       |
|✅ Role Management           | Admin, Student roles using spatie/laravel-permission                               |
|📤 File Upload               | Upload profile photo and document with preview, drag-and-drop support              |
| 📧 Email Integration         | Confirmation emails, notification emails                                           |
| 📥 PDF Viewer & Export       | View documents in browser, export report to PDF                                    |
| 📥 Excel Export              | Export student list and application list to Excel                                  |
| 📊 Dropdown Cascading        | Department → Course dynamic selection (AJAX)                                       |
| 📄 Charts & Analytics        | Students per department, Admissions per month, Course demand                       |
| 📜 Pagination & Search       | AJAX-based real-time search with pagination                                        |
| 📄 Captcha                   | Google reCAPTCHA for registration form                                             |
|  📄 Stored Procedures         | Use MySQL SP for calculating application stats                                     |
|⚙️ Session & Cookie Handling | Remember login, store temporary form values                                        |
| 📄 AJAX Modals               | Open edit/view forms in modal via AJAX                                             |
|📄  Print View                | Printable admission receipt or student report                                      |
| 📄 Queues & Jobs             | Email queue processing (optional)                                                  |
| 🛠️ CI/CD (Bonus)             | Setup GitHub Actions or GitLab CI for deployment                                  |
|🚀 REST API (Bonus)          | API for CRUD operations using Sanctum or Passport                                 |
|🧪 Unit Testing              | Write PHPUnit tests for 3 core modules                                             |

---

## 📈 Charts and Analytics (Chart.js / Laravel Charts)

- 📊 Number of students by department
- 📈 Admissions trend (monthly)
- 📌 Course popularity
- 📍 Gender distribution (Pie chart)

---

## 🛠️ Setup Instructions

```bash
git clone https://github.com/yourusername/student-admission-system.git
cd student-admission-system
composer install
cp .env.example .env
php artisan key:generate
php artisan migrate --seed
php artisan serve
```

## 🧪 Testing
```bash
php artisan test
```


## 🚀 Deliverables

- Code base with proper folder structure

- Seeder, migration, and stored procedure SQL files

- Screenshots of chart views, reports, exports

- Postman collection (if REST APIs implemented)

- README.md with project setup

