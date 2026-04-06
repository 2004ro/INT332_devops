# Unit 1: Basics of DevOps Infrastructure

## 1. The Need for Containers: Virtualization vs. Containerization
With changing times, businesses needed solutions to reduce overhead costs, enhance scalability, and standardize application deployment. 

### Virtualization
Virtualization is the process of partitioning a physical server into multiple virtual servers using software called a 'hypervisor' (e.g., VMware, VirtualBox). 
* **How it works:** Each Virtual Machine (VM) contains a full Host OS, application code, and libraries.
* **Drawbacks:** Heavy storage requirements, high memory usage, slow startup times, and lower overall system efficiency.

### Containerization
Containers reduce complexity and resource usage. Unlike VMs, containers run on the same Host OS but behave as if they are separate machines. 
* **Container Runtime:** Responsible for creating, starting, and stopping containers.
* **Advantages:** Lightweight, highly efficient, and extremely fast startup times.

---

## 2. Docker Architecture & The Docker Engine
Docker uses a client-server architecture. 

* **Docker Client (CLI):** This is where you type commands (like `docker run`). It sends your requests to the Daemon.
* **Docker Host (Daemon):** The core engine running on your machine. Think of the Daemon as a **restaurant kitchen**—the customer (CLI) places orders, and the kitchen (Daemon) does all the cooking (building images, starting containers, managing networks). You never go into the kitchen; you just send requests and get results!
* **Docker Registry:** A central storage location where images are stored and shared (e.g., Docker Hub).

### High-Level vs. Low-Level Runtimes
* **High-Level Runtime (Docker Engine):** Handles image pulling, networking, storage, and container lifecycles.
* **Low-Level Runtime (runC & Linux Kernel):** Works directly with the OS Kernel to manage CPU, memory, processes, and hardware resources.

---

## 3. How Containers Achieve Isolation
Containers use features of the Linux Kernel to create isolated environments.

### Namespaces (Process Isolation)
Namespaces ensure that processes inside one container cannot see or interfere with the host system or other containers.
* **PID Namespace:** Gives each container its own independent process tree. Process IDs inside a container start fresh from 1.
* **Network Namespace:** Gives each container its own network environment (own IP address, routing tables, and port numbers). This allows multiple containers to use port 80 internally without conflicting on the host.
* **Mount Namespace:** Isolates the file system. Each container has its own root file system. Files created inside the container do not affect the host system.
* **UTS Namespace (Unit Timesharing):** Allows the container to have its own hostname, behaving like a separate machine on the network.
* **User Namespace (Advanced):** Maps container users to non-root users on the host for security.

### Control Groups (Cgroups)
While Namespaces isolate the *processes*, **Cgroups** limit the *resources* (CPU, Memory) that a container can use so one container doesn't consume the entire system's capacity.

---

## 4. Docker Images & Layers
A container image is a **read-only, immutable blueprint** used to run an application. Images are built as a stack of layers, and Docker saves these layers in a cache to speed up future builds.

* **Layer 1: Base OS Layer** (Minimal OS, e.g., Linux)
* **Layer 2: Runtime Layer** (Environment to run the app, e.g., Python, Java)
* **Layer 3: Dependencies Layer** (Required libraries)
* **Layer 4: Application Layer** (Your actual code)

**Tags:** Tags identify different versions of the same image (e.g., `latest` (default), `v1`, `dev`, `qa`). Without a tag, Docker assumes you want the `latest` version.

---

## 5. Image Registries & Distribution
A registry is where developers push and pull container images.
* **Public Registries:** Open to everyone (e.g., Docker Hub).
* **Private Registries:** Restrict access using authentication. Used by companies for production applications so only authorized servers can access the code (e.g., Amazon ECR).

**The Standard Image Distribution Process:**
1.  **Build:** `docker build -t myapp:v1.0 .`
2.  **Tag:** `docker tag myapp:v1.0 username/myapp:v1.0`
3.  **Login:** `docker login`
4.  **Push:** `docker push username/myapp:v1.0`
5.  **Pull (on server):** `docker pull username/myapp:v1.0`
6.  **Run (on server):** `docker run username/myapp:v1.0`
