# 🚀 Project: Deploy a Static Website in Apache Container on RHEL EC2

## 🎯 Objective

Deploy a static HTML website using **Apache HTTPD inside a container**, running on a **RHEL EC2 instance** in **AWS**.

---

## 🧰 Technologies Required

- AWS Account
- Red Hat Enterprise Linux (RHEL) EC2 instance
- Podman or Docker
- Apache HTTP Server (via container)
- Basic HTML knowledge

---

## 📝 Project Tasks

### 1. Launch EC2 Instance (RHEL)
- Launch a new EC2 instance using a RHEL AMI.
- Configure the security group to allow SSH and HTTP traffic.
- Connect to the instance using SSH.

---

### 2. Install Container Engine
- Update the system packages.
- Install and verify either Podman or Docker.

---

### 3. Prepare Static Website
- Create a simple `index.html` file that displays a message in the browser.
- Organize your project files in a working directory.

---

### 4. Create a Dockerfile
- Use the `httpd` base image.
- Copy the HTML file into Apache's web root directory.
- Build the container image.

---

### 5. Run the Container
- Expose port 80 from the container to the host.
- Ensure Apache serves your HTML page correctly from inside the container.

---

### 6. Verify Deployment
- Open the EC2 public IP in a browser.
- Confirm that your HTML content is served properly via Apache.

---


