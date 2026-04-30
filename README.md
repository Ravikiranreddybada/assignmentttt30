# Lab 27: Full-Stack MERN Application

A professional full-stack application demonstrating modern web development practices, including microservices architecture, Docker containerization, and automated CI/CD pipelines with Jenkins.

## 🚀 Overview

This project consists of a React-based frontend and a Node.js/Express backend, designed to showcase advanced database relationships (One-to-Many and Many-to-Many) using MongoDB Atlas.

### Key Features
- **User Management**: Complete CRUD operations for user profiles.
- **Advanced Relationships**:
  - **One-to-Many**: Users can have multiple posts.
  - **Many-to-Many**: Students can enroll in multiple courses, and courses can have multiple students.
- **Dockerized Environment**: Fully containerized using Docker and Docker Compose for consistent development and deployment.
- **CI/CD Pipeline**: Automated build, test, and containerization using Jenkins.

---

## 🛠 Tech Stack

### Frontend
- **Framework**: React.js
- **Styling**: CSS3
- **HTTP Client**: Axios

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MongoDB Atlas (Cloud)
- **ODM**: Mongoose

### DevOps & Infrastructure
- **Containerization**: Docker, Docker Compose
- **CI/CD**: Jenkins (with custom Docker-in-Docker agent)
- **Version Control**: Git / GitHub

---

## 📦 Project Structure

```text
.
├── backend/            # Express API service
│   ├── models/         # Mongoose schemas (User, Post, Student, Course)
│   ├── routes/         # API endpoints
│   └── Dockerfile      # Backend container config
├── frontend/           # React application
│   ├── src/            # Components and logic
│   └── Dockerfile      # Frontend container config
├── jenkins/            # CI/CD Infrastructure
│   ├── Dockerfile      # Custom Jenkins image (Node + Docker CLI)
│   └── docker-compose  # Jenkins instance setup
├── Jenkinsfile         # CI/CD Pipeline definition
└── docker-compose.yml  # Root orchestration for app services
```

---

## 🚦 Getting Started

### Prerequisites
- [Docker Desktop](https://www.docker.com/products/docker-desktop/)
- [Node.js](https://nodejs.org/) (optional, for local development)

### Local Development (Docker)
The easiest way to run the entire stack is using Docker Compose:

1. **Clone the repository**:
   ```bash
   git clone https://github.com/Ravikiranreddybada/assignmentttt30.git
   cd assignmentttt30
   ```

2. **Run the application**:
   ```bash
   docker-compose up --build
   ```
   - Frontend: [http://localhost:3001](http://localhost:3001)
   - Backend API: [http://localhost:5001](http://localhost:5001)

---

## ⚙️ CI/CD with Jenkins

This project includes a fully configured Jenkins pipeline.

1. **Start Jenkins**:
   ```bash
   cd jenkins
   docker-compose up -d
   ```
2. **Access Jenkins**: Navigate to `http://localhost:8080`.
3. **Pipeline Stages**:
   - `Install Dependencies`: Runs `npm install` for all modules.
   - `Test`: Executes unit tests.
   - `Build Frontend`: Generates production assets.
   - `Docker Build`: Builds and tags images for production deployment.

---

## 🔗 API Endpoints

| Method | Endpoint | Description |
|:--- |:--- |:--- |
| `GET` | `/api/user` | Fetch all users |
| `POST` | `/api/user` | Create a new user |
| `POST` | `/api/enroll` | Enroll a student in a course (Many-to-Many) |
| `GET` | `/api/post` | Fetch posts with populated user data |

---

## 📄 License
This project is for educational purposes as part of Lab 27.
