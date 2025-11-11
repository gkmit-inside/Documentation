# **DFD Level 2 — Feed & Content Delivery**

---

## **Overview**

The **Feed & Content Delivery** module powers the Employee’s primary viewing experience.  
Its main goal is to ensure **fast**, **secure**, and **personalized** delivery of approved content — enriched with real-time engagement metrics like **comments**, **reactions**, and **bookmarks**, along with user-specific interaction states.

This workflow operates in two sequential phases — **content filtering** and **content enrichment** — to optimize performance and ensure dynamic, up-to-date results.

---

## **Workflow Explanation**

![DFD: Level - 2 (Feed & Content Delivery)](assets/images/feed-dfd-level-2.png){ width="1900" height="1900" }

The feed delivery pipeline consists of two main processes:

1. **Fetch, Filter & Search Posts (P1)**
2. **Content Augmentation (P2)**

This two-stage design first retrieves and filters approved posts, then enriches them with real-time engagement data for final display.

---

### **1. Fetch, Filter & Search Posts (P1)**

This process retrieves the initial set of approved post records based on user actions — either a general feed request or a targeted search.

| Step  | Flow Description                                                                                                               |
| ----- | ------------------------------------------------------------------------------------------------------------------------------ |
| **1** | **Employee → Fetch, Filter & Search Posts:** Initiates a feed or search request.                                               |
| **2** | **P1 → POSTS (Approved Content):** Queries `POSTS` collection applying filters (e.g., approval status, chronology, relevance). |
| **3** | **POSTS → P1:** Returns filtered and approved post records.                                                                    |
| **4** | **P1 → Content Augmentation:** Passes curated base post records for enrichment.                                                |

---

### **2. Content Augmentation (P2)**

This process enhances the filtered posts with engagement metrics and user-specific interaction data.

| Step  | Flow Description                                                                                                                |
| ----- | ------------------------------------------------------------------------------------------------------------------------------- |
| **5** | **P2 → ENGAGEMENT & STATUS DATA:** Fetches related engagement data (from `COMMENTS`, `REACTIONS`, and `BOOKMARKS` collections). |
| **6** | **ENGAGEMENT & STATUS DATA → P2:** Returns aggregated metrics and user-specific flags (e.g., hasLiked, isBookmarked).           |
| **7** | **P2 → Employee:** Sends the final enriched feed payload back to the client for real-time display.                              |

---

## **Summary**

The **Feed & Content Delivery** module employs a **two-phase architecture** for optimized performance and scalability.

- **Filtering (P1)** isolates and retrieves only approved, relevant posts.
- **Augmentation (P2)** enriches content with **real-time engagement data** and **personalized interaction states**.

This modular approach ensures Employees receive a **fast**, **comprehensive**, and **dynamic** feed — always reflecting the most current and relevant platform activity.

---
