# DFD Level 2: Interaction System

---

## Overview

The **Interaction System** module is responsible for processing all user engagement with published content (Posts). It ensures that every action is validated against the post's status and correctly logged in the corresponding interaction data stores.

This system guarantees that only approved posts can be interacted with, maintaining the quality and integrity of the engagement data.

The module primarily interacts with **POSTS (Validation)**, **COMMENTS**, **REACTIONS**, and **BOOKMARKS** data stores.

---

## Workflow Explanation

The module is divided into two core processes:

- **Request Validation (P7.0)**: Checks if the post exists and is open for interaction.
- **Interaction Logging & Routing (P8.0)**: Executes the specific action (Comment, Like, Bookmark).

---

## Workflow of Interaction System Module

![Interaction DFD: Level - 2](assets/images/interaction-dfd-level-2.png){ width="1900" height="1900" }

---

## Request Validation (P7.0)

This flow validates the feasibility of the user's request (e.g., preventing a comment on a rejected post).

| Step | Data Flow                                                                  | Process         | Detail & Status                                                                                                                                    |
| ---- | -------------------------------------------------------------------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.   | Employee → 7.0 Request Validation (1) Interaction Request                  | Input           | The Employee sends an authenticated request containing the Type of interaction (Comment/React/Bookmark) and the Post ID.                           |
| 2.   | 7.0 Request Validation → POSTS (2) Read Post ID                            | Database Read   | The system reads the target post from the POSTS collection.                                                                                        |
| 3.   | POSTS → 7.0 Request Validation (3) Post Status / Existence Check           | Validation Data | The database returns the post record. The system checks if the post is `postStatus: "approved"` and has not been soft-deleted (`deletedAt: null`). |
| 4.   | 7.0 Request Validation → 8.0 Interaction Logging (4) Valid Request Details | Success Path    | If the post is valid, the request proceeds to the logging process.                                                                                 |
| 5.   | 7.0 Request Validation → Employee (5) Invalid Request / Error Message      | Failure Path    | If the post is not found or is not approved, the Employee receives an immediate error message.                                                     |

---

## Interaction Logging & Routing (P8.0)

This process logs the successful interaction into the correct collection based on the request type.

| Step | Data Flow                                                                         | Process            | Detail & Status                                                                                                                              |
| ---- | --------------------------------------------------------------------------------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.   | 7.0 Validation → 8.0 Interaction Logging (4) Valid Request Details                | Input              | The process receives the verified Post ID and Interaction Type.                                                                              |
| 2a.  | 8.0 Interaction Logging → COMMENTS (6a) Log Comment                               | Database Write     | If Type is Comment, a new document is created in the COMMENTS collection.                                                                    |
| 2b.  | 8.0 Interaction Logging → REACTIONS (6b) Log Reaction (Toggle)                    | Database Write     | If Type is React, the process toggles the record (creates or deletes) in the REACTIONS collection.                                           |
| 2c.  | 8.0 Interaction Logging → BOOKMARKS (6c) Log Bookmark (Toggle)                    | Database Write     | If Type is Bookmark, the process toggles the record in the BOOKMARKS collection.                                                             |
| 3.   | COMMENTS/REACTIONS/BOOKMARKS → 8.0 Interaction Logging (7a-7c) Write Confirmation | Write Confirmation | The database confirms the successful creation, deletion, or modification of the record.                                                      |
| 4.   | 8.0 Interaction Logging → Employee (8) Update UI / Confirmation                   | Output             | The Employee receives a final confirmation message, and the frontend updates the interaction count and button status (Optimistic UI update). |

---

## Process Summary

| Process                                    | Primary Interactor | Core Action                                       | Database Outcome                               |
| ------------------------------------------ | ------------------ | ------------------------------------------------- | ---------------------------------------------- |
| **7.0 Request Validation (Post ID Check)** | Employee           | Verify post existence and status.                 | Gate for unauthorized or invalid interactions. |
| **8.0 Interaction Logging & Routing**      | Employee           | Executes and logs the comment, like, or bookmark. | Logged record in COMMENTS/REACTIONS/BOOKMARKS. |
