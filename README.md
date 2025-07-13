
# 🐳 Docker Guide for Python, Streamlit & FastAPI Projects

![Docker Logo](https://user-images.githubusercontent.com/72096831/200459883-2ff14cb5-9378-4e5a-bbae-c8d423fb9220.png)

A complete Docker workflow guide for Python-based applications including **Streamlit**, **FastAPI**, and **GLPK (Pyomo)** with practical commands and error troubleshooting.

---

## 📁 Dockerfile Examples

### 🐍 Basic Python App

```dockerfile
# Use Python 3.8 base image
FROM python:3.8

# Set working directory
WORKDIR /folder_name

# Copy source code to container
COPY . /folder_name

# Install dependencies
RUN pip install -r requirements.txt

# Expose the application port
EXPOSE 5000

# Start the app
CMD ["python", "run.py"]
```

---

### 📊 Streamlit App with GLPK Support

```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY . /app

RUN apt-get update && \
    apt-get install -y glpk-utils && \
    pip install pyomo && \
    pip install -r requirements.txt

EXPOSE 8501

ENTRYPOINT ["streamlit", "run", "main.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

---

### ⚡ FastAPI App with GLPK Support

```dockerfile
FROM python:3.10

WORKDIR /app

COPY . /app

RUN apt-get update && \
    apt-get install -y glpk-utils && \
    pip install pyomo && \
    pip install -r requirements.txt

EXPOSE 8000

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

---

## 📦 Docker Image Commands

| Action                             | Command                                                                         |
| ---------------------------------- | ------------------------------------------------------------------------------- |
| 🔻 Pull image from Docker Hub      | `docker pull username/image_name`                                               |
| ⬆️ Push image to Docker Hub        | `docker tag new_image username/image_name`<br>`docker push username/image_name` |
| 📋 List local images               | `docker images`                                                                 |
| ❌ Remove a specific image          | `docker rmi image_name`                                                         |
| ❌❌ Remove all images               | `docker rmi -f $(docker images -q)`                                             |
| 🔍 Search for images on Docker Hub | `docker search username`                                                        |
| 🛠️ Build image from Dockerfile    | `docker build -t image_name .`                                                  |
| 💾 Save image to `.tar` file       | `docker save image_name > file_name.tar`                                        |
| 📦 Load image from `.tar` file     | Linux: `docker load -i file_name.tar`<br>Windows: `docker load < file_name.tar` |

---

## 📦 Docker Container Commands

| Action                           | Command                                                               |
| -------------------------------- | --------------------------------------------------------------------- |
| ▶️ Start container               | `docker start container_name`                                         |
| ⏹ Stop container                 | `docker stop container_name`                                          |
| ⏹⏹ Stop all containers           | `docker stop $(docker ps -aq)`                                        |
| 🗑 Remove a container            | `docker rm container_name`                                            |
| 🧹 Remove all stopped containers | `docker rm $(docker ps -aq)`                                          |
| 🔍 List all containers           | `docker ps -a`                                                        |
| ▶️ List running containers       | `docker ps`                                                           |
| 🔄 General Docker info           | `docker stats`, `docker info`                                         |
| 💬 Enter container shell         | `docker exec -it container_id bash`<br>`docker attach container_name` |

---

## 🚀 Run Container from Image

### Method 1: Create & Run Interactively

```bash
docker run -it --name container_name image_name
```

### Method 2: Run with Port Mapping

```bash
docker run -td --name container_name -p 5000:5000 image_name
```

### Method 3: Detached Mode Only

```bash
docker run -p 5000:5000 -d image_name
```

---

## 🛠 Docker Compose Workflow

```bash
docker-compose down
docker-compose up -d
```

This stops, removes, and recreates containers with the updated Docker Compose configuration.

---

## ❗ Troubleshooting: `pip` Connection Errors

### ❌ Error Example:

```
WARNING: Retrying (Retry(total=3, ...)) after connection broken by 'NewConnectionError(...)'
```

### ✅ Solution: Add DNS to `/etc/resolv.conf`

1. Open the DNS configuration file:

   ```bash
   sudo nano /etc/resolv.conf
   ```

2. Add the following lines:

   ```bash
   nameserver 8.8.8.8
   nameserver 8.8.4.4
   ```

3. Save and close the file:

   * In `nano`: Press `Ctrl + O` to save, `Ctrl + X` to exit.
   * In `vi`: Press `Esc`, type `:wq`, and hit Enter.

---

## ✅ Summary

This guide provides:

* Dockerfiles for various Python-based applications.
* Core Docker commands for managing images and containers.
* Solutions for common connectivity issues (`pip` DNS errors).
* Streamlit, FastAPI, and Pyomo integration examples.
