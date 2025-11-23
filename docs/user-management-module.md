# DFD Level 2: User Management

---

## Overview

The **User Management** module serves as the administrative gatekeeper for the GKMIT-INSIDE platform. Its primary function is to enforce and track user authorization, ensuring that only approved personnel can access the core application features.

This module exclusively handles administrative tasks related to user status:

*   **Retrieval**: Fetching lists of pending and approved users.
*   **Approval**: Updating a user's status to grant or revoke access.

The module interacts solely with the **USERS (MongoDB)** data store.

---

## Workflow Explanation

The module is divided into two core processes, managed entirely by the Admin:

*   **User Data Retrieval & Search (P5.0)**: Fetches the required lists of users based on their status.
*   **User Status Update (Approval) (P6.0)**: Executes the final approval or rejection decision.

---

## Workflow of User Management Module

![User MGMT DFD: Level - 2](assets/images/user-dfd-level-2.png){ width="1000" height="1000" }

---

## User Data Retrieval & Search (P5.0)

This flow describes how the Admin populates the User Management dashboard tabs (Pending and Approved).

| Step | Data Flow                                        | Process       | Detail & Status                                                                                                   |
| ---- | ------------------------------------------------ | ------------- | ----------------------------------------------------------------------------------------------------------------- |
| 1    | Admin → 5.0 User Data Retrieval (1) Request All / Pending Users | Input         | The Admin selects a tab (e.g., 'Pending') which triggers a request to fetch users by status (`GET /api/admin/users?status=pending`). |
| 2    | 5.0 User Data Retrieval → USERS (2) Read All User Records       | Database Read | The process queries the **USERS** collection for records matching the requested status (`isApproved: false` for pending). |
| 3    | USERS → 5.0 User Data Retrieval (3) All User Data           | Data Return   | The database returns the user records, including essential fields like name, email, and `isApproved` status.      |
| 4    | 5.0 User Data Retrieval → Admin (4) Display List            | Output        | The dashboard displays the retrieved users in a tabular list, ready for administrative action.                      |

---

## User Status Update (Approval) (P6.0)

This flow describes how the Admin executes an action that changes a user's access status.

| Step | Data Flow                                       | Process        | Detail & Status                                                                                                                              |
| ---- | ----------------------------------------------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | Admin → 6.0 User Status Update (5) User ID + Action | Input          | The Admin clicks "Approve" or "Reject" on a user, sending the target user's `_id` and the desired new status (approved or pending).        |
| 2    | 6.0 User Status Update → USERS (6) Update 'isApproved' Status | Database Write | The process updates the user's record in the **USERS** collection. If approved, `isApproved` is set to `true` and the `approvedAt` timestamp is recorded. |
| 3    | 6.0 User Status Update → Admin (7) Success Message  | Output         | The Admin receives confirmation (via toast/optimistic UI update) that the user's status has been successfully updated, and the user disappears from the current list. |

---

## Process Summary

| Process                          | Primary Interactor | Core Action                      | Database Outcome                                     |
| -------------------------------- | ------------------ | -------------------------------- | ---------------------------------------------------- |
| **5.0 User Data Retrieval & Search** | Admin              | Fetch user lists by status.      | Retrieve user records.                               |
| **6.0 User Status Update (Approval)** | Admin              | Grant or revoke user platform access. | Update `isApproved` status and approval timestamp. |

---

## Summary

-   The **User Management** module has a simple but critical governance function. By limiting its capabilities to reading user data and updating the binary approval flag, it centralizes system-level access control.
-   This design ensures that no user can access the main application features without explicit administrative approval.
-   It maintains strict oversight of user onboarding and upholds security and operational integrity across the GKMIT_INSIDE platform.
