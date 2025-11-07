# **Technology Stack**

GKMIT_INSIDE is built using modern web technologies to ensure performance, scalability, and maintainability.

<!-- <div style="display: flex; justify-content: start; align-items: center; gap: 30px;">
  <img src="https://cdn.worldvectorlogo.com/logos/react-2.svg" alt="React" width="75">
  <img src="https://cdn.worldvectorlogo.com/logos/nodejs-icon.svg" alt="Node.js" width="75">
  <img src="https://cdn.worldvectorlogo.com/logos/express-109.svg" alt="Express.js" width="100" style="background-color: white; padding: 0.2rem">
  <img src="https://cdn.worldvectorlogo.com/logos/mongodb-icon-1.svg" alt="MongoDB" width="75">
  <img src="https://cdn.worldvectorlogo.com/logos/tailwindcss.svg" alt="TailwindCSS" width="75">
</div> -->

<div style="display: flex; justify-content: center; align-items: center; flex-wrap: wrap; gap: 30px;">

  <!-- ReactJS -->
  <img src="https://cdn.worldvectorlogo.com/logos/react-2.svg" alt="ReactJS" width="90">

  <!-- TailwindCSS -->
  <img src="https://cdn.worldvectorlogo.com/logos/tailwindcss.svg" alt="TailwindCSS" width="90">

  <!-- Shadcn UI -->
  <img src="https://avatars.githubusercontent.com/u/139895814?s=200&v=4" alt="Shadcn UI" width="90" style="border-radius: 10px;">

  <!-- Node.js -->
  <img src="https://cdn.worldvectorlogo.com/logos/nodejs-icon.svg" alt="Node.js" width="90">

  <!-- Express.js -->
  <span style="display:inline-flex;align-items:center;justify-content:center;width:85px;height:85px;background:white;padding:6px;border-radius:10px;box-shadow:0 1px 2px rgba(0,0,0,0.08);">
    <img src="https://cdn.worldvectorlogo.com/logos/express-109.svg" alt="Express.js" width="100">
  </span>

  <!-- MongoDB -->
  <img src="https://cdn.worldvectorlogo.com/logos/mongodb-icon-1.svg" alt="MongoDB" width="90">

  <!-- Vercel -->
  <img style="display:inline-flex;align-items:center;justify-content:center;width:85px;height:85px;background:white;padding:6px;border-radius:10px;box-shadow:0 1px 2px rgba(0,0,0,0.08);" src="https://cdn.worldvectorlogo.com/logos/vercel.svg" alt="Vercel" width="100">
</div>

## Stack Overview

| Category                 | Technology  | Purpose                    |
| ------------------------ | ----------- | -------------------------- |
| **Frontend Framework**   | ReactJS     | Core Library               |
| **State Management**     | Context API | Global state management    |
| **Styling Framework**    | TailwindCSS | Utility-first CSS styling  |
| **UI Component Library** | Shadcn UI   | Pre-built UI components    |
| **Backend Framework**    | Express.js  | Web application framework  |
| **Database**             | MongoDB     | NoSQL document database    |
| **Authentication**       | JWT         | Token-based authentication |
| **Frontend Deployment**  | Vercel      | Frontend hosting platform  |
| **Backend Deployment**   | Render      | Backend hosting platform   |

---

## System Architecture Diagram

```
┌─────────────────────────────────────────────────┐
│                   Client Layer                  │
│  (React + Context API + TailwindCSS + Shadcn)   │
└──────────────────┬──────────────────────────────┘
                   │ HTTPS/REST API
┌──────────────────┴──────────────────────────────┐
│              Application Layer                  │
│         (Node.js + Express + JWT)               │
└──────────────────┬──────────────────────────────┘
                   │ MongoDB Driver
┌──────────────────┴─────────────────────────────-─┐
│               Database Layer                     │
│                  (MongoDB)                       │
└──────────────────────────────────────────────────┘
```

---
