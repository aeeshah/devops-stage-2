# Full-Stack FastAPI and React Template

Welcome to the Full-Stack FastAPI and React template repository. This repository serves as a demonstration application for interns, showcasing how to configure and run a full-stack application using a FastAPI backend and a ReactJS frontend with ChakraUI.

## Project Structure

The repository is divided into two primary directories:

- **frontend**: Contains the ReactJS application.
- **backend**: Contains the FastAPI application and PostgreSQL database integration.

Each directory includes a README file with detailed instructions for setting up and running the respective parts of the application locally on your server without containers. To run the complete full-stack application using Docker Compose, follow the instructions in this README file.

## Prerequisites

- Docker
- Docker Compose

## Getting Started

To run this application locally, please follow the instructions provided in the respective directories:

- [Frontend README](./frontend/README.md)
- [Backend README](./backend/README.md)

This repository offers a comprehensive full-stack setup using Docker Compose. The application includes a FastAPI backend, a ReactJS frontend, a PostgreSQL database, an Adminer database management tool, an Nginx Proxy Manager, and an Nginx web server.

## Services

- **backend**: FastAPI application providing the backend API.
- **frontend**: ReactJS application serving the frontend.
- **db**: PostgreSQL database for storing application data.
- **adminer**: Database management tool for interacting with the PostgreSQL database.
- **proxy**: Nginx Proxy Manager for handling SSL certificates and domain management.
- **nginx**: Nginx web server for serving the frontend and reverse proxying requests to the backend.

## Setup Instructions

1. Clone the repository:

    ```bash
    git clone https://github.com/aeesha/devops-stage-2
    cd devops-stage-2
    ```

2. Build and start the services:

    ```bash
    docker compose up -d #-d to avoid logs on terminal
    ```

3. Verify that the services are running:

    - FastAPI Backend: [http://localhost/api](http://localhost/api)
    - FastAPI Backend: [http://localhost/docs](http://localhost/docs)
    - FastAPI Backend: [http://localhost/redoc](http://localhost/api)
    - ReactJS Frontend: [http://localhost](http://localhost)
    - PostgreSQL Database: Accessible on port 5432 with no direct browser access
    - Adminer: [http://localhost:8080](http://localhost:8080) or [http://db.localhost](http://db.localhost)
    - Nginx Proxy Manager: [http://localhost:8090](http://localhost:8090) or [http://proxy.localhost](http://proxy.localhost)

## Service Details

### Backend (FastAPI)

- **Directory**: `./backend`
- **Docker Container**: `fastapi_app`
- **Port**: `8000`
- **Environment Variables**:
  - `POSTGRES_SERVER`: Hostname of the PostgreSQL server.
  - `POSTGRES_PASSWORD`: Password for the PostgreSQL user.

### Frontend (ReactJS)

- **Directory**: `./frontend`
- **Docker Container**: `nodejs_app`
- **Port**: `5173`
- **Environment Variables**:
  - `VITE_API_URL`: URL of the backend API.

### Database (PostgreSQL)

- **Docker Image**: `postgres:latest`
- **Docker Container**: `postgres_db`
- **Port**: `5432`
- **Environment Variables**:
  - `POSTGRES_USER`: Username for PostgreSQL.
  - `POSTGRES_PASSWORD`: Password for the PostgreSQL user.
  - `POSTGRES_DB`: Name of the PostgreSQL database.
- **Volumes**:
  - `postgres_data`: Persists PostgreSQL data.

### Adminer

- **Docker Image**: `adminer`
- **Docker Container**: `adminer`
- **Port**: `8080`

### Proxy (Nginx Proxy Manager)

- **Docker Image**: `jc21/nginx-proxy-manager:latest`
- **Docker Container**: `nginx_proxy_manager`
- **Port**: `8090` or `81` 
- **Volumes**:
  - `./data`: Persistent data for the proxy manager.
  - `./letsencrypt`: SSL certificates.

### Nginx

- **Docker Image**: `nginx:latest`
- **Docker Container**: `nginx`
- **Port**: `80`
- **Volumes**:
  - `./nginx.conf`: Configuration file for Nginx.
  - `./proxy_params.conf`: Proxy parameters for Nginx.
- **Dependencies**:
  - `frontend`
  - `backend`
  - `db`
  - `adminer`
  - `proxy`

## Accessing the Application

- **Localhost**: Access the application at [http://localhost](http://localhost).
- **Custom Domain**: Configure your domain to connect to the application using the Nginx Proxy Manager.
