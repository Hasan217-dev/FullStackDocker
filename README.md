# 🚀 Full Stack Docker

A modern, production-ready full-stack application with containerized frontend, backend, and PostgreSQL database orchestrated using Docker Compose. Built for seamless development and deployment with isolated microservices architecture.

## ✨ Features

- **🐳 Docker Containerization** - Frontend, backend, and database in isolated containers
- **🔗 Docker Compose Orchestration** - Multi-container orchestration with service dependencies
- **⚡ Modern Stack** - Node.js backend, React/Vite frontend, PostgreSQL database
- **🌉 Bridge Network** - Custom Docker network for inter-service communication
- **📊 PostgreSQL Database** - Alpine Linux-based PostgreSQL 16 for data persistence
- **🔄 Auto Restart** - Database service configured for automatic restart on failure
- **📦 Volume Persistence** - Persistent PostgreSQL data storage with Docker volumes
- **🎯 Environment Isolation** - Pre-configured environment variables for database connectivity

## 🏗️ Project Structure

```
FullStackDocker/
├── frontend/                 # React + Vite frontend application
│   ├── Dockerfile           # Frontend container configuration
│   ├── src/                 # React source code
│   ├── public/              # Static assets
│   └── package.json         # Frontend dependencies
├── backend/                 # Node.js backend API
│   ├── Dockerfile           # Backend container configuration
│   ├── index.js             # Express server entry point
│   └── package.json         # Backend dependencies
├── docker-compose.yml       # Multi-container orchestration config
└── README.md                # This file
```

## 🎯 Services

### Frontend Service
- **Port**: 3000 (mapped to container port 80)
- **Build**: Dockerfile in `./frontend`
- **Dependencies**: Requires backend service to be running

### Backend Service
- **Port**: 5001 (mapped to container port 5000)
- **Build**: Dockerfile in `./backend`
- **Environment Variables**:
  - `DB_HOST: database`
  - `DB_USER: postgres`
  - `DB_PASS: password`
  - `DB_NAME: postgres`
- **Dependencies**: Requires database service to be running

### Database Service
- **Image**: PostgreSQL 16 Alpine (lightweight)
- **Port**: 5432 (internal only)
- **Restart Policy**: Always restart on failure
- **Credentials**:
  - User: `postgres`
  - Password: `password`
  - Database: `postgres`
- **Volume**: `pgdata` for persistent storage

## 🚀 Getting Started

### Prerequisites
- Docker Desktop installed and running
- Git installed on your machine

### Installation & Deployment

1. **Clone the repository**
   ```bash
   git clone https://github.com/Hasan217-dev/FullStackDocker.git
   cd FullStackDocker
   ```

2. **Build and start all services**
   ```bash
   docker-compose up --build
   ```
   This command will:
   - Build the frontend image
   - Build the backend image
   - Pull the PostgreSQL image
   - Start all three services
   - Establish network connectivity

3. **Access the application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5001
   - Database: localhost:5432

### Common Commands

**Start services** (without rebuilding)
```bash
docker-compose up
```

**Start services in background**
```bash
docker-compose up -d
```

**Stop all services**
```bash
docker-compose down
```

**Stop and remove volumes** (WARNING: deletes database data)
```bash
docker-compose down -v
```

**View logs**
```bash
docker-compose logs -f              # All services
docker-compose logs -f backend      # Specific service
docker-compose logs -f database     # Database logs
```

**Rebuild images**
```bash
docker-compose build --no-cache
```

**Execute commands in running container**
```bash
docker-compose exec backend npm install
docker-compose exec database psql -U postgres
```

## 🔧 Configuration

### Database Connection (Backend)
The backend connects to the database using these environment variables:
```
DB_HOST=database        # Service name in docker-compose.yml
DB_USER=postgres        # PostgreSQL username
DB_PASS=password        # PostgreSQL password
DB_NAME=postgres        # Database name
```

### Network
All services communicate over a custom bridge network named `my-custom-network`, ensuring:
- Service-to-service communication by service name
- Isolation from other Docker containers
- Network security and control

### Volumes
- `pgdata`: Stores PostgreSQL data for persistence across container restarts

## 📝 Development

### Frontend Development
```bash
docker-compose exec frontend npm run dev
```

### Backend Development
```bash
docker-compose exec backend npm install
docker-compose exec backend npm start
```

### Database Access
```bash
docker-compose exec database psql -U postgres -d postgres
```

## 🐛 Troubleshooting

**Port already in use**
```bash
# Change ports in docker-compose.yml
# frontend: "3001:80"
# backend: "5002:5000"
```

**Database connection refused**
- Ensure database service is running: `docker-compose ps`
- Check logs: `docker-compose logs database`
- Wait for PostgreSQL to be ready (usually takes 2-3 seconds)

**Images not rebuilding**
```bash
docker-compose build --no-cache
```

**Clear everything and start fresh**
```bash
docker-compose down -v
docker system prune -a
docker-compose up --build
```

## 📦 Technology Stack

- **Frontend**: React, Vite, Node.js
- **Backend**: Node.js, Express.js
- **Database**: PostgreSQL 16 (Alpine)
- **Containerization**: Docker & Docker Compose
- **Networking**: Docker Bridge Network

## 🔐 Security Notes

⚠️ **Development Only**: Default credentials in `docker-compose.yml` are for development use only.

For production deployment:
- Use strong, unique passwords
- Store secrets in environment files or secret management systems
- Never commit sensitive data to git
- Use `.env` files with `.gitignore`
- Enable SSL/TLS encryption
- Implement proper authentication and authorization

## 📄 License

This project is open source and available under the MIT License.

## 👤 Author

**Hasan Nawaz** - Full Stack Developer
- GitHub: [@Hasan217-dev](https://github.com/Hasan217-dev)
- Portfolio: Full Stack Development | MERN | Next.js | TypeScript | Docker

## 🤝 Contributing

Contributions are welcome! Feel free to fork this repository and submit pull requests for any improvements.

## 📧 Support

For issues, questions, or suggestions, please open an issue on GitHub or contact the author.

---

**Happy coding! 🎉** Let's build amazing things with Docker.
