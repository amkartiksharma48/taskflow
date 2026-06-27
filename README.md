# TaskFlow — Full Stack Task Manager

A full-stack web application built with Node.js, Express, MongoDB, Docker, and deployed to AWS EC2 via a GitHub Actions CI/CD pipeline.

## Tech Stack

| Layer       | Technology              |
|-------------|-------------------------|
| Frontend    | HTML, CSS, JavaScript   |
| Backend     | Node.js + Express.js    |
| Database    | MongoDB Atlas           |
| Container   | Docker + docker-compose |
| CI/CD       | GitHub Actions          |
| Deployment  | AWS EC2                 |

## Project Structure

```
taskflow/
├── backend/
│   ├── models/
│   │   └── Task.js          # MongoDB schema
│   ├── routes/
│   │   └── tasks.js         # API endpoints
│   ├── server.js            # Main entry point
│   ├── package.json
│   ├── Dockerfile
│   └── .env.example
├── frontend/
│   ├── index.html           # UI (HTML + CSS + JS)
│   └── Dockerfile
├── .github/
│   └── workflows/
│       └── deploy.yml       # CI/CD pipeline
├── docker-compose.yml
└── .gitignore
```

## API Endpoints

| Method | Route             | Description       |
|--------|-------------------|-------------------|
| GET    | /api/tasks        | Get all tasks     |
| POST   | /api/tasks        | Create a task     |
| PUT    | /api/tasks/:id    | Update a task     |
| DELETE | /api/tasks/:id    | Delete a task     |

## Local Setup

### 1. Clone the repo
```bash
git clone https://github.com/yourusername/taskflow.git
cd taskflow
```

### 2. Set up environment variables
```bash
cp backend/.env.example backend/.env
# Edit .env and add your MongoDB Atlas URI
```

### 3. Run with Docker
```bash
docker-compose up --build
```

- Frontend: http://localhost:3000
- Backend API: http://localhost:5000

## CI/CD Pipeline

On every push to `main`, GitHub Actions automatically:
1. Builds Docker images for frontend and backend
2. Pushes images to Docker Hub
3. SSHs into AWS EC2 and deploys the latest containers

### GitHub Secrets Required

| Secret           | Value                        |
|------------------|------------------------------|
| DOCKER_USERNAME  | Your Docker Hub username     |
| DOCKER_PASSWORD  | Your Docker Hub password     |
| EC2_HOST         | Your EC2 public IP address   |
| EC2_USERNAME     | ubuntu                       |
| EC2_SSH_KEY      | Contents of your .pem file   |

## Deployment (AWS EC2)

1. Launch an EC2 instance (Ubuntu, t2.micro — free tier)
2. Install Docker and docker-compose on the instance
3. Clone the repo and create the `.env` file
4. Add GitHub Secrets (listed above)
5. Push to `main` — the pipeline handles the rest
