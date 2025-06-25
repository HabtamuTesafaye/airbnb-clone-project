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

| **Entity**             | **Key Fields**                                                     | **Description / Why it’s Needed**                                                                                                          |
|-----------------------|-------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **users**             | `id`, `email`, `password`, `full_name`, `is_host`                | Stores all users including guests and hosts. `is_host` marks if a user can list properties. Passwords should be hashed securely.           |
| **properties**        | `id`, `title`, `location`, `price_per_night`, `user_id (FK)`     | Represents property listings owned by hosts. Stores essential info like price and location. Linked to the owner via `user_id`.             |
| **bookings**          | `id`, `property_id (FK)`, `user_id (FK)`, `check_in`, `check_out`, `status` | Stores reservations made by users for properties. The `status` tracks booking progress (pending, confirmed, cancelled).                    |
| **payments**          | `id`, `booking_id (FK)`, `amount`, `payment_status`, `transaction_reference`, `payment_method`, `timestamp` | Records payments linked to bookings. Stores method, status, and transaction info for auditing and refund handling.                         |
| **reviews**           | `id`, `user_id (FK)`, `property_id (FK)`, `rating`, `comment`, `created_at`, `updated_at` | Allows users to leave feedback on properties they stayed in. Enforces one review per user per property.                                    |
| **property_images**   | `id`, `property_id (FK)`, `image_url`, `is_primary`              | Stores multiple images per property. `is_primary` indicates the main display image.                                                        |
| **amenities**         | `id`, `name`                                                     | List of possible amenities like "WiFi", "Pool". Used for filtering and search.                                                             |
| **property_amenities**| `property_id (FK)`, `amenity_id (FK)`                            | Many-to-many relationship linking properties to amenities they offer.                                                                      |
| **property_calendar** | `id`, `property_id (FK)`, `available_date`, `is_available`       | Tracks daily availability of properties for accurate booking and avoiding double-booking.                                                  |
| **booking_status_log**| `id`, `booking_id (FK)`, `status`, `updated_at`                   | Logs every status change on bookings, useful for audit trails and debugging.                                                               |
| **messages**          | `id`, `sender_id (FK)`, `receiver_id (FK)`, `content`, `sent_at` | Enables in-app communication between users (hosts and guests). Optional but improves user experience.                                       |
| **notifications**     | `id`, `user_id (FK)`, `message`, `is_read`, `created_at`          | Stores user notifications for events like booking confirmation, messages, or payment status.                                               |

---

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

### Users
| Endpoint            | Method | Purpose                                                      |
|---------------------|--------|--------------------------------------------------------------|
| `/users/`           | GET    | Retrieve a list of all users (for admin or internal use).    |
| `/users/`           | POST   | Register a new user with email and password.                 |
| `/users/{id}/`      | GET    | Retrieve a specific user profile (public or self).           |
| `/users/{id}/`      | PUT    | Update user info like name, password (secured).              |
| `/users/{id}/`      | DELETE | Delete user account (usually soft-delete in production).     |

### Properties
| Endpoint              | Method | Purpose                                              |
|-----------------------|--------|------------------------------------------------------|
| `/properties/`        | GET    | List all available properties (with filters).        |
| `/properties/`        | POST   | Host creates a new property listing.                  |
| `/properties/{id}/`   | GET    | Get detailed info about a specific property.          |
| `/properties/{id}/`   | PUT    | Update property details (only by the owner).          |
| `/properties/{id}/`   | DELETE | Delete property listing (only by the owner).          |

### Bookings
| Endpoint              | Method | Purpose                                              |
|-----------------------|--------|------------------------------------------------------|
| `/bookings/`          | GET    | List all bookings of the current user or admin.      |
| `/bookings/`          | POST   | Create a new booking (check availability & validate).|
| `/bookings/{id}/`     | GET    | Retrieve details of a specific booking.               |
| `/bookings/{id}/`     | PUT    | Update booking status (cancel, confirm) by authorized users. |
| `/bookings/{id}/`     | DELETE | Cancel or remove booking (depending on business logic).|

### Payments
| Endpoint              | Method | Purpose                                              |
|-----------------------|--------|------------------------------------------------------|
| `/payments/`          | POST   | Process a payment for a booking.                      |
| `/payments/{id}/`     | GET    | Retrieve payment details or transaction history.     |

### Reviews
| Endpoint              | Method | Purpose                                              |
|-----------------------|--------|------------------------------------------------------|
| `/reviews/`           | GET    | List reviews for properties (optionally filtered).   |
| `/reviews/`           | POST   | Create a new review for a property.                   |
| `/reviews/{id}/`      | GET    | Retrieve a specific review.                           |
| `/reviews/{id}/`      | PUT    | Update own review.                                    |
| `/reviews/{id}/`      | DELETE | Delete own review.                                    |

### Property Images (optional, usually part of property endpoints)
| Endpoint              | Method | Purpose                                              |
|-----------------------|--------|------------------------------------------------------|
| `/properties/{id}/images/` | GET    | List images of a property.                             |
| `/properties/{id}/images/` | POST   | Upload new image for property (owner only).           |
| `/properties/images/{image_id}/` | DELETE | Delete an image (owner only).                           |

### Messages (optional)
| Endpoint              | Method | Purpose                                              |
|-----------------------|--------|------------------------------------------------------|
| `/messages/`          | GET    | List all messages involving current user.            |
| `/messages/`          | POST   | Send a new message.                                   |

### Notifications (optional)
| Endpoint              | Method | Purpose                                              |
|-----------------------|--------|------------------------------------------------------|
| `/notifications/`     | GET    | List notifications for current user.                  |
| `/notifications/{id}/`| PUT    | Mark notification as read.                            |

---
---

## 👤 Author

**Habtamu Tesfaye**

* Full stack developer
* GitHub: [HabtamuTesafaye](https://github.com/HabtamuTesafaye)  
* LinkedIn: [linkedin.com/in/habtamu-tesfaye](https://linkedin.com/in/habtamu-tesfaye-4285551b5)  
* Email: habtamu.t.bekele.com  

---

## 📁 Repository

* **GitHub Repo:** [airbnb-clone-project](https://github.com/HabtamuTesafaye/airbnb-clone-project)

---
