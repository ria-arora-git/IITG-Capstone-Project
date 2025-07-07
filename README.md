# IITG-Capstone-Project

# 🚗 Dynamic Pricing for Urban Parking Lots

**Capstone Project | Summer Analytics 2025**  
Hosted by Consulting & Analytics Club × Pathway

---

## 📌 Overview

Urban parking lots often operate with static pricing, leading to underutilization during low demand and overcrowding during high demand. This project builds a **real-time dynamic pricing engine** for 14 parking spaces based on demand signals, competition, and traffic conditions.

The system simulates data streaming and adjusts parking prices using intelligent logic — from simple occupancy-based adjustments to a competitor-aware rerouting mechanism.

---

## 🛠 Tech Stack

| Tool            | Purpose                               |
|-----------------|---------------------------------------|
| **Python**      | Core programming language             |
| **NumPy**       | Numerical computations                |
| **Pandas**      | Data manipulation & feature extraction|
| **Pathway**     | Real-time data streaming simulation   |
| **Bokeh**       | Interactive visualization             |
| **Google Colab**| Coding & deployment environment       |

---

## 🧠 Project Models

The pricing engine is built in **3 progressively complex models**:

1. **Model 1: Baseline Linear Model**
   - Price increases linearly with occupancy.
   - Formula:  
     \[
     P_{t+1} = P_t + \alpha \cdot \frac{\text{Occupancy}}{\text{Capacity}}
     \]

2. **Model 2: Demand-Based Model**
   - Price is based on a demand function including:
     - Occupancy, Queue Length, Traffic, Special Days, Vehicle Type.
   - Uses sigmoid-normalized demand:
     \[
     \text{Demand} = \alpha_d \cdot \text{occ} + \beta_d \cdot \text{queue} - \gamma_d \cdot \text{traffic} + \delta_d \cdot \text{special} + \epsilon_d \cdot \text{vehicle}
     \]
     \[
     \text{Price}_t = \text{BasePrice} \cdot \left(1 + \lambda_d \cdot \frac{1}{1 + e^{-\text{Demand}}}\right)
     \]

3. **Model 3: Competitive Pricing + Rerouting**
   - Incorporates:
     - Geographic proximity
     - Nearby lot pricing
     - Rerouting suggestions if lot is full and cheaper nearby options exist.

---

## 🏗 Architecture Diagram

```mermaid
flowchart TD
    A[Raw Parking Data (CSV)] -->|Streamed with Delay| B(Pathway Streaming Engine)
    B --> C[Real-Time DataFrame]
    C --> D[Model 1: Baseline Linear Pricing]
    C --> E[Model 2: Demand-Based Pricing]
    C --> F[Model 3: Competitor-Aware Pricing]
    F --> G[Rerouting Logic]
    F --> H[Visualization with Bokeh]
    E --> H
    D --> H
    H --> I[Dashboard Output]
