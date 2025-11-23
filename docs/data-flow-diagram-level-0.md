# **Level 0 — Context Diagram**

## Overview

This **Level 0 Data Flow Diagram (DFD)** provides a high-level overview of the **GKMIT_INSIDE** platform, illustrating how data moves between **external entities** (Employee and Admin), the **main system**, and the **MongoDB database**.

It highlights how both **Admin** and **Employee** users interact with the platform — for registration, posting, approvals, and content access — while the system handles core logic and persistent data management through **MongoDB**.

---

## Workflow of Level 0 Diagram

<!-- Importing image of DFD Level 0 -->

![DFD: Level - 0](assets/images/dfd-level-0.png){ width="2800" }

---

## Explanation

**Employee**

- Can register, log in, and create posts.
- All newly created posts remain in a _pending_ state until reviewed and approved by an Admin.

**Admin**

- Oversees user and post approvals, manages analytics.
- Admins ensure that only compliant and approved content is published.

**GKMIT INSIDE (System Process)**

- Acts as the **central application hub** — handling user authentication, post workflows, data validation, and communication between the user and the database.

**MongoDB Database**

- Serves as the **primary data store**, maintaining all persistent information such as users, posts, comments, reactions, bookmarks,  and activity logs.

---

## Summary

- This diagram represents the **Level 0 Context View** of the system.
- It shows external entities (Employee and Admin) and their high-level interactions with the central process, which in turn, exchanges and manages data through the **MongoDB databases**.
