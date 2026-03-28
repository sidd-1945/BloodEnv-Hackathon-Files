# 🩸 BloodEnv: Autonomous Perishable Logistics
**Submission for Meta x Hugging Face OpenEnv Hackathon**

## 🏥 The Real-World Problem: The "Cold-Chain" Crisis
Blood is a **hyper-perishable asset** with a rigid 42-day shelf life. Every year, thousands of units are discarded due to expiration in one facility, while neighboring trauma centers face critical shortages. Traditional static logistics fail to balance the "buffer vs. waste" equation in real-time, especially across decentralized hospital networks.

## 🤖 The Agentic Solution
**BloodEnv** is a high-stakes, OpenAI Gym-compatible environment designed for autonomous logistics agents. The agent acts as a **Regional Logistics Controller** managing a 5-hospital grid. It must solve the complex trade-off between keeping enough stock to save lives and moving stock fast enough to prevent biological waste.

### ⚙️ State & Action API Structure
The environment provides a granular interface for reinforcement learning:

* **Observation Space (State):** A multi-dimensional tensor representing:
    * **Inventory Age Profile:** Units remaining categorized by days until expiration ($d_{1}$ to $d_{42}$).
    * **Demand Forecast:** Stochastic signals representing predicted surgical and emergency needs.
    * **Transit Pipeline:** Units currently in motion between facilities.
* **Action Space:** a continuous/discrete vector representing:
    * **Transshipment:** Moving $X$ units from Hospital $A$ to Hospital $B$.
    * **Procurement:** Ordering new units from central donation hubs.

### 📈 Scoring & Logistical Efficiency
The agent is evaluated on a normalized scale from **0.0 to 1.0**:

| Score | Logistical Meaning |
| :--- | :--- |
| **1.0 (Optimal)** | **Perfect Cycle:** 100% demand fulfillment with zero units expired. |
| **0.7 - 0.9** | **Efficient:** High fulfillment, but minor wastage due to over-stocking. |
| **0.4 - 0.6** | **Sub-Optimal:** Significant "Outdates" (wastage) or minor "Shortfalls" (unmet demand). |
| **< 0.3** | **Critical Failure:** High shortages (emergency risk) or systemic logistics collapse. |

## 🚀 Deployment & Usage
This repository is configured for immediate deployment to **Hugging Face Spaces** using the OpenEnv orchestrator.

1.  **Environment Manifest:** See `openenv.yaml` for task definitions (Easy, Medium, Hard).
2.  **Containerization:** The included `Dockerfile` ensures a lightweight, reproducible Python 3.10 environment.
3.  **Local Evaluation:** ```bash
    pip install -r requirements.txt
    python eval_baseline.py
    ```

---
*Built with ❤️ for the Meta x Hugging Face OpenEnv Hackathon.*