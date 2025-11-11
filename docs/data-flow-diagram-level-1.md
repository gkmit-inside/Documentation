# **DFD: Level 1 — GKMIT INSIDE**

## Overview

This Data Flow Diagram (Level 1) illustrates the internal functional breakdown of the **GKMIT_INSIDE** system, which facilitates employee engagement and administrative management. The system supports operations like user registration, authentication, post creation, feed delivery, and interactive features such as comments, reactions, and bookmarks.

Additionally, it provides administrators with user and post management capabilities along with analytics and dashboard insights. The flow clearly depicts how various components interact with the MongoDB database to maintain data consistency and transparency across modules.

---

## Data Flow Diagram: Level 1

![DFD: Level - 0](assets/images/dfd-level-1.png){ width="1900" height="1600" }

---

## Description

The diagram expands on the Level 0 view by detailing individual subsystems within the GKMIT_INSIDE platform. Employees interact with the system through **Authentication**, **Post Management**, **Feed**, and **Interaction** modules.

- Authentication handles user login and registration, storing and validating records in the **USERS** collection.
- Once authenticated, users can create, edit, or delete posts via the Post Management module, which updates the **POSTS** database.
- Admins have extended access through **User Management** to approve or reject users, and through **Post Management** to review and moderate content.
- The **Feed** module retrieves approved posts for users, while **Interaction Features** capture user engagement—storing comments, reactions, and bookmarks into their respective collections.
- Finally, the **Analytics & Dashboard** module aggregates user, post, and interaction data to generate insights and reports for administrators.
- The database serves as a centralized backbone for all operations, ensuring smooth data exchange across the system.

---
