# Industry 4.0 Production Line Simulator

An educational Unreal Engine 5 simulator showcasing the transition from Industry 3.0 to Industry 4.0 using a four-stage smart production line. Inspired by the **SMC FAS-200 SE testbed**, this project integrates real-time automation concepts, modular blueprint logic, and AI-generated assets via **404-GEN** to create a gamified training environment.

https://github.com/user-attachments/assets/4fabb535-701e-4460-9700-da684d81590f
![Screenshot (47)](https://github.com/user-attachments/assets/41ec8e34-fe0e-4928-ab4e-b3bc47d41a1a)
![Screenshot (46)](https://github.com/user-attachments/assets/ae9782a9-1988-489d-9222-325de885a5b9)
![Screenshot (48)](https://github.com/user-attachments/assets/33767628-8c3e-43b6-a06d-937d49e38d3a)
![Screenshot (49)](https://github.com/user-attachments/assets/84027650-979a-4e7e-9a0d-7dbaafe600fa)

> Developed by **Ashwin Ravikumar** at TIH-iHub Drishti Foundation, IIT Jodhpur.

---

## 🚀 Quick Start

### Prerequisites

- Unreal Engine 5.5
- Windows 10/11 64-bit
- 8 GB RAM minimum
- Dedicated GPU recommended

### Run the Project

```bash
# Clone the repository
https://github.com/E-Lucid-At0r/Ind_40_IITJ.git

# Open the .uproject file in Unreal Engine 5
# Click 'Play' to run the simulation.
```

---
**Google Drive Link Backup:** https://drive.google.com/file/d/1uRyI4Qb6F0Z5Wu5R2njhx3f0npDPXIpk/view?usp=drive_link

## 🧩 Project Structure (Modular Blueprint System)

Following the modular folder structure from [`Ind_40_IITJ`](https://github.com/E-Lucid-At0r/Ind_40_IITJ):

```
📁 Blueprints
├── Core
│   ├── BP_ProductionGameMode          # Controls game cycle, RP, analytics
│   ├── BP_SimulationManager           # Optional runtime coordinator
│   └── Structs (e.g., FPayload)       # Shared data types
│
├── Stations
│   ├── BP_Station_Base                # Parent station logic
│   ├── BP_Station_Generator           # Spawns base part
│   ├── BP_Station_Assembly            # Uses cobot or pneumatic actuator
│   ├── BP_Station_Handling            # Transfers part
│   └── BP_Station_QA                  # Vision inspection logic
│
├── Managers
│   ├── BP_ResearchManager             # Controls tech tree logic
│   ├── BP_AnalyticsManager            # Logs production stats
│   └── BP_MaintenanceManager          # Predictive/manual repair logic
│
📁 UI
├── WBP_ResearchTree                   # R&D interface
├── WBP_SCADA                          # Real-time dashboard
├── WBP_AnalyticsReport                # End-of-cycle summary
│
📁 Assets
├── 404GEN_Meshes                      # Imported AI-generated models
├── Materials
├── Animations
└── Prompts (reference prompts used with 404-GEN)
```

---

## 🧠 Blueprint Role Reference

| Blueprint               | Type      | Role                                                                  |
| ----------------------- | --------- | --------------------------------------------------------------------- |
| `BP_ProductionGameMode` | GameMode  | Central logic controller for game state, cycle control, RP system     |
| `BP_Station_Base`       | Actor     | Defines core station lifecycle (`StartStationCycle`, `PerformAction`) |
| `BP_Station_Assembly`   | Actor     | Handles lid placement, supports upgrades to cobot arm                 |
| `BP_ResearchManager`    | Actor     | Manages unlocks, timers, and research tree using DataTables           |
| `BP_AnalyticsManager`   | Actor     | Tracks energy, cycle time, defects, outputs reports                   |
| `BP_AIVisionComponent`  | Component | QA logic using height, color, and part detection                      |
| `BP_MaintenanceManager` | Component | Simulates predictive/manual maintenance based on wear cycle           |
| `WBP_ResearchTree`      | UI        | R&D upgrade system; timed and gated by prerequisites                  |
| `WBP_SCADA`             | UI        | Real-time visual feedback on system health, output, efficiency        |

---

## 📦 Asset Pipeline: 404-GEN Integration

This project uses **404-GEN**, a decentralized AI-based model generation system. Assets are generated using natural language prompts describing industrial parts and components.

### Example Prompts:

- "Pneumatic actuator with rear mounting brackets"
- "UR-3 style cobot with 6-axis rigging"
- "Industrial vision camera with casing"

### Workflow:

1. Prompt submitted to 404-GEN node
2. FBX received and reviewed
3. Imported into UE5 → Collision setup → Material assignment
4. Placed in `404GEN_Meshes` folder and linked via blueprints

---

![Screenshot (52)](https://github.com/user-attachments/assets/da1c37dd-bbf6-4601-8064-38216e0a65eb)
![Screenshot (51)](https://github.com/user-attachments/assets/631ca417-c406-4a00-9ab6-4e4ec99f5285)
![Screenshot (50)](https://github.com/user-attachments/assets/ca38d730-9f82-48b2-a403-9318307a8fd8)
![Screenshot (53)](https://github.com/user-attachments/assets/26cd4c7c-7e57-4eb4-85fb-1dedc08a209a)

## ⚙️ Modular Integration Notes

- All stations inherit from `BP_Station_Base`. To add a new station:

  1. Create a child blueprint
  2. Override `PerformAction()`
  3. Register in sequence inside `BP_ProductionGameMode`

- To add a new upgrade/technology:

  1. Add new row to `DT_ResearchUpgrades` (uses `FResearchTechRow` struct)
  2. Implement logic in `BP_ResearchManager`
  3. Broadcast event to affected station (`I_Upgradable` interface)

- Analytics, Maintenance, and Research systems are **fully decoupled** via events, allowing component-level reuse.

---

## 📈 Expansion Guidelines

To continue development:

- Add **warehouse or expedition modules** as new stations
- Develop **scenario-based missions** in GameMode (e.g., "Optimize energy", "Reduce defects")
- Extend the R&D tree with SCADA, AR, MES-like modules
- Hook SCADA outputs to external dashboards for classroom deployment

---

## 📫 Contact & Acknowledgments

**Ashwin Ravikumar**\
[📧 Email](mailto\:ashwin.ravikumar36@gmail.com)\
[🌐 Portfolio](https://theashfolio.com)\
[🔗 LinkedIn](https://linkedin.com/in/ashwin-ravikumar0306)

Project supported by **TIH-iHub Drishti Foundation, IIT Jodhpur**. Special thanks to **SMC Corporation** for their documentation on the FAS-200 SE testbed, which inspired this simulator.

---

## 📄 License

This project is intended for research and educational use. Please contact the author for reuse in academic or institutional training contexts.

