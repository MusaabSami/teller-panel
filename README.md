# Teller Panel

A full-stack web application built with React (Vite) and Express.js.

## Project Structure

```
├── frontend/          # React + Vite frontend
└── backend/           # Express.js backend
```

## Tech Stack

### Frontend
- React
- Vite
- Tailwind CSS
- Axios
- React Router DOM

### Backend
- Express.js
- MongoDB
- JWT Authentication
- Express Validator

## Getting Started

1. Clone the repository
```bash
git clone <repository-url>
cd teller-panel
```

2. Install dependencies
```bash
# Install frontend dependencies
cd frontend
npm install

# Install backend dependencies
cd ../backend
npm install
```

3. Set up environment variables
- Create `.env` in backend directory
- Create `.env` in frontend directory

4. Run the application
```bash
# Run frontend (in frontend directory)
npm run dev

# Run backend (in backend directory)
npm run dev
```

# Bank Teller Panel – Fullstack Deployment with Kubernetes

This project is a complete MERN stack web application for bank teller operations. It includes frontend (React + Vite), backend (Node.js + Express), and MongoDB, deployed using **Minikube** and **Docker**, with optional GitHub Actions CI/CD support.

---

## 📁 Project Structure

```
.
├── backend/                   # Express.js backend
├── frontend/                  # React frontend (Vite)
├── Dockerfile                 # Backend Dockerfile
├── deployment.yaml            # Backend Deployment
├── service.yaml               # Backend Service
├── Frontend-deployment.yaml  # Frontend Deployment
├── Frontend-service.yaml      # Frontend Service
├── mongo-deployment.yaml      # MongoDB Deployment
├── .github/workflows/         # GitHub Actions workflows
│   └── deploy.yml             # Backend deployment CI
│   └── frontend-deploy.yml    # Frontend deployment CI
└── README.md
```

---

## ⚙️ Local Kubernetes Setup (Minikube)

Make sure `minikube`, `kubectl`, and `docker` are installed.

```bash
minikube start
kubectl create namespace teller-panel
eval $(minikube docker-env)  # Use Minikube Docker
```

---

## 🚀 Manual Deployment Steps (Used for Submission)

Due to self-hosted runner queuing delays, manual deployment was used:

### 🖼️ Frontend

```bash
eval $(minikube docker-env -u)   # Reset to host Docker
docker build -t musaabsami/bms-frontend:latest ./frontend
docker push musaabsami/bms-frontend:latest
kubectl apply -f Frontend-deployment.yaml -n teller-panel
kubectl apply -f Frontend-service.yaml -n teller-panel
```

### 🔧 Backend

```bash
docker build -t musaabsami/bms-backend:latest .
docker push musaabsami/bms-backend:latest
kubectl apply -f deployment.yaml -n teller-panel
kubectl apply -f service.yaml -n teller-panel
```

### 🗄️ MongoDB

```bash
kubectl apply -f mongo-deployment.yaml -n teller-panel
```

---

## 🌐 Access the App

```bash
minikube service bms-frontend-service -n teller-panel
```

> Opens the app in browser, usually at `http://192.168.49.2:30008`

---

## 🧪 Health & Debugging

```bash
kubectl get pods -n teller-panel -o wide
kubectl get svc -n teller-panel
kubectl logs -n teller-panel -l app=bms-backend
```

---

## ⚙️ GitHub Actions CI/CD

> CI/CD is configured but not used for submission due to a runner delay. Workflows are defined and functional.

- `.github/workflows/deploy.yml` (Backend)
- `.github/workflows/frontend-deploy.yml` (Frontend)

---

## 👤 Author

- **Musaab Sami**
- Docker Hub: [musaabsami](https://hub.docker.com/u/musaabsami)
- GitHub: [MusaabSami](https://github.com/MusaabSami)

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](https://choosealicense.com/licenses/mit/)
