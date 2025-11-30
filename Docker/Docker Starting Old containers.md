

### 🧩 1. To simply restart the old container:

`docker start -a portfolio`

- `-a` (attach) means it’ll show logs/output in your terminal
    
- You can remove `-a` if you want it to run in background:
    
    `docker start portfolio`
    

If the app runs fine, you’re done ✅

---

### 🧩 2. If it fails or crashes again (common after long time):

It’s usually because:

- The container’s environment is outdated
    
- Code has changed since it was built
    
- Dependencies weren’t persisted properly
    

In that case, it’s better to **rebuild and rerun** it:

#### Step 1: Remove the old container

`docker rm portfolio`

#### Step 2: Rebuild the image (if you have the Dockerfile)

`docker build -t my-portfolio .`

#### Step 3: Run it again with a name and port mapping

`docker run -d -p 8000:8000 --name portfolio my-portfolio`

- `-d` = run detached (background)
    
- `-p 8000:8000` = expose port 8000 (change depending on your app)
    
- `--name portfolio` = gives your container an easy name
    

Then open:  
👉 http://localhost:8000

---