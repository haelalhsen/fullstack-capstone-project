# GiftLink Application

## Project Overview

**GiftLink** is a full-stack web application designed to connect users who wish to give away household items they no longer need with users who prefer to find free items for recycling or upcycling purposes. This platform supports a circular economy, reducing waste and providing an environmentally friendly alternative to purchasing new products.

The application utilizes a microservices architecture, separating the frontend, backend, and sentiment analysis services. It features secure authentication, robust search capabilities, and automated deployment pipelines.

## Table of Contents

- [Key Features](#key-features)
- [Architecture & Tech Stack](#architecture--tech-stack)
- [Directory Structure](#directory-structure)
- [Setup & Installation](#setup--installation)
- [API Documentation](#api-documentation)
- [Frontend Components](#frontend-components)
- [DevOps & Deployment](#devops--deployment)

---

## Key Features

- **User Authentication:** Secure Registration, Login, and Profile Management using JWT.

- **Gift Listings:** Users can browse all available gifts with images and timestamps.

- **Advanced Search:** Filter gifts by name, category, condition, and age.

- **Item Details:** A protected view for logged-in users to see full details and user comments.

- **Sentiment Analysis:** An integrated AI microservice analyzes user comments to determine if they are positive, negative, or neutral.

---

## Architecture & Tech Stack

The application relies on a **Full-Stack JavaScript** environment.

### Frontend

- **Framework:** React.

- **Styling:** CSS, HTML.

- **State Management:** React Context/State for auth tokens and form inputs.

### Backend

- **Server:** Node.js with Express.

- **Database:** MongoDB (NoSQL).

- **Libraries:** `natural` (Sentiment Analysis), `axios` (HTTP requests), `jsonwebtoken` (Auth).

### Infrastructure

- **Containerization:** Docker.
- **Orchestration:** Kubernetes (Backend & DB), IBM Cloud Code Engine (Frontend) .

- **CI/CD:** GitHub Actions (Linting & Building).

---

## Directory Structure

The repository follows a clear separation of concerns:

- `giftlink-backend/`: Contains models, routes, and API logic.
- `giftlink-frontend/`: Contains the React application, components, and pages.
- `giftlink-backend/models`: Mongoose schemas.
- `giftlink-backend/routes`: API route definitions (`authRoutes.js`, `giftRoutes.js`, `searchRoutes.js`).

---

## Setup & Installation

### Prerequisites

- Node.js and npm installed.
- MongoDB installed and running locally or via cloud.

### 1. Database Setup

1. Initialize your MongoDB instance. **Important:** Note the password generated during startup.

2. Import the provided sample data (`json` file) into your MongoDB instance.

### 2. Environment Configuration

1. Locate the `env.sample` file in the backend directory.

2. Create a copy named `.env`.
3. Update the `MONGO_URL` and password credentials to match your database instance.

4. Set your JWT secret key in the `.env` file for authentication.

### 3. Installation

```bash
# Clone the repository
git clone <repo-url>

# Install Backend Dependencies
cd giftlink-backend
npm install

# Install Frontend Dependencies
cd ../giftlink-frontend
npm install

```

---

## API Documentation

### Authentication API

Handles user access and profile management.

| Method | Endpoint             | Description                                  |
| ------ | -------------------- | -------------------------------------------- |
| `POST` | `/api/auth/register` | Registers a new user and returns a token.    |
| `POST` | `/api/auth/login`    | Authenticates a user and returns a token.    |
| `PUT`  | `/api/auth/update`   | Updates user profile details (requires JWT). |

### Gifts & Search API

Manages the retrieval of item data.

| Method | Endpoint         | Description                                                 |
| ------ | ---------------- | ----------------------------------------------------------- |
| `GET`  | `/api/gifts`     | Retrieves a list of all available gifts.                    |
| `GET`  | `/api/gifts/:id` | Retrieves a specific gift by ID.                            |
| `GET`  | `/api/search`    | Filters gifts by `name`, `category`, `condition`, or `age`. |

### Sentiment Service

A dedicated microservice for text analysis.

| Method | Endpoint     | Description                                                     |
| ------ | ------------ | --------------------------------------------------------------- |
| `POST` | `/sentiment` | payload: `{ sentence: "string" }` - Returns sentiment analysis. |

---

## Frontend Components

The React application is structured into several key pages and components:

1.  **Landing Page:** The entry point (`home.html`/`css`) featuring an inspirational quote and a "Get Started" button .

2.  **Main Page:** Displays the grid of all gifts with images, names, and posting dates . Includes the global `Navbar`.

3.  **Authentication Pages:**

- **Login & Register:** Forms handling user input (name, email, password) and session storage for tokens.

4. **Details Page (Protected):** Accessible only to logged-in users. Displays full item details and user comments.

5. **Search Page:** Allows users to input text or select attributes (age, condition) to query the database.

6. **Profile Page:** Allows users to view and edit their registration details (e.g., name).

---

## DevOps & Deployment

### CI/CD Pipeline

The project uses **GitHub Actions** for Continuous Integration.

- **Workflow:** Triggers on push to the `main` branch.

- **Jobs:**

1.  `lint js`: Checks JavaScript files for syntax errors and coding style.

2.  `client build`: Builds the frontend client to ensure no compilation errors.

### Containerization & Cloud Deployment

The application is deployed using a microservices pattern:

1.  **MongoDB:** Containerized and deployed on **Kubernetes**.

2.  **Backend Service:** Containerized, configured with environment variables to point to the K8s MongoDB, and deployed on **Kubernetes**.

3.  **Frontend Service:** Containerized, configured to communicate with the Backend K8s service, and deployed on **IBM Cloud Code Engine**.
