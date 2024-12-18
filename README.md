## Automate Deployment with Terraform and Ansible  

### **Task Overview**  

You will:
1. **Prebuild and push Docker images for the application stack from Week 1..**
2. **Design and provision cloud infrastructure using Terraform.**
3. **Use Terraform to:**
   - Trigger Ansible playbooks for:
     - Deploying the application stack.
     - Deploying the monitoring stack.
     - Configuring routing with Traefik or Nginx.
   - Automatically generate the `inventory.ini` file for Ansible.  
4. **Set up application and monitoring stacks using Ansible roles.**

The final deployment will be tested by running:
```bash
terraform apply -auto-approve
```
This command should provision the infrastructure, deploy all services, and configure routing automatically.

---

### **Components**  

#### **1. Application Stack(Same app as Week 1)**
- **Frontend:** A React application.
- **Backend:** A FastAPI service.
- **Database:** PostgreSQL.
- **Reverse Proxy:** Traefik or Nginx (for routing between services).

You must prebuild the Docker images for the **Frontend** and **Backend** and push them to your public Docker Hub repositories:  
- Example frontend image: `docker.io/<your_username>/frontend:latest`  
- Example backend image: `docker.io/<your_username>/backend:latest`  

The application stack Ansible role will pull these images from Docker Hub.

---

#### **2. Monitoring Stack**
- **Prometheus** for metrics collection.
- **Grafana** for visualization (configured with dashboards for cAdvisor and Loki).
- **cAdvisor** for container-level metrics.
- **Loki** for log aggregation.
- **Promtail** for log collection.

---

#### **3. Deployment Workflow**
- **Terraform:**  
  - Provisions the cloud infrastructure (e.g., server instance, networking).
  - Generates the Ansible inventory file (`inventory.ini`) dynamically.  
  - Triggers Ansible playbooks.  

- **Ansible:**  
  - Configures the server environment.  
  - Creates a shared Docker network.  
  - Deploys the application and monitoring stacks by pulling prebuilt images from Docker Hub and running them via Docker Compose.  
  - Configures Traefik or Nginx for routing across all services.

---

### **What You Need to Do**  

#### **Step 1: Prebuild Docker Images**  
1. Build the Docker images for the **Frontend** and **Backend** applications(Same app as Week 1).
2. Push the images to your public Docker Hub repositories.  

#### **Step 2: Design the Architecture**
1. Create an architecture diagram for the deployment, showing how the application and monitoring stacks interact.  
2. Ensure your design accounts for:  
   - Shared Docker networks.  
   - Routing between services.  

#### **Step 3: Write Terraform and Ansible Configurations**
1. **Terraform:**  
   - Provision cloud infrastructure (e.g., a VM instance).  
   - Automatically generate the Ansible inventory file (`inventory.ini`).  
   - Trigger Ansible playbooks.  

2. **Ansible:**  
   - Use roles to:
     - Configure the server environment.
     - Set up and run the **Application Stack** (using Docker Compose).
     - Set up and run the **Monitoring Stack** (using Docker Compose).
     - Configure routing with Traefik.

---


