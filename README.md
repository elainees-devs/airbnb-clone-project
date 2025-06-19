# 🏡 Airbnb Clone - Backend

## 🚀 Overview

The **Airbnb Clone Backend** provides a robust and scalable foundation for managing core features of an online rental platform, including user interactions, property listings, bookings, and payment processing. Built with Django and GraphQL, this backend ensures smooth operations for users and hosts alike.

---

## 🎯 Objective

The backend is designed to:
- Handle user registration, authentication, and profile management.
- Manage property listings and details.
- Enable users to book stays and manage reservations.
- Process payments securely.
- Support user reviews and ratings.
- Optimize performance with indexing and caching.

---

## 🏆 Project Goals

- **User Management**: Secure registration, authentication, and user profile handling.
- **Property Management**: Listing creation, updates, and deletion.
- **Booking System**: Reservation functionality with check-in/out handling.
- **Payment Processing**: Secure transaction handling.
- **Review System**: User-generated feedback for properties.
- **Data Optimization**: Fast retrieval via indexing and caching.

---

## 🛠️ Features Overview

### 1. API Documentation
- **OpenAPI Standard**: Clear and standardized documentation for REST APIs.
- **Django REST Framework**: Robust and scalable RESTful APIs.
- **GraphQL**: Flexible querying and data retrieval.

### 2. User Authentication
- **Endpoints**: `/users/`, `/users/{user_id}/`
- **Features**: User registration, login, profile management.

### 3. Property Management
- **Endpoints**: `/properties/`, `/properties/{property_id}/`
- **Features**: CRUD operations for property listings.

### 4. Booking System
- **Endpoints**: `/bookings/`, `/bookings/{booking_id}/`
- **Features**: Manage bookings and check-in/check-out details.

### 5. Payment Processing
- **Endpoints**: `/payments/`
- **Features**: Handle payments and transaction records.

### 6. Review System
- **Endpoints**: `/reviews/`, `/reviews/{review_id}/`
- **Features**: Add, edit, and delete reviews and ratings.

### 7. Database Optimizations
- **Indexing**: For efficient querying of high-demand data.
- **Caching**: Reduces database load and boosts performance.

---

## ⚙️ Technology Stack

| Tech               | Role                                      |
|--------------------|-------------------------------------------|
| Django             | Web framework for backend logic           |
| Django REST Framework | API management for REST endpoints     |
| GraphQL            | Flexible and efficient data queries       |
| PostgreSQL         | Relational database for persistent storage|
| Celery             | Task queue for async operations           |
| Redis              | Caching and session management            |
| Docker             | Containerized development & deployment    |
| CI/CD Pipelines    | Automated testing and deployment          |

---

## 📦 Database Design

The database schema is designed to support the core entities of the platform with clear relationships that reflect real-world interactions between users, properties, bookings, reviews, and payments.

### 🔑 Key Entities & Relationships

#### 1. **User**

* `id`: Unique identifier (UUID)
* `username`: Unique display name
* `email`: Unique contact email
* `password`: Hashed password
* `is_host`: Boolean flag to identify hosts

🔗 **Relationships**:

* A user **can own multiple** properties (if `is_host`).
* A user **can make multiple** bookings.
* A user **can leave** multiple reviews.

---

#### 2. **Property**

* `id`: Unique identifier
* `title`: Name of the listing
* `description`: Detailed information
* `location`: Address or coordinates
* `price_per_night`: Rental price

🔗 **Relationships**:

* A property **belongs to one** user (host).
* A property **can have multiple** bookings.
* A property **can have multiple** reviews.

---

#### 3. **Booking**

* `id`: Unique identifier
* `user_id`: Reference to the guest (User)
* `property_id`: Reference to the property
* `check_in`: Start date of stay
* `check_out`: End date of stay

🔗 **Relationships**:

* A booking **belongs to one** user (guest).
* A booking **belongs to one** property.
* A booking **can have one** payment.

---

#### 4. **Review**

* `id`: Unique identifier
* `user_id`: Reference to the reviewer
* `property_id`: Reference to the reviewed property
* `rating`: Numerical rating (e.g., 1-5)
* `comment`: Optional text review

🔗 **Relationships**:

* A review **belongs to one** user.
* A review **belongs to one** property.

---

#### 5. **Payment**

* `id`: Unique identifier
* `booking_id`: Reference to the related booking
* `amount`: Total paid
* `status`: e.g., `pending`, `completed`, `failed`
* `payment_method`: e.g., card, wallet

