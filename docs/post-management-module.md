# **DFD Level 2: Post Management**

---

## Overview

The **Post Management** module is the content quality gatekeeper for the GKMIT-INSIDE platform. It handles the content lifecycle, ensuring all submitted material is reviewed and approved by an Admin before publication.

It manages the creation, deletion, and approval of all posts.

The module primarily interacts with the **POSTS (MongoDB)** data store, which tracks post records and status (pending/approved/rejected).

---

## Workflow Explanation

The module is divided into two core processes:

*   **Post Submission (P3.0)**: Initial creation by the Employee.
*   **Admin Review & Decision (P4.0)**: Content moderation by the Admin.

---

## Workflow of Post Management Module

![Post DFD: Level - 2](assets/images/post-dfd-level-2.png){ width="2900" height="2600" }

---

## Post Submission (P3.0)

This flow describes how an **Employee** submits new content using the `CreatePost.jsx` component.

| Step | Data Flow                                     | Process        | Detail & Status                                                                               |
| ---- | --------------------------------------------- | -------------- | --------------------------------------------------------------------------------------------- |
| 1    | Employee → 3.0 Post Submission (1) Post Data  | Input          | The Employee sends post content (Title, Description, Image File, etc.) via the POST request. |
| 2    | 3.0 Post Submission → POSTS (2) Create Record | Database Write | The process creates a new document in the **POSTS** collection, automatically setting the `postStatus` to "pending". |
| 3    | 3.0 Post Submission → Employee (3) Confirmation | Output         | The Employee receives a success message ("Post created successfully. Awaiting admin approval."). |

---

## Admin Review & Decision (P4.0)

This flow is managed by the **Admin** through the Post Management dashboard tabs.

| Step | Data Flow                                                   | Process        | Detail & Status                                                                                                   |
| ---- | ----------------------------------------------------------- | -------------- | ----------------------------------------------------------------------------------------------------------------- |
| 1    | Admin → 4.0 Admin Review & Decision (4) Request Pending Posts | Input          | The Admin requests a list of posts awaiting review via the Admin dashboard. |
| 2    | 4.0 Admin Review & Decision → POSTS (5) Read Pending Posts    | Database Read  | The process queries the **POSTS** collection for records where `postStatus` is "pending".                               |
| 3    | POSTS → 4.0 Admin Review & Decision (6) Pending Post Details  | Data Return    | The database returns the pending posts to the Admin table for review.                                             |
| 4    | Admin → 4.0 Admin Review & Decision (7) Approve / Reject Action | Input          | The Admin chooses to Approve or Reject a post via the action buttons.                                             |
| 5    | 4.0 Admin Review & Decision → POSTS (8) Update Status         | Database Write | The process updates the record, changing `postStatus` to "approved" or "rejected", and sets the `approvedAt` timestamp. |
| 6    | 4.0 Admin Review & Decision → Admin (9) Dashboard Update / Confirmation | Output         | The Admin confirms the successful status change and the post is removed from the pending queue.                     |

---

## Process Summary

| Process                         | Primary Interactor | Core Action                   | Database Outcome                                   |
| ------------------------------- | ------------------ | ----------------------------- | -------------------------------------------------- |
| **3.0 Post Submission**         | Employee           | Submit content to moderation  | New record created with `postStatus: pending`      |
| **4.0 Admin Review & Decision** | Admin              | Approve/Reject Content Visibility | `postStatus` updated to `approved` or `rejected` |

---

## Summary

-   The **Post Management** module acts as the **content quality gatekeeper** for the GKMIT_INSIDE platform.
-   It enforces a structured flow where Employees focus on content creation, while Admins maintain governance and moderation.
-   Through explicit approval workflows, it ensures that only reviewed and authorized posts reach the main feed.
-   This separation of duties maintains platform integrity, promotes accountability, and supports transparent publication control.
-   Ultimately, it forms a vital bridge between **content creation** and **content governance** within the system.
