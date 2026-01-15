# Job Application-Tracker Deployment

This repository contains the **deployment configuration** for the full **Application-Tracker** stack, including:

- **Frontend** [Application Tracker Frontend](https://github.com/Tobin123456/Job-Application-Tracker-Frontend)
- **Backend** [Application Tracker Backend](https://github.com/Tobin123456/Job-Application-Tracker-Backend)
- **Database** PostgreSQL



The deployment uses **Docker Compose** to run all components together in a consistent and isolated environment.

---

## Features

- Full-stack deployment of the Application-Tracker project
- Database with persistent storage using Docker volumes
- Environment variables can be customized for your own setup
- Easy update of frontend and backend images

---

## Getting Started

### Prerequisites

- [Docker](https://www.docker.com/get-started)
- [Docker Compose](https://docs.docker.com/compose/install/)

Clone this repository and navigate to it:

```bash
git clone https://github.com/Tobin123456/application-tracker-deployment.git
cd application-tracker-deployment
```
### Running the Stack

Use the following commands to start, access, and stop the full Application-Tracker stack.  

1. Start the full stack in detached mode
   ```bash
   docker-compose up -d
   ```

2. Access the services
   - PostgreSQL database -> localhost:5432
   - Backend API         -> localhost:8080
   - Frontend UI         -> localhost:4200

3. Stop the stack
   ```bash
   docker-compose down
   ```

4. Optional: Rebuild images if frontend or backend was updated
   ```bash
   docker-compose build
   docker-compose up -d
   ```

### Environment Variables

You can customize the deployment by editing the `docker-compose.yml` file.  
The following environment variables are available for the database, backend, and frontend services.

---

#### Database (PostgreSQL)

| Variable | Default | Description |
|----------|---------|-------------|
| `POSTGRES_DB` | `application_data` | Name of the PostgreSQL database. |
| `POSTGRES_USER` | `job_searcher` | Username for the database. |
| `POSTGRES_PASSWORD` | `231198` | Password for the database user. |

---

#### Backend (Spring Boot)

| Variable | Default | Description |
|----------|---------|-------------|
| `SPRING_DATASOURCE_URL` | `jdbc:postgresql://db:5432/application_data` | JDBC URL used by the backend to connect to PostgreSQL. |
| `SPRING_DATASOURCE_USERNAME` | `job_searcher` | Database username for Spring Boot. |
| `SPRING_DATASOURCE_PASSWORD` | `231198` | Database password for Spring Boot. |
| `CORS_ALLOWED_ORIGINS` | `http://localhost:4200` | Allowed origins for cross-origin requests (frontend URL). |
| `JWT_SECRET_KEY` | `MySuperSecretKeyForJWTsThe_Factory_Must_Grow!` | Secret key used to sign JWT tokens for authentication. |

---

#### Frontend

- The frontend does not require environment variables in this deployment setup.  
- If the backend URL changes, you may need to update the API endpoint in the frontend [config](https://github.com/Tobin123456/Job-Application-Tracker-Frontend/blob/main/src/assets/config/app-config.json).

---

> ⚠️ **Note:** If you modify the backend or frontend code and build new Docker images, update the corresponding `image:` paths in `docker-compose.yml` to point to your new images.

## Updating Backend or Frontend Images

If you have updated the backend or frontend and built new Docker images, you need to update this deployment to use your latest images.

---

### 1. Update docker-compose.yml

Edit the `docker-compose.yml` file and replace the old image paths with your new images:

```yaml
backend:
  image: ghcr.io/<YOUR_GITHUB_USERNAME>/application-tracker-backend:<tag>
...
frontend:
  image: ghcr.io/<YOUR_GITHUB_USERNAME>/application-tracker-frontend:<tag>
```

### 2. Update docker-compose.yml

After updating the images in docker-compose.yml, restart the stack:

```bash
docker-compose up -d
```

## License

This deployment repository itself does not contain any code beyond configuration and documentation.  

Please refer to the licenses of the respective projects:  

- [Application Tracker Frontend](https://github.com/Tobin123456/Job-Application-Tracker-Frontend)
- [Application Tracker Backend](https://github.com/Tobin123456/Job-Application-Tracker-Backend)

These repositories contain the source code and are distributed under their own licenses.


