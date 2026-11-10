# 🖥️ OS Resource Allocation Intelligence & Deadlock Simulator



An interactive, browser-native operating system kernel simulator designed to model multi-instance resource contention, render real-time **Resource Allocation Graphs (RAG)**, execute **Work-Finish / Banker's safety reduction**, and evaluate **explainable deadlock recovery heuristics**.

🔗 **Live Deployed Application:** https://shetesaha-create.github.io/OS_Deadlock_Simulator/  
📂 **Source Code Repository:** https://github.com/shetesaha-create/OS_Deadlock_Simulator

---

## ✨ Core Architecture & Features

* **Interactive Multi-Instance RAG Engine:** Renders system resource classes (`R0: MutexLocks`, `R1: DBConnections`, `R2: DiskBuffers`), instance occupancy tokens, solid green allocation edges ($R_j \rightarrow P_i$), and dashed amber request edges ($P_i \rightarrow R_j$).
* **Live OS Resource Dispatcher:** Supports manual kernel interventions (`Request`, `Allocate`, `Release`), dynamic process spawning with custom scheduling priorities ($\Pi_i \in [1, 10]$), and runtime resource class creation.
* **Work-Finish Deadlock Detection:** Evaluates state safety in $O(m \cdot n^2)$ time upon every state transition, isolating exact deadlocked process subsets without falsely flagging non-contending processes.
* **Explainable Heuristic Recovery Engine:** Quantifies and ranks candidate interventions across **Resource Preemption** (single-instance rollback) and **Process Termination** (full process abort) using an explicit priority- and holding-weighted cost model.
* **Real-Time Comparative Telemetry (Chart.js):**
  * *Process Allocation vs. Pending Requests:* Grouped bar chart comparing held instances against outstanding request queues per process.
  * *Recovery Strategy Cost & Rollback Impact:* Horizontal bar chart benchmarking preemption overhead against process termination penalties.

---

## 🧮 Mathematical Formulation

### 1. Kernel State Tuple
At discrete step $t$, the system state over $n$ processes and $m$ resource classes is defined by $S(t) = (E, V, A, Q, \Pi)$, where $E \in \mathbb{Z}_{\ge 0}^m$ is the total resource vector, $A \in \mathbb{Z}_{\ge 0}^{n \times m}$ is the allocation matrix, $Q \in \mathbb{Z}_{\ge 0}^{n \times m}$ is the pending request matrix, and $V_j = E_j - \sum_{i=0}^{n-1} A_{i,j}$ is the available vector.

### 2. Explainable Recovery Cost Functions
For every deadlocked process $P_i \in D$:
* **Single-Instance Resource Preemption Cost ($A_{i,j} > 0$):**
  $$C_{\text{preempt}}(P_i, R_j) = \max\left(4, \; 3\Pi_i - 2j + 2A_{i,j}\right)$$
* **Full Process Termination Cost:**
  $$C_{\text{term}}(P_i) = 9\Pi_i + 5\sum_{j=0}^{m-1} A_{i,j}$$

---

## 📊 Preset Contention Scenarios

1. **Safe State (Banker's Ideal):** Non-cyclic allocation where all requests are satisfiable via a verified safe execution sequence.
2. **Classic Circular Wait (2P, 2R):** Mutual single-instance deadlock between `P0 (AuthService)` and `P1 (PaymentGate)`.
3. **Unsafe State Warning:** High-contention state demonstrating deadlock escalation upon additional resource requests.
4. **Complex Multi-Instance Deadlock:** Multi-instance circular wait across `P0, P1, P2` while `P3 (AuditLogger)` remains unblocked.

---

## 💻 Running Locally

No external build tools or local servers are required:

```bash
git clone [https://github.com/shetesaha-create/OS_Deadlock_Simulator.git](https://github.com/shetesaha-create/OS_Deadlock_Simulator.git)
cd OS_Deadlock_Simulator
# Open index.html directly in any modern web browser
```

---

## 👩‍💻 Author

**Shraoshi Saha**  
Department of Computer Science and Engineering  
Faculty of Engineering and Technology, Jain University
