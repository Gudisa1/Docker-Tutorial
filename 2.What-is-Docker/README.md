---

# Docker Tutorial

---

## **1. What is Docker?**

Docker is an open-source platform designed to automate the deployment, scaling, and management of applications using containerization. It provides lightweight, portable, and self-contained environments that package an application with all its dependencies.

### **Why Docker?**
- **Consistency:** Ensures applications run identically in development, testing, and production.
- **Efficiency:** Containers use fewer resources than virtual machines.
- **Portability:** Containers can run on any system that supports Docker.
- **Rapid Deployment:** Containers start in milliseconds.

---

## **2. Docker Terminologies**

Here are the key terms in Docker and what they mean:

### **Image**
- A lightweight, immutable blueprint for creating containers.
- Contains the application and its dependencies.
- Example: The official `nginx` image contains the Nginx web server.

### **Container**
- A runtime instance of a Docker image.
- Containers are isolated environments for running applications.

### **Dockerfile**
- A script containing instructions to build a Docker image.
- Example: Install dependencies, copy files, and specify commands to run.

### **Docker Hub**
- A public registry for sharing Docker images.
- Example: Official images like `mysql` or `node`.

### **Volumes**
- Persistent storage for containers.
- Useful for storing data outside the container’s lifecycle.

### **Docker Compose**
- A tool to define and run multi-container Docker applications using a YAML file.

---

## **3. Docker Architecture**

Docker's architecture consists of the following components:

### **Components:**
1. **Docker Client:**
   - The primary interface for users.
   - Sends commands (like `docker run`) to the Docker daemon.

2. **Docker Daemon:**
   - Runs on the host machine.
   - Builds, runs, and manages containers.

3. **Docker Engine:**
   - The core component that executes the Docker commands.

4. **Images:**
   - Immutable templates used to create containers.

5. **Containers:**
   - The running instances of Docker images.

6. **Docker Registry:**
   - Stores Docker images (e.g., Docker Hub).

### **Diagram: Docker Architecture**
```plaintext
+--------------------+
|   Docker Client    |
|--------------------|
| docker commands    |
+--------------------+
         |
         v
+--------------------+
|   Docker Daemon    |
|--------------------|
| Manages containers |
+--------------------+
         |
         v
+--------------------+
|    Docker Images   |
+--------------------+
         |
         v
+--------------------+
|   Docker Containers|
+--------------------+
```

---

## **4. Docker Lifecycle**

Understanding the Docker lifecycle helps in managing containers effectively.

### **Docker Lifecycle Steps:**
1. **Build:**
   - Use a `Dockerfile` to create an image.
   ```bash
   docker build -t my-image .
   ```

2. **Run:**
   - Start a container from the built image.
   ```bash
   docker run -d my-image
   ```

3. **Stop:**
   - Stop a running container.
   ```bash
   docker stop container_id
   ```

4. **Remove:**
   - Delete stopped containers and images.
   ```bash
   docker rm container_id
   docker rmi image_id
   ```

5. **Restart:**
   - Restart stopped containers.
   ```bash
   docker start container_id
   ```

---

## **5. Installing Docker**

### **On Linux:**
1. **Update System Packages:**
   ```bash
   sudo apt update
   sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
   ```

2. **Add Docker’s GPG Key:**
   ```bash
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
   ```

3. **Set Up Repository:**
   ```bash
   sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
   ```

4. **Install Docker:**
   ```bash
   sudo apt update
   sudo apt install -y docker-ce
   ```

5. **Verify Installation:**
   ```bash
   docker --version
   ```

---

## **6. Running a Simple "Hello World" Node.js App**

### **Step 1: Create a Node.js Application**
1. Create a directory for the application:
   ```bash
   mkdir hello-docker && cd hello-docker
   ```

2. Initialize a new Node.js project:
   ```bash
   npm init -y
   ```

3. Create a `server.js` file:
   ```javascript
   const http = require('http');

   const hostname = '0.0.0.0';
   const port = 3000;

   const server = http.createServer((req, res) => {
     res.statusCode = 200;
     res.setHeader('Content-Type', 'text/plain');
     res.end('Hello, Docker!');
   });

   server.listen(port, hostname, () => {
     console.log(`Server running at http://${hostname}:${port}/`);
   });
   ```

4. Install dependencies:
   ```bash
   npm install
   ```

---

### **Step 2: Create a Dockerfile**
1. Create a file named `Dockerfile` in the `hello-docker` directory.
   ```Dockerfile
   # Use the Node.js image as the base image
   FROM node:14

   # Set the working directory
   WORKDIR /app

   # Copy package files and install dependencies
   COPY package*.json ./
   RUN npm install

   # Copy the application code
   COPY . .

   # Expose the port
   EXPOSE 3000

   # Run the application
   CMD ["node", "server.js"]
   ```

---

### **Step 3: Build and Run the Docker Container**
1. **Build the Docker Image:**
   ```bash
   docker build -t hello-docker .
   ```

2. **Run the Docker Container:**
   ```bash
   docker run -d -p 3000:3000 hello-docker
   ```

3. **Access the Application:**
   Open a browser and visit `http://localhost:3000`. You should see:
   ```
   Hello, Docker!
   ```

4. **Stop the Container:**
   ```bash
   docker stop container_id
   ```

---

### **Conclusion**
This guide has walked through Docker’s core concepts, architecture, lifecycle, and how to set up a simple "Hello World" Node.js application. With this foundation, you can now build and manage your own containerized applications.
