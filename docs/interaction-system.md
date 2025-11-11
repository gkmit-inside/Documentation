# DFD Level 2: Interaction System

---

## Overview

The **Interaction System** module is responsible for capturing all user engagement with published posts, including **comments**, **reactions**, and **bookmarks**.

This module is designed for both **security** and **scalability**, ensuring that all interactions are validated against existing posts before being logged into their respective database collections.

---

## Workflow Explanation

The interaction flow is divided into two main sequential processes — **Request Validation** and **Interaction Logging & Routing**.  
This approach centralizes the validation logic shared across all three interaction types.

![User MGMT DFD: Level - 2](assets/images/interaction-dfd-level-2.png){ width="1900" height="1900" }

---

### 1. Request Validation (P1)

This process ensures that any action taken by an Employee is legitimate and corresponds to an active post.

1. **Employee → 8.0 Request Validation (1) Interaction Request (Type, Post ID)**  
   The Employee initiates an interaction (e.g., comment, reaction, or bookmark) by sending the request type and target Post ID.

2. **8.0 Request Validation → POSTS (2) Read Post ID**  
   The system queries the **POSTS** collection using the provided Post ID to verify validity.

3. **POSTS → 8.0 Request Validation (3) Post Status / Existence Check**  
   The database confirms whether the post exists and is in an approved state.

4. **8.0 Request Validation → 9.0 Interaction Logging & Routing (4) Valid Request Details**  
   If valid, the request details are passed forward to the logging process.

5. **8.0 Request Validation → Employee (5) Invalid Request / Error Message**  
   If the Post ID is invalid or the post is unapproved, the system immediately returns an error message to the Employee.

---

### 2. Interaction Logging & Routing (P2)

Once validated, this process handles the actual data storage, routing each interaction type to the appropriate collection.

1. **9.0 Interaction Logging & Routing → COMMENTS (6a) Log Comment (CRUD)**  
   For comment interactions, the process performs Create, Read, Update, or Delete operations in the **COMMENTS** collection.

2. **9.0 Interaction Logging & Routing → REACTIONS (6b) Log Reaction (Toggle)**  
   For reactions, the system performs a toggle operation — adding or removing the reaction in the **REACTIONS** collection.

3. **9.0 Interaction Logging & Routing → BOOKMARKS (6c) Log Bookmark (Toggle)**  
   For bookmarks, the system toggles the bookmark status in the **BOOKMARKS** collection.

4. **COMMENTS / REACTIONS / BOOKMARKS → 9.0 Interaction Logging & Routing (7) Write Confirmation**  
   Each respective collection confirms that the write operation was successful.

5. **9.0 Interaction Logging & Routing → Employee (8) Update UI / Confirmation**  
   The system sends a final response to the Employee, updating the UI to reflect the interaction (e.g., displaying a new comment or toggled icon).

---

## Summary

- The **Interaction System** is optimized for efficiency and modular data handling.
- By consolidating **validation** into a single pre-processing step (P1), it eliminates redundant checks across modules.
- The use of **dedicated collections** — **COMMENTS**, **REACTIONS**, and **BOOKMARKS** — in the logging process (P2) enables scalable storage, high write-throughput, and specialized analytics queries.
- This design ensures consistent data integrity while maintaining real-time responsiveness for all user interactions.
