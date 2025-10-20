# 🚀 Automated Ticket Assignment for ABC Corporation (ServiceNow)

**Team ID:** 160664

This repository documents the implementation, configuration blueprints, and code snippets for the **automated ticket routing solution** for Operations Tickets within ABC Corporation's ServiceNow instance.

The objective was to transition from manual ticket triage to an intelligent, criteria-based assignment system, significantly boosting operational efficiency and reducing Mean Time To Resolution (MTTR).

---

## 🎯 Key Project Goals

| Goal | Description | Status |
| :--- | :--- | :--- |
| **Automation** | Develop an automated, criteria-based distribution mechanism in ServiceNow Flow Designer. | ✅ Complete |
| **Efficiency** | Instantly route tickets to the correct support group (`Certificate Group`, `Platform Group`). | ✅ Complete |
| **Security** | Implement role-based ACLs to govern and secure the core assignment configuration. | ✅ Complete |
| **Optimization** | Optimize resource utilization within the support department by reducing manual triage overhead. | ✅ Complete |

---

## 🛠️ Technology Stack & Skills

This solution is built entirely on the **ServiceNow Platform**.

| Component | Purpose |
| :--- | :--- |
| **ServiceNow** | Platform hosting the solution. |
| **Flow Designer** | Core tool for building the decision-making and assignment automation logic (two dedicated Flows). |
| **ACLs (Access Control Lists)** | Ensures security and governance over the custom table configuration data. |
| **Custom Table** | `u_operations_related` table used for centralized ticket data and assignment configuration. |

---

## 📦 Implementation Components

### 1. Automation Logic (ServiceNow Flow Designer)

The assignment process is managed by **two separate, dedicated Flows**, each triggered by specific criteria on the ticket's **`Issue`** field. Both flows use the **`create or update a record`** trigger on the **`Operations related`** table.

#### **Flow 1: "Regarding Certificate"**
* **Trigger Condition:** `Issue` is **`Regrading Certificates`**.
* **Action:** Updates the record's **`Assigned to group`** field to **`Certificates`**.

#### **Flow 2: "Regarding Platform"**
* **Trigger Conditions (OR Logic):**
    * `Issue` is **`Unable to login to platform`**
    * `Issue` is **`404 Error`**
    * `Issue` is **`Regrading User expired`**
* **Action:** Updates the record's **`Assigned to group`** field to **`Platform`**.

### 2. Data Structure and Configuration

| Component | Detail | Purpose |
| :--- | :--- | :--- |
| **Custom Table** | `u_operations_related` | The table where the Flows are triggered and the `Issue` field holds the routing criteria. |
| **Assignment Groups**| `Certificate Group`, `Platform Group` | The two primary support teams. |
| **Custom Roles** | `Certification_role`, `Platform_role` | Used for defining user access and security permissions. |

### 3. Security and Governance (ACLs)

To maintain configuration integrity, record-level security was applied to the `u_operations_related` table.

* **Objective:** Restrict who can modify the routing configuration data.
* **Implementation:** A record-level **write ACL** is applied, granting access to modify the assignment mapping to the **`Certification_role`, `Platform_role`** roles and System Administrators.

---

## 📂 Repository Structure

| Directory/File | Description |
| :--- | :--- |
| `/documentation` | Project charter, requirements, design documents, and final sign-off documentation. |
| `/configuration` | XML/Update Sets for the custom table schema (`u_operations_related`) and related data policies. |
| `/blueprints` | Screenshots and configuration steps for the Flow Designer logic and custom ACLs. |
| `/code` | Any server-side scripts (Business Rules, Script Includes) used to support this solution (if applicable). |
| `README.md` | This overview file. |
