# Dockerized Two-Tier Flask Application with Kubernetes on AWS

A containerized two-tier web application built using **Python Flask, MySQL, Docker, Docker Compose, and Kubernetes**, with cloud deployment on AWS.

This project demonstrates application containerization, multi-container orchestration, database persistence, Kubernetes deployment, and cloud infrastructure management.

The application consists of two independent tiers:

- **Application Tier:** Python Flask application served using Gunicorn.
- **Database Tier:** MySQL database responsible for storing application data.

The application can be run using Docker Compose and deployed using Kubernetes manifests.

## Architecture

The project follows a two-tier architecture with separate application and database components.

### Application Architecture

```text
                  User
                   |
                   v
              AWS EC2
                   |
                   v
             Docker Network
                   |
          +--------+--------+
          |                 |
          v                 v
     Flask App           MySQL
     Container           Container
          |                 |
          +-----------------+
                            |
                            v
                      Docker Volume
                     Persistent Data
```

### Kubernetes Architecture

```text
                  User
                   |
                   v
             Kubernetes
                Cluster
                   |
                   v
             Application
                Service
                   |
                   v
           Flask Deployment
                   |
                   v
             MySQL Service
                   |
                   v
             MySQL Deployment
                   |
                   v
             Persistent Storage
```

*The Kubernetes architecture represents the intended application and database deployment topology. Actual ingress, service types, replicas and storage configuration depend on the deployed manifests.*

## Technology Stack

| Technology | Purpose |
|---|---|
| Python | Application development |
| Flask | Web application framework |
| MySQL | Relational database |
| Gunicorn | Production WSGI server |
| Docker | Application containerization |
| Docker Compose | Multi-container orchestration |
| Kubernetes | Container orchestration |
| kubectl | Kubernetes cluster management |
| AWS EC2 | Cloud deployment |
| AWS EKS | Managed Kubernetes, if used |
| Linux | Server environment |
| Git & GitHub | Version control |

## Project Structure

```text
two-tier-flask-app/
│
├── app.py
├── Dockerfile
├── Dockerfile.multistage
├── docker-compose.yml
├── requirements.txt
├── Makefile
├── .dockerignore
├── .env.example
│
├── tests/
│
├── jenkins/
│
├── kubernetes/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── configmap.yaml
│   ├── secret.yaml
│   └── storage.yaml
│
├── aws/
│
├── elastic-beanstalk/
│
└── README.md
```

*Update the Kubernetes filenames above to match the actual files in your repository.*

## Application Workflow

1. Users access the Flask web application.
2. Flask processes incoming HTTP requests.
3. The application communicates with MySQL through an internal service or Docker network.
4. MySQL stores application data using persistent storage.
5. Docker Compose manages the application and database containers during local deployment.
6. Kubernetes manages application workloads, services and storage during Kubernetes deployment.

## Key Features

- **Containerized application:** Flask and MySQL run in separate containers.
- **Multi-container orchestration:** Docker Compose manages application services.
- **Kubernetes deployment:** Kubernetes manifests define application and database workloads.
- **Persistent storage:** Docker volumes and Kubernetes persistent storage provide database data persistence.
- **Service communication:** Application and database communicate over internal networks.
- **Health checks:** Container health checks help monitor service readiness.
- **Production application server:** Gunicorn serves the Flask application.
- **Non-root execution:** Application container uses a non-root user.
- **Environment-based configuration:** Application and database settings are externally configurable.
- **Multi-stage Docker build:** An alternative Dockerfile demonstrates multi-stage image building.

## Docker Compose Deployment

### Prerequisites

- Docker Engine
- Docker Compose plugin
- Git

### 1. Clone the repository

```bash
git clone https://github.com/akhilesh-singh-official/two-tier-flask-app.git

cd two-tier-flask-app
```

### 2. Configure environment variables

```bash
cp .env.example .env
```

Update the database credentials in `.env`.

Never commit actual credentials to GitHub.

### 3. Build and start containers

```bash
docker compose up -d --build
```

### 4. Verify containers

```bash
docker compose ps
```

### 5. View logs

```bash
docker compose logs -f
```

### 6. Access the application

```text
http://localhost:5000
```

Use the application port configured in Docker Compose.

## Kubernetes Deployment

The project also includes Kubernetes configurations for deploying the application in a Kubernetes environment.

### Kubernetes Concepts

- **Deployments:** Manage application and database workloads.
- **Services:** Enable internal communication between application components.
- **ConfigMaps:** Manage non-sensitive application configuration.
- **Secrets:** Manage sensitive configuration.
- **Persistent Volumes and Claims:** Provide persistent database storage.

### Deployment Workflow

1. Build the Flask application Docker image.
2. Push the image to a container registry.
3. Configure Kubernetes manifests.
4. Apply the required Kubernetes resources.
5. Deploy application and database workloads.
6. Verify pods, deployments and services.
7. Access the application through the configured service or ingress.

### Useful Kubernetes Commands

```bash
# Check cluster connectivity
kubectl get nodes

# Apply Kubernetes configurations
kubectl apply -f kubernetes/

# Check pods
kubectl get pods

# Check deployments
kubectl get deployments

# Check services
kubectl get services

# Check persistent volume claims
kubectl get pvc

# View application logs
kubectl logs <pod-name>
```

*Apply resources in dependency order if your manifests require it. Adjust paths and commands to match your actual Kubernetes configuration.*

## AWS Deployment

The application can be deployed on AWS infrastructure.

### EC2 Deployment

1. Launch an EC2 Linux instance.
2. Configure security groups.
3. Install Docker and Docker Compose.
4. Clone the repository.
5. Configure application environment variables.
6. Build and run the application.
7. Access the application using the EC2 public address and configured port.

### EKS Deployment

If using Amazon EKS, the Kubernetes deployment can run on an AWS-managed Kubernetes control plane.

The deployment workflow includes:

1. Configure AWS CLI and cluster access.
2. Connect kubectl to the EKS cluster.
3. Push the application image to a container registry such as Amazon ECR.
4. Apply Kubernetes manifests.
5. Verify workloads and services.
6. Access the application through the configured exposure mechanism.

## Security Considerations

- Keep database services on private networks.
- Avoid exposing MySQL directly to the internet.
- Use environment variables or secure secret management.
- Run application containers as non-root users.
- Apply least-privilege access to AWS resources.
- Restrict inbound traffic through security groups.
- Scan container images for known vulnerabilities.
- Avoid committing `.env` files and credentials.

## What I Learned

Through this project, I gained practical experience with:

- Containerizing Python applications using Docker.
- Managing multi-container applications with Docker Compose.
- Understanding two-tier application architecture.
- Configuring Docker networking and persistent volumes.
- Deploying applications using Kubernetes.
- Managing Kubernetes workloads, services and storage.
- Running Flask applications using Gunicorn.
- Deploying containerized workloads on AWS.
- Understanding application configuration and container security.

## Author

**Akhilesh Singh**

DevOps | Cloud Infrastructure | Containerization

GitHub: [akhilesh-singh-official](https://github.com/akhilesh-singh-official)

---

*This project is part of my hands-on DevOps journey, focused on building, deploying, securing, and managing containerized applications using modern cloud and orchestration technologies.*