🔗 **Relationships**:

* A payment **is linked to one** booking.
* A payment **is initiated by one** user indirectly through the booking.

---

This design promotes data integrity, supports scalability, and ensures smooth querying across user activities, property availability, and transaction history.

---


## 👥 Team Roles

- **Backend Developer**: API, logic, schema design
- **Database Administrator**: DB design and optimization
- **DevOps Engineer**: Deployment and scaling
- **QA Engineer**: Functional and integration testing

---

## 📈 API Documentation Overview

### REST API
- Detailed using **OpenAPI**.
- Covers core modules: Users, Properties, Bookings, Payments, Reviews.

### GraphQL API
- Offers advanced querying capability with less overhead.

---

## 📌 Endpoints Overview

### 👤 Users
- `GET /users/` – List users  
- `POST /users/` – Create user  
- `GET /users/{user_id}/` – Get user details  
- `PUT /users/{user_id}/` – Update user  
- `DELETE /users/{user_id}/` – Delete user  

### 🏠 Properties
- `GET /properties/` – List properties  
- `POST /properties/` – Add property  
- `GET /properties/{property_id}/` – Get property  
- `PUT /properties/{property_id}/` – Update property  
- `DELETE /properties/{property_id}/` – Delete property  

### 📆 Bookings
- `GET /bookings/` – List bookings  
- `POST /bookings/` – Create booking  
- `GET /bookings/{booking_id}/` – Get booking  
- `PUT /bookings/{booking_id}/` – Update booking  
- `DELETE /bookings/{booking_id}/` – Cancel booking  

### 💳 Payments
- `POST /payments/` – Process payment  

### 🌟 Reviews
- `GET /reviews/` – List reviews  
- `POST /reviews/` – Add review  
- `GET /reviews/{review_id}/` – Get review  
- `PUT /reviews/{review_id}/` – Update review  
- `DELETE /reviews/{review_id}/` – Delete review  

---

## 🔒 API Security

Securing the backend APIs is critical to protecting both user data and platform integrity. Below are the key security measures implemented:

### Key Measures
- **Authentication**: Only verified users can access protected endpoints using token-based authentication (e.g., JWT).
- **Authorization**: Role-based access controls ensure that only users with the right permissions (e.g., host, admin) can perform specific actions.
- **Rate Limiting**: Prevents abuse and brute-force attacks by limiting the number of requests from a single IP or user in a given time frame.
- **Input Validation & Sanitization**: Prevents injection attacks (e.g., SQL, XSS).
- **HTTPS Enforcement**: Ensures all data exchanged between client and server is encrypted.
- **Secure Payment Handling**: Payment endpoints are isolated and integrated with trusted providers, with sensitive transaction data never stored in plain text.

### Why It Matters
- **User Data Protection**: Prevents unauthorized access to personal and sensitive user information.
- **Transaction Security**: Secures financial data during booking and payment operations.
- **System Integrity**: Protects backend systems from malicious activity and downtime.
- **Trust and Compliance**: Maintains platform credibility and helps meet data protection regulations.

---

## 🔁 CI/CD Pipeline

Continuous Integration and Continuous Deployment (CI/CD) streamline the development lifecycle by automating testing, building, and deploying code.

### Why CI/CD is Important
- **Faster Development**: Automates code integration and testing.
- **Reduced Errors**: Catches bugs early in the development process.
- **Consistent Deployments**: Ensures the same environment is used every time.
- **Improved Collaboration**: Enables team members to work on features independently without integration conflicts.

### Tools Used
- **GitHub Actions**: Automates testing and deployment workflows.
- **Docker**: Provides consistent environments for development, testing, and production.
- **Docker Compose**: Manages multi-container environments easily.
- **CI/CD Scripts**: Custom bash or YAML scripts to run builds, migrations, and tests.

---

## 🧪 Manual Review

The project is regularly subjected to **manual code and feature reviews** to ensure:

- **Security Compliance**: All endpoints and sensitive operations are double-checked.
- **Functional Integrity**: Features are manually tested against requirements.
- **Code Quality**: Developers verify that the code follows project standards.
- **Documentation Accuracy**: README and API documentation reflect the current state of the codebase.

Manual reviews are essential in addition to automated testing to catch issues related to user experience, unclear documentation, or edge cases that tools might miss.

---


