This README explains the **key folders and their purposes** within the project.

---

##  Key Folders Overview

### 1. `app/`
This is the main application directory where all the Flask code lives.

####  `__init__.py`
- Initializes Flask app using application factory pattern.
- Registers routes, extensions, and configuration.

####  `config.py`
- Centralized app configuration (development, production, environment variables).

---

### 2. `app/models/`
Contains schema definitions for all data models using **MongoEngine** or **Pydantic** if you're using raw PyMongo.

- `user.py`: User profile, preferences, and linked wallet details.
- `transaction.py`: Tracks each UPI transaction, amount saved, and category.
- `goal_jar.py`: Stores virtual savings jar info like name, target, and deadline.
- `alert.py`: Tracks budget alerts, overspending warnings, etc.

---

### 3. `app/routes/`
REST API endpoints grouped by domain using **Flask Blueprints**.

- `auth.py`: Handles user registration, login, JWT authentication.
- `users.py`: Profile-related endpoints (update name, preferences).
- `transactions.py`: APIs to fetch or create UPI transaction records.
- `goals.py`: Create, update, or delete saving goals.
- `analytics.py`: APIs for AI-based insights, nudges, and overspending warnings.

---

### 4. `app/services/`
Core business logic and integrations live here.

- `savings_engine.py`: Logic for rounding transactions and allocating to jars.
- `budget_analyzer.py`: Manages monthly budget checks and triggers alerts.
- `notification_service.py`: Sends FCM/OneSignal notifications to users.
- `upi_integration.py`: (Future) Connect with UPI APIs for real-time transactions.

---

### 5. `app/ml/`
Home of all AI/ML-powered functionality.

- `categorizer.py`: NLP-based classifier to assign transaction categories.
- `overspend_predictor.py`: Time-series models to predict budget overruns.
- `recommender.py`: Suggests nudges, saving tips, or challenges based on habits.
- `train/`: Contains dummy data and training scripts for local/offline model building.

---

### 6. `app/tasks/`
Background jobs powered by **Celery**.

- `scheduler.py`: Periodic tasks (e.g., daily budget checks).
- `task_runner.py`: Triggers savings events or reminders in background.

---

### 7. `app/utils/`
Helper functions and reusable utilities.

- `auth_utils.py`: JWT decode, token validation, role checks.
- `rounding.py`: Functions for custom rounding logic (₹1/₹10/₹50).
- `enums.py`: Enum classes for transaction categories, alert types.
- `logger.py`: Centralized logging for events and errors.

---

### 8. `app/extensions.py`
Centralized initialization for Flask extensions:
- MongoDB (`PyMongo` or `MongoEngine`)
- JWT Authentication
- CORS setup
- Celery (if used)

---

##  `tests/`
Unit and integration test cases organized per module.
- Test cases for routes, services, and AI modules using `pytest` or `unittest`.

---

##  Docker & Deployment Files
- `Dockerfile`: Container image definition for the Flask app.
- `docker-compose.yml`: Launches Flask + MongoDB + Redis (for Celery).

---

##  migrations/ (Optional)
- For database migration handling (e.g., MongoEngine upgrades or fixtures).

---

##  Recommended Next Steps

- Start Flask app using `run.py`
- Set up MongoDB (local or Atlas)
- Train AI models using mock data under `app/ml/train/`
- Add API documentation (Swagger/Postman)
- Start frontend SDK or mobile integration

