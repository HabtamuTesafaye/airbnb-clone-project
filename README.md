# 🏠 Airbnb Clone Project – Backend

## 📌 About the Project

The **Airbnb Clone Project** is a real-world, full-stack development challenge focused on building a scalable and secure backend system that mimics the core functionality of Airbnb. This project offers hands-on experience with API design, database modeling, and backend architecture. It also emphasizes modern development workflows, such as CI/CD integration and collaborative team dynamics.

## 🎯 Project Goals

* **User Management:** Secure registration, login, and profile updates.
* **Property Management:** CRUD operations for property listings.
* **Booking System:** Mechanism to book, update, and cancel stays.
* **Payment Processing:** Handle and record transactions securely.
* **Review System:** Post, edit, and view property reviews.
* **Performance:** Optimize API and database access for scalability.

---

## 👥 Team Roles

* **Backend Developer:** Builds API endpoints, business logic, and integrates third-party services.
* **Database Administrator (DBA):** Designs schemas, ensures normalization, and optimizes queries.
* **DevOps Engineer:** Manages deployments, containerization, and CI/CD pipelines.
* **QA Engineer:** Tests API functionality and performance, ensuring robust delivery.

---

## ⚙️ Technology Stack

| Technology                                                                 | Purpose                                                                |
| -------------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| [**Django**](https://www.djangoproject.com/)                               | Web framework for building robust APIs and admin tools.                |
| [**Django REST Framework**](https://www.django-rest-framework.org/)        | Handles RESTful API development.                                       |
| [**PostgreSQL**](https://www.postgresql.org/)                              | Relational database for storing structured data.                       |
| [**GraphQL**](https://graphql.org/)                                        | Flexible query language for retrieving and manipulating data.          |
| [**Celery**](https://docs.celeryq.dev/)                                    | Executes asynchronous tasks like sending emails or payment processing. |
| [**Redis**](https://redis.io/)                                             | Caching and queuing support for Celery.                                |
| [**Docker**](https://www.docker.com/)                                      | Containerization for development and deployment.                       |
| [**GitHub Actions**](https://docs.github.com/en/actions)                  | Automates testing and deployment with CI/CD pipelines.                 |


---

## 🧩 Database Design

| Entity         | Key Fields                                                        |
| -------------- | ----------------------------------------------------------------- |
| **Users**      | `id`, `email`, `password`, `full_name`, `is_host`                 |
| **Properties** | `id`, `title`, `location`, `price_per_night`, `user_id (FK)`      |
| **Bookings**   | `id`, `property_id (FK)`, `user_id (FK)`, `check_in`, `check_out` |
| **Reviews**    | `id`, `user_id (FK)`, `property_id (FK)`, `rating`, `comment`     |
| **Payments**   | `id`, `booking_id (FK)`, `amount`, `payment_status`, `timestamp`  |

**Relationships:**

* A **user** can own multiple **properties**.
* A **property** can have multiple **bookings** and **reviews**.
* A **booking** is linked to one **user**, one **property**, and one **payment**.
* A **review** is linked to one **user** and one **property**.

---

## 🚀 Feature Breakdown

* **User Management:** Allows secure sign-up, login, and profile management with token-based authentication.
* **Property Listings:** Hosts can list properties with details like price, location, and images.
* **Booking System:** Enables users to check availability and book properties with date validation.
* **Payment Integration:** Processes payments and stores transaction history securely.
* **Reviews:** Lets users provide feedback and ratings for properties they stayed at.
* **API Documentation:** Built using OpenAPI and GraphQL for interactive exploration.
* **Data Optimization:** Indexing and caching are used to enhance performance and scalability.

---

## 🔐 API Security

* **Authentication:** Token-based (JWT/session) authentication for all protected routes.
* **Authorization:** Role-based access control ensuring only owners can modify their content.
* **Rate Limiting:** Prevents abuse by throttling excessive API calls.
* **Input Validation:** Protects against injection attacks and malformed data.
* **Secure Payments:** Ensures encrypted transactions and storage of sensitive data.

Security is critical to:

* Protect **user data**.
* Prevent **unauthorized bookings or changes**.
* Ensure **safe financial transactions**.

---

## ⚙️ CI/CD Pipeline

* **What is CI/CD?**
  Continuous Integration and Continuous Deployment (CI/CD) automates testing and deployment of code, ensuring reliability and consistency.

* **Tools Used:**

  * **GitHub Actions:** Runs tests, lints code, and deploys on every push.
  * **Docker:** Ensures the environment is consistent across all stages.
  * **PostgreSQL + Redis Containers:** Used for automated test environments.

---

## 📚 API Documentation

### ✅ REST Endpoints

#### **Users**

* `GET /users/` – List all users
* `POST /users/` – Create a new user
* `GET /users/{id}/` – Retrieve user
* `PUT /users/{id}/` – Update user
* `DELETE /users/{id}/` – Delete user

#### **Properties**

* `GET /properties/` – List all properties
* `POST /properties/` – Create property
* `GET /properties/{id}/` – Retrieve property
* `PUT /properties/{id}/` – Update property
* `DELETE /properties/{id}/` – Delete property

#### **Bookings**

* `GET /bookings/` – List all bookings
* `POST /bookings/` – Create booking
* `GET /bookings/{id}/` – Retrieve booking
* `PUT /bookings/{id}/` – Update booking
* `DELETE /bookings/{id}/` – Delete booking

#### **Payments**

* `POST /payments/` – Process payment

#### **Reviews**

* `GET /reviews/` – List reviews
* `POST /reviews/` – Create review
* `GET /reviews/{id}/` – Retrieve review
* `PUT /reviews/{id}/` – Update review
* `DELETE /reviews/{id}/` – Delete review

---

## 📈 Learning Objectives

By completing this project, you will:

* Build and document secure RESTful and GraphQL APIs.
* Design relational databases optimized for real-world use cases.
* Apply CI/CD principles with automated testing and deployment.
* Collaborate using GitHub and follow structured project workflows.
* Deepen backend and DevOps skills through real-world feature implementation.

---

## 📁 Repository

* **GitHub Repo:** [airbnb-clone-project](https://github.com/HabtamuTesafaye/airbnb-clone-project)

---

Let me know if you'd like this broken into Markdown sections or if you want a version of it prefilled for direct copy-paste into your `README.md`.
