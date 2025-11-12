# **AWS System Architecture Overview**

## **Overview of the Architecture**

This architecture illustrates a **hybrid deployment model** where the **frontend** is hosted on **Vercel**, while the **backend (API/server)** and data infrastructure reside within **Amazon Web Services (AWS)**.  
This setup leverages the strengths of both platforms:

- **Vercel** → optimized for global, fast frontend delivery.
- **AWS Cloud** → provides a secure, scalable, and customizable backend environment.

![Auth DFD: Level - 2](assets/images/aws-arch.png){ width="2900" height="2600" }

The system serves users who access the Vercel-hosted frontend. The frontend communicates with the backend running on an **EC2 instance** within a protected **AWS Virtual Private Cloud (VPC)**.

---

## **Workflow**

The system workflow can be categorized into two major flows — **Deployment Workflow** and **Runtime Data Flow**.

### **1. Deployment Workflow (CI/CD)**

The deployment pipeline handles client (frontend) and server (backend) code separately:

#### **Frontend Deployment (Vercel)**

- The **frontend Git repository** is connected directly to **Vercel**.
- Any push to the `main` or deployment branch triggers **Auto Deploy**.
- Vercel builds and deploys the frontend globally for fast user access.

#### **Backend Deployment (AWS EC2)**

- The **backend Git repository** uses a **GitHub Actions Deploy Pipeline**.
- The workflow packages the backend code and deploys it to **Amazon EC2**, located in the **Public Subnet** of the **VPC**.
- The deployment ensures that the backend remains up-to-date and securely hosted inside the AWS infrastructure.

---

### **2. Runtime Workflow (Data Flow)**

The runtime flow defines how data moves between the user, frontend, backend, and external data services:

1. **User Request**  
   Users access the web application via the **Vercel Frontend Deployment**.

2. **API Interaction**  
   The frontend communicates with the **AWS EC2 Backend** through secure REST API calls, handling operations such as data fetching and form submission.

3. **Data Persistence**  
   The EC2 backend interacts with two key external data services:

   - **MongoDB Atlas** → For primary database operations (structured app data).
   - **ImageKit** → For image storage, optimization, and delivery.

4. **Response**  
   The backend processes logic, retrieves or updates data as required, and sends a structured response to the **Vercel frontend**, which renders the final user-facing output.

---

## **Summary**

This **AWS-Vercel Hybrid Architecture** achieves a balance of performance, security, and scalability:

- **Vercel** ensures **fast, global content delivery** for the frontend.
- **AWS EC2** provides a **secure, private compute environment** for backend logic.
- **MongoDB Atlas** and **ImageKit** deliver **scalable storage and media handling**.
- Together, they form a **modern, modular cloud architecture** designed for real-time performance and maintainable infrastructure.
