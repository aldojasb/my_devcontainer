# 🛠️ Personal Dev Container Setup

This project provides a fully isolated personal development environment using **Dev Containers + Docker Compose**, complete with:
- Python development tools
- PostgreSQL database
- `pgAdmin` for visual DB inspection

---

## Services Overview

### 👨‍💻 `personal_dev`
Your main coding environment inside a container:
- Based on a Python image with custom tooling
- Automatically mounts the current project to `/workspace`
- Exposes port `8000` for your local app

### 🛢️ `personal_database`
A PostgreSQL service for local DB development:
- Credentials:
  - **DB**: `my_database`
  - **User**: `my_user`
  - **Password**: `my_password`
- Exposed on port **15432** (so it doesn't conflict with work projects)

### 🧠 `pg_admin`
A web-based PostgreSQL GUI:
- Runs on port `18888`
- Login:
  - **Email**: `personal@localhost.com`
  - **Password**: `my_pgadmin_password`

---

## Getting Started

### 1. Open in VS Code
Use the Dev Containers extension to open the project folder in a container:

Remote-Containers: Open Folder in Container


### 2. Install Your Project Tools
Once inside:
```bash
cd /workspace
poetry install  # Or use pip install -r requirements.txt
```

### 3. Launch Your App
If you're using FastAPI, for example:

```bash
uvicorn app.main:app --host 0.0.0.0 --port 8000
```

Then visit: http://localhost:8000


## Using pgAdmin
Open your browser and go to:

http://localhost:18888
Log in using:

Email: personal@localhost.com

Password: my_pgadmin_password

Register a new server:

Name: Local Postgres

Host: personal_database

Port: 5432

Username: my_user

Password: my_password

---

# Benefits and Downsides of Working with Dev Containers

## Benefits of Working with Dev Containers

### 1. **Isolated Development Environment**
Dev containers provide a fully isolated environment that won’t affect the host system. This is especially useful for keeping development dependencies, libraries, and versions separate from the host system, ensuring no accidental conflicts.

### 2. **Reproducibility**
The development environment is consistent across different machines. By defining the environment in a Dockerfile or `devcontainer.json`, you ensure that all team members and CI pipelines can recreate the exact same setup, reducing “works on my machine” issues.

### 3. **Pre-configured Tools and Libraries**
You can pre-configure your container with all the tools and dependencies (like Python, pyenv, poetry, etc.) so that when you start a new project, your development environment is ready to go without additional setup.

### 4. **Version Control for Development Environments**
The configuration of the dev container (like Python versions, tools, dependencies) can be stored in version control (alongside your code), allowing you to roll back to a known working environment if needed.

### 5. **Integration with VS Code**
When using dev containers with VS Code, you get a seamless experience where the IDE runs inside the container, so any tools installed inside the container (e.g., pyenv, poetry, Python, linters) work directly within VS Code.

### 6. **Lightweight and Portable**
Dev containers are built on Docker, making them lightweight and portable across different operating systems (Linux, Windows, macOS).

## Downsides of Working with Dev Containers

### 1. **Learning Curve**
Docker and container management can have a learning curve, especially when it comes to debugging, networking, and managing volumes. Setting up a containerized environment might take extra time compared to a local setup.

### 2. **Performance Overhead**
Running containers can introduce some performance overhead, especially on macOS and Windows due to Docker’s architecture. Performance might vary depending on the complexity of the container and how it interacts with the host system (e.g., file mounting).

### 3. **Dependency on Docker**
You need Docker installed on your machine, and for certain environments, this might not be possible due to restrictions or lack of administrative privileges.

### 4. **Complexity in Managing Multiple Containers**
If you’re running multiple containers (e.g., a web server, database, app container), managing container orchestration, networking, and volumes can add complexity to the setup.

---

By understanding the pros and cons, you can determine if dev containers are the right choice for your development workflow.


