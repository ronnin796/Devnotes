docker images
docker ps
docler ps -a 
docker tag  "image-name" ronnin796/portfolio:v1.o
docker run -it --rm ronnin796/portfolio:v1.o
Here’s what the options mean:

-it → interactive terminal (so you can see output or interact with the container)

--rm → automatically remove the container when it exits (keeps your system clean)

ronnin796/portfolio:v1.o → the image name with the tag you just created
If your container runs a server or app and you need to expose ports, you can do:

`docker run -it -p 8000:8000 ronnin796/portfolio:v1.o`

That maps port 8000 inside the container to port 8000 on your host.
docker push ronnin796/portfolio:v1.o
docker stop $(docker ps -q)



## 1️⃣ Where Docker files live

On Linux, Docker stores its files (images, containers, volumes, networks) under:

`/var/lib/docker/`

- **`/var/lib/docker/overlay2/`** → filesystem layers for images/containers
    
- **`/var/lib/docker/containers/`** → container logs and metadata
    
- **`/var/lib/docker/volumes/`** → persistent volumes
    
- **`/var/lib/docker/image/`** → image metadata
    

This directory can grow huge over time, especially with large images like TensorFlow or PyTorch.

---

## 2️⃣ Clean up space

### a) Remove stopped containers

`docker container prune`

This deletes **all stopped containers**.

### b) Remove unused images

`docker image prune -a`

- `-a` removes **all unused images**, not just dangling ones.
    

### c) Remove unused volumes

`docker volume prune`

### d) Remove build cache

`docker builder prune`

- Frees space used during `docker build`.
    
- You can also do `docker system prune -a --volumes` to clean **everything unused** in one go.
    

---

## 3️⃣ Check disk usage

`docker system df`

- Shows how much space images, containers, and volumes take.
    

---

💡 **Pro tip:** TensorFlow, PyTorch, and large Python images can be **1–4 GB each**, so even after deleting images, build cache and volumes may still take **several GB**.

---

If you want, I can give you a **step-by-step command sequence to safely free up 10+ GB of Docker space** on your system. Do you want me to do that?

  

ChatGPT can make mistakes. Check important info.