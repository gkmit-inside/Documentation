# DFD Level 2: Analytics & Dashboard

---

## Overview

The **Analytics & Dashboard** module is the central component for measuring platform performance and user engagement.  
It provides the **Admin** with quantitative insights necessary for strategic decision-making.

This module operates on a **Read-Only** principle, ensuring all core operational data stores (**USERS**, **POSTS**, **INTERACTIONS**) are accessed strictly for calculation and reporting purposes, without risk of modification.

---

## Workflow Explanation

The analytics workflow is structured around three sequential processes:  
**User Metrics Aggregation (P1)**, **Content & Engagement Aggregation (P2)**, and **Report Generation & Display (P3)**.

The dashboard view (**P3**) acts as the central orchestrator, triggering the necessary data aggregation before compiling the final output.

![DFD: Analytics & Dashboard](assets/images/analytics-dfd-level-2.png){ width="1900" height="1900" }

---

## 1. Report Generation & Display (P3)

This process initiates the data retrieval and is responsible for compiling and formatting the final visualization payload for the Admin.

1. **Admin → 14.0 Report Generation & Display (1) Request Dashboard View**  
   The Admin accesses the dashboard, initiating the entire analytics pipeline.

2. **14.0 Report Generation & Display → 12.0 User Metrics Aggregation (2) Request User Metrics**  
   P3 requests the core user statistics (e.g., total registered users).

3. **14.0 Report Generation & Display → 13.0 Content & Engagement Aggregation (3) Request C&E Metrics**  
   P3 simultaneously requests post and engagement metrics (e.g., comment counts, post volume).

4. **12.0 User Metrics Aggregation → 14.0 Report Generation & Display (6) User Metric Aggregates**  
   P3 receives the compiled user statistics from P1.

5. **13.0 Content & Engagement Aggregation → 14.0 Report Generation & Display (11) Content & Engagement Aggregates**  
   P3 receives the compiled content and interaction statistics from P2.

6. **14.0 Report Generation & Display → Admin (12) Structured Data Visualization Payload**  
   P3 combines all aggregates and formats the final payload for dashboard display.

---

## 2. User Metrics Aggregation (P1)

This process is dedicated to calculating metrics related to the platform’s user base.

1. **12.0 User Metrics Aggregation → D1: USERS (4) Read User Status (Total/Approved)**  
   P1 reads from the **USERS** collection to determine the total number of registered accounts and the count of approved, active users.

2. **D1: USERS → 12.0 User Metrics Aggregation (5) User Records**  
   The relevant user records are returned to P1 for calculation.

---

## 3. Content & Engagement Aggregation (P2)

This process calculates metrics related to the platform’s content volume and level of user interaction.

1. **13.0 Content & Engagement Aggregation → D2: POSTS (7) Read Post Status (Total/Approved)**  
   P2 reads post metadata from the **POSTS** collection to count total posts and the ratio of approved to pending content.

2. **D2: POSTS → 13.0 Content & Engagement Aggregation (8) Post Records**  
   The required post records are returned to P2.

3. **13.0 Content & Engagement Aggregation → D3/D4/D5 (9a, 9b, 9c) Read Interaction Data (Total/Trends)**  
   P2 reads from the **COMMENTS**, **REACTIONS**, and **BOOKMARKS** collections to gather total counts and time-series data for trends.

4. **D3, D4, D5 → 13.0 Content & Engagement Aggregation (10) Interaction Records**  
   The raw interaction records are returned to P2 for aggregation and trend calculation.

---

## Summary

- The **Analytics & Dashboard** system provides clear, data-driven insights to the Admin.
- The workflow is strictly **Read-Only**, ensuring zero impact on operational databases.
- By separating into **User (P1)** and **Content/Engagement (P2)** aggregation processes, the module enables modular development and efficient, focused data retrieval.
- The central **Report Generation (P3)** process orchestrates data collection and produces the final, actionable visualization payload for the dashboard.
