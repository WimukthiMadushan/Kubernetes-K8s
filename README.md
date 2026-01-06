## ☸️ Introduction to Kubernetes


**K8s** is an open-source container orchestration platform originally developed by Google and now maintained by the Cloud Native Computing Foundation (CNCF).

Kubernetes is designed to automate the deployment, scaling, and management of containerized applications. It helps developers and operators run applications reliably in production environments by managing containers across a cluster of machines.

Key capabilities of Kubernetes include:
- Automatic deployment and rollback of applications  
- Horizontal scaling based on demand  
- Self healing (restarting failed containers)  
- Service discovery and load balancing  
- Configuration and secret management  

By abstracting the underlying infrastructure, Kubernetes allows applications to run consistently across on-premises, cloud, and hybrid environments, making it a core technology in modern cloud-native systems.

## 📚 Core Concepts in Kubernetes

### 1️⃣ Containers
Containers are lightweight, portable units that package an application along with all its dependencies, libraries, and runtime environment. They ensure that applications run consistently across different systems. Tools like Docker are commonly used to build and run containers.

---

### 2️⃣ Kubernetes
kubernetes is an open-source container orchestration platform that manages containerized applications at scale. It automates deployment, scaling, load balancing, and recovery of applications running in containers.

---

### 3️⃣ Kubernetes Cluster
A Kubernetes cluster is a group of machines (nodes) that work together to run containerized applications.  
It consists of:
- **Control Plane** – Manages the cluster state, scheduling, and orchestration  
- **Worker Nodes** – Run application workloads inside pods  

Clusters provide high availability and fault tolerance.
(minikube is a local one node cluster which helpful for local test applications)

#### 📌 Kubernetes Cluster Architecture

<p align="center">
  <img src="https://github.com/user-attachments/assets/48a59b60-5ce8-489c-9f72-e0d8a4a0c1b5"
       width="750"
       alt="Kubernetes Cluster Architecture Diagram">
</p>

## 🧠 Control Plane Components (Cluster Brain)

These components decide **what should run**, **where it should run**, and **what to do when something fails**.

### 🔹 kube-apiserver
- The **entry point** to the cluster
- All commands (`kubectl`, dashboards, CI/CD tools) talk to the cluster through this
- Validates and processes requests

Think of it as the **front desk** of Kubernetes.

### 🔹 etcd
- A **key-value database** that stores the entire cluster state
- Saves information about:
  - Nodes
  - Pods
  - Configurations
  - Secrets

Think of it as the **memory** of the cluster.

### 🔹 controller-manager
- Continuously checks if the cluster matches the desired state
- If something goes wrong (pod crashes, node fails), it takes action

Think of it as the **auto-repair system**.

### 🔹 kube-scheduler
- Decides **which worker node** should run a new pod
- Considers CPU, memory, and availability

Think of it as the **task allocator**.

## 🖥️ Worker Node Components (Where Apps Run)

Worker nodes are responsible for actually **running your applications**.

### 🔹 kubelet
- An agent running on each worker node
- Communicates with the control plane
- Ensures containers are running as instructed

Think of it as the **node supervisor**.

### 🔹 kube-proxy
- Handles **networking and load balancing**
- Allows services to communicate with pods
- Maintains network rules

Think of it as the **traffic controller**.

### 🔹 Container Runtime
- Software that actually **runs containers**
- Common runtimes:
  - containerd
  - Docker (via containerd)

Think of it as the **engine** that runs containers.

---

### 4️⃣ Pods
A **Pod** is the smallest deployable unit in Kubernetes.  
It represents a single instance of an application and can contain:
- One main container (most common)
- Multiple containers (sidecar pattern)

Pods share the same network and storage resources and are always scheduled onto a single node.

---

### 5️⃣ ReplicaSets
A **ReplicaSet** ensures that a specified number of identical pods are running at all times.  
If a pod crashes or is deleted, the ReplicaSet automatically creates a new one, providing:
- High availability
- Fault tolerance
- Load distribution

---

### 6️⃣ Deployments
A **Deployment** is a higher level abstraction that manages ReplicaSets and Pods.  
It enables:
- Rolling updates (zero-downtime deployments)
- Rollbacks to previous versions
- Easy scaling of applications  

Deployments are the most commonly used way to deploy applications in Kubernetes.

---

### 7️⃣ Services
A **Service** provides a stable network endpoint to access a set of pods.  
Since pods are dynamic and their IPs change, services ensure reliable communication by,
- Load balancing traffic
- Enabling service discovery
- Exposing applications internally or externally

Common service types include ClusterIP, NodePort, and LoadBalancer.

---

### 8️⃣ Ingress
An **Ingress** manages external access to services within a Kubernetes cluster, typically via HTTP or HTTPS.

Instead of exposing multiple services using different ports or load balancers, Ingress provides:
- Path-based routing (`/api`, `/app`)
- Host-based routing (`app.example.com`)
- TLS/HTTPS termination
- Centralized traffic control

Ingress works together with an **Ingress Controller** (such as NGINX or Traefik) to route incoming traffic to the correct services.

---


### 9️⃣ ConfigMaps
A **ConfigMap** is used to store non sensitive configuration data separately from application code.

It allows you to:
- Inject configuration into containers as environment variables
- Mount configuration files into pods
- Update application behavior without rebuilding images

Using ConfigMaps improves portability and follows best practices by separating configuration from application logic.

---

### 🔟 Volumes (Data Inside Kubernetes)
By default, data inside a container is **ephemeral**, meaning it is lost when the pod is restarted or recreated.  
Kubernetes **Volumes** provide a way to share and preserve data during a pod’s lifecycle.

Volume types include:
- **EmptyDir** – Temporary storage shared between containers in a pod  
- **HostPath** – Uses local node storage (not recommended for production)  

For persistent data, Kubernetes integrates with **storage backends**, such as:
- Cloud storage (AWS EBS, GCP Persistent Disk, Azure Disk)
- Network storage (NFS, Ceph)

These are commonly accessed via Persistent Volumes (PV) and Persistent Volume Claims (PVC).

---

### 1️⃣1️⃣ StatefulSets
A **StatefulSet** is a workload controller designed for stateful applications that require:
- Stable pod identities
- Predictable network names
- Persistent storage per pod

Unlike Deployments, StatefulSets ensure:
- Ordered pod creation and deletion
- Each pod gets its own dedicated storage
- Pod names remain consistent (e.g., `db-0`, `db-1`)

StatefulSets are commonly used for databases, message queues, and distributed systems such as MySQL, PostgreSQL, Kafka, and Redis.

---
