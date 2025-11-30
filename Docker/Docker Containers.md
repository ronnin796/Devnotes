### 🧱 1. See running containers

`docker ps`

This shows all **currently running** containers.  
Example output:

`CONTAINER ID   IMAGE         COMMAND                  STATUS         PORTS                    NAMES a1b2c3d4e5f6   catdog-app    "streamlit run app.py"   Up 2 minutes   0.0.0.0:8501->8501/tcp   catdog-container`

---

### 🧱 2. See _all_ containers (including stopped ones)

`docker ps -a`

This lists every container (running + stopped), along with their **exit codes** and **statuses**.

---

### 🧱 3. Stop a running container

`docker stop <container_id_or_name>`

Example:

`docker stop a1b2c3d4e5f6`

---

### 🧱 4. Remove a stopped container

`docker rm <container_id_or_name>`

Or remove **all stopped** containers:

`docker container prune`

---

### 🧱 5. View container logs

If your app is running but you don’t see output:

`docker logs <container_id_or_name>`

---

### 🧱 6. Enter a container shell (for debugging)

`docker exec -it <container_id_or_name> /bin/bash`

You’ll get an interactive shell inside the container — great for debugging or checking files.

---

### 🧱 7. Remove all containers and images (cleanup)

⚠️ Use carefully — this clears everything:

`docker system prune -a`

---

Would you like me to show you how to **name** your container (so you can easily find it, e.g., `catdog-demo`) when you run it?