# EcoTrack: Smart E-Waste Collection & Recycling Network

> **DBMS Course-Based Project (CBP) Prototype**  
> *A normalized, full-featured web application demonstrating circular economy supply chain management, relational integrity, transaction simulation, and environmental sustainability telemetry.*

---

## 🌿 Project Overview

**EcoTrack** is a centralized platform designed to solve the critical urban challenge of electronic waste (e-waste). Built to conform with the statutory requirements of the **Central Pollution Control Board (CPCB) E-Waste Management Rules 2022**, the platform orchestrates the end-to-end lifecycle of discarded electronics:
1. **Intake & Logistics**: Citizens and enterprises schedule doorstep collection requests with verified quantity and hazard categorization.
2. **Intermediate Warehousing**: Municipal Collection Centers receive and verify batch manifests, managing volumetric capacity thresholds.
3. **Certified Material Recovery**: Authorized Recycling Facilities disassemble, pyrometallurgically refine, and granulate secondary raw materials (e.g., Copper, Gold, High-Purity Engineering Plastics).
4. **Incentivization Ledger**: Transactional credit awards (10 Eco-Credits per 1.0 kg recycled) encourage active citizen participation with strict duplicate-award prevention.

---

## 🗄️ Relational DBMS Architecture (7 Entities)

EcoTrack models a normalized Third Normal Form (3NF) relational schema comprising seven distinct entities:

| # | Entity / Relation | Primary Key | Foreign Keys | Business Description |
|---|---|---|---|---|
| **1** | `User` | `user_id` | *None* | Citizen profiles, contact credentials, and accumulated incentive credits balance. |
| **2** | `E_Waste_Category` | `category_id` | *None* | Standard electronic waste taxonomy with statutory toxic hazard classifications (High / Medium / Low). |
| **3** | `Collection_Center` | `center_id` | *None* | Physical intake depots with registered storage limits (Tons) and contact points. |
| **4** | `Pickup_Request` | `request_id` | `user_id`, `category_id`, `center_id` | Operational collection manifests tracking quantities (kg), schedules, and pipeline status. |
| **5** | `Recycling_Facility` | `facility_id` | *None* | Certified industrial plants with specialized pyro/hydro material processing capacity. |
| **6** | `Recycled_Material` | `material_id` | `request_id`, `facility_id` | Recovered secondary commodities extracted from recycled electronic batches. |
| **7** | `Administrator` | `admin_id` | *None* | Environmental officers, logistics superintendents, and compliance auditors. |

---

## 📊 Simulated Relational Query Reports

The application provides an interactive **Database Insights & Reports** module showcasing standard SQL relational semantics executed in-memory over live application data:

1. **Pending Pickup Requests with Citizen & Center Details**:
   - *Technique*: Multi-Table `INNER JOIN` linking `pickup_requests`, `users`, and `collection_centers` with `WHERE status = 'Pending'`.
2. **Total Collected Waste Aggregated by Collection Center**:
   - *Technique*: `GROUP BY` with aggregate `SUM()` and `COUNT()` over intake manifests.
3. **Citizens with More Than 100 Eco-Credits**:
   - *Technique*: Filter condition (`WHERE credits > 100`) with descending order (`ORDER BY credits DESC`).
4. **High-Hazard E-Waste Categories Analysis**:
   - *Technique*: Filter on `hazard_level = 'High'` with cumulative intake summation.
5. **Recovered Raw Materials Grouped by Processing Facility**:
   - *Technique*: Multi-table `JOIN` across facilities and recovered secondary commodities.
6. **Collection Centers Capacity & Intake Utilization**:
   - *Technique*: Derived volumetric ratio (`kg` to `tons` conversion: $\text{Tons} = \text{kg} / 1000$) and capacity threshold alerts.

---

## 🚀 Key Features

- **Executive Sustainability Dashboard**: Dynamic metric cards for registered users, total requests, waste collected (kg), waste recycled (kg), pending requests, and total credits. Visual category charts and environmental impact telemetry (CO₂ saved, toxic metals diverted, trees equivalent).
- **Schedule a Pickup**: Validated form with real-time credit calculation, citizen quick-fill shortcuts, positive quantity enforcement, and immediate manifest generation.
- **Pickup Request Pipeline**: Searchable and filterable management table with status actions (`Pending` ➔ `Collected` ➔ `Recycled`).
- **Transactional Credit Safety**: Automatically awards 10 Eco-Credits per kg when transitioned to `Recycled`. Safeguarded against double-counting via immutable flags (`credits_awarded: true`).
- **Citizen Rewards & History**: Detailed user profiles, recycling history timeline modal, and demonstration credit redemption catalog.
- **Collection Centers with Storage Gauge**: Visual capacity utilization bars with accurate kg-to-ton conversion.
- **Recycling Facilities & Recovered Materials**: Secondary material inventory (e.g. Copper 8 kg, Plastic 12 kg for Request #1003) with batch logging.
- **Demo Controls & Administration**: Administrative view toggle, database JSON dump download, and confirmed one-click reset to initial CBP sample dataset.

---

## 🛠️ Technology Stack

- **Frontend Library**: React 18
- **Build Tool**: Vite 6 (Ultra-fast HMR and optimized production bundles)
- **Styling**: Modern Vanilla CSS (Environmental Forest Green Design System)
- **Icons**: Lucide React
- **Data Engine**: HTML5 `localStorage` (persistent across refreshes, zero external DB installation required)

---

## 💻 Quick Start & Run Instructions

### Prerequisites
- Node.js (v18+ or v20+)
- npm installed

### 1. Install Dependencies
```bash
npm install
```

### 2. Start the Development Server
```bash
npm run dev
```
The application will launch at:  
👉 **`http://localhost:3000`**

### 3. Production Build & Verification
```bash
npm run build
npm run preview
```

---

## 📋 Preloaded Demonstration Dataset

On first launch, the prototype automatically seeds the official CBP scenario data:
- **Citizens**:
  - `Ravi Kumar` (Hyderabad, 150 Credits)
  - `Sneha Reddy` (Pune, 80 Credits)
  - `Amit Shah` (Mumbai, 200 Credits)
- **Sample Manifests**:
  - `Req #1001`: 15 kg IT Equipment (Collected)
  - `Req #1002`: 2 kg Home Appliances (Pending)
  - `Req #1003`: 25 kg Mobile Devices (Recycled)
- **Intake Centers**:
  - `Green E-Cycle` (Hyderabad, 50 Tons Capacity)
  - `EcoTech Collect` (Pune, 30 Tons Capacity)
- **Processing Facilities**:
  - `MetalRecover Inc` (Hyderabad, 100 Tons Capacity)
  - `PolyRecycle Ltd` (Pune, 80 Tons Capacity)
- **Recovered Materials**:
  - `Copper` (8 kg) and `Plastic` (12 kg) associated with Request #1003.

---

## 📜 Faculty Evaluation Notes

- **Zero Hardcoded Totals**: Every statistic on the dashboard and query reports is calculated in real time directly from the underlying data array.
- **Data Persistence**: Refreshing the browser preserves all newly added requests, citizens, or centers. Use the red **"Reset Demo Data"** button to restore the clean baseline anytime.
- **Demonstration Notice**: Administrative mode is intentionally unlocked with a one-click toggle to facilitate frictionless demonstration during viva examination.
