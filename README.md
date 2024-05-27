# DevOps

## Terminal Commands

Follow these steps to build the Docker image, create the network, and run the containers:

### 1. Build the PostgreSQL Image

```bash
docker build -t my-postgres-db .
```

### 2. Run the PostgreSQL Container

```bash
docker run -d --name my-postgres-container my-postgres-db
```

### 3. Create the Docker Network

```bash
docker network create app-network
```

### 4. Remove the Running PostgreSQL Container

```bash
docker rm -f my-postgres-container
```

### 5. Run the PostgreSQL Container on the Network

```bash
docker run -d --name my-postgres-container --network app-network -v /data_dir:/var/lib/postgresql/data my-postgres-db
```

### 6. Run Adminer on the Network

```bash
docker run -d -p 8090:8080 --name adminer --network app-network adminer
```

### Access Adminer
Open your web browser and go to http://localhost:8090 to access Adminer. Use the following credentials to connect to the PostgreSQL database:

- Server: my-postgres-container
- User: usr
- Password: pwd
- Database: db

### Explanation

- Dockerfile: Defines the PostgreSQL image configuration, including environment variables and SQL scripts to initialize the database.
- docker build: Builds the Docker image from the Dockerfile.
- docker run: Runs a container from the built image.
- docker network create: Creates a Docker network named app-network for container communication.
- docker rm -f: Forces removal of the existing PostgreSQL container.
- docker run --network: Runs the PostgreSQL container within the created network and mounts a volume for persistent data.
- Adminer: A lightweight database management tool to manage PostgreSQL.
