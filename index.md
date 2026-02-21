---
layout: default
title: openlane-guide
---

# 🛠 OpenLane Guide — Repository Index

This repository **must be read in order**.  
⚠️ It is **intentionally strict**.

If you jump around, you will **recreate the exact failures** this guide exists to prevent.

[![Go to Portal (EN)](https://img.shields.io/badge/Go%20to%20Portal-6F42C1?style=for-the-badge&logo=homeassistant&logoColor=white)](https://samizo-aitl.github.io/portal/en/)

---

## 🔗 Links

| Language | GitHub Pages 🌐 | GitHub 💻 |
|----------|----------------|-----------|
| EN English | [![GitHub Pages EN](https://img.shields.io/badge/GitHub%20Pages-English-brightgreen?logo=github)](https://samizo-aitl.github.io/openlane-guide/) | [![GitHub Repo EN](https://img.shields.io/badge/GitHub-English-blue?logo=github)](https://github.com/Samizo-AITL/openlane-guide) |

---

## 🧱 Phase 1 — Environment Survival (Mandatory)

> **Goal:**  
> Build an OpenLane environment that **does not break**,  
> **can be reproduced**, and **can be restored after failure**.

| Step | Document | Purpose |
|-----:|----------|---------|
| 01 | [01_WSL_Docker_Setup.md](./01_WSL_Docker_Setup.md) | 🐧 WSL2 + Docker Desktop setup for stability and export/import survivability |
| 02 | [02_OpenLane1_Setup.md](./02_OpenLane1_Setup.md) | 🧊 Install and **freeze** OpenLane1 (Makefile-based, production flow) |
| 03 | [03_OpenLane2_Setup.md](./03_OpenLane2_Setup.md) | 🧪 OpenLane2 for **evaluation only** — strict isolation |
| 04 | [04_PDK_Setup.md](./04_PDK_Setup.md) | 🧬 PDK is an **asset** — pin version, build once, never casually rebuild |
| 05 | [05_Verification_Test.md](./05_Verification_Test.md) | ✅ Smoke tests proving toolchain, PDK, and environment correctness |
| 06 | [06_Migration_WSL_Export.md](./06_Migration_WSL_Export.md) | ♻️ Disaster recovery via WSL export/import |
| 07 | [07_Troubleshooting.md](./07_Troubleshooting.md) | 🧯 Failure **prevention** checklist (not a fix-it guide) |

---

## 🧭 Phase 2 — Physical Design Reality

> **Goal:**  
> Understand where RTL assumptions **collapse into physical constraints**.

| Step | Document | Focus |
|-----:|----------|-------|
| 08 | [08_Placement.md](./08_Placement.md) | 📐 Placement fundamentals: density, legalization, convergence |
| 09 | [09_CTS.md](./09_CTS.md) | ⏱ Clock Tree Synthesis: skew, insertion delay |
| 10 | [10_Routing.md](./10_Routing.md) | 🧵 Global & detailed routing, congestion, DRC pressure |
| 11 | [11_STA.md](./11_STA.md) | 📊 STA: WNS/TNS, setup/hold, uncertainty |
| 12 | [12_GLS.md](./12_GLS.md) | 🔍 Gate-level simulation **without SDF** — limits and blind spots |
| 13 | [13_SDF_GLS.md](./13_SDF_GLS.md) | ⏳ SDF-annotated GLS — timing becomes behavior |

---

## 🔗 Phase 3 — Integration and Timing Truth

> **Goal:**  
> Align **tool output**, **timing analysis**, and **physical reality**.

| Step | Document | Insight |
|-----:|----------|---------|
| 14 | [14_OpenROAD_STA.md](./14_OpenROAD_STA.md) | 🧠 Using OpenROAD + STA without dead ends |
| 15 | [15_Routing_and_Congestion.md](./15_Routing_and_Congestion.md) | 🚦 Congestion analysis and routing strategy |
| 16 | [16_GLS_and_SDF.md](./16_GLS_and_SDF.md) | 🔁 RTL vs GLS vs SDF-GLS — what “matches” means |
| 17 | [17_Magic_KLayout_Reality_Check.md](./17_Magic_KLayout_Reality_Check.md) | 🪞 What layout viewers show — and hide |
| 18 | [18_STA_Reality_and_Timing_Closure.md](./18_STA_Reality_and_Timing_Closure.md) | 🧩 Timing closure mindset and rollback discipline |
| 19 | [19_GLS_SDF_Timing.md](./19_GLS_SDF_Timing.md) | 📉 Timing failure signatures visible only in waveforms |
| 20 | [20_Environment_Failure_Model.md](./20_Environment_Failure_Model.md) | 💥 Why OpenLane environments collapse |
| 21 | [21_Final_Rules_of_Survival.md](./21_Final_Rules_of_Survival.md) | 🛡 Non-negotiable survival rules |

---

## 📚 Appendices — Hard-Earned Knowledge

> Real failures. Real scars. No theory.

- 📌 [APPENDIX_GLS_Failure_Patterns.md](./APPENDIX_GLS_Failure_Patterns.md)
- 📌 [APPENDIX_PDK_Mismatch_Anatomy.md](./APPENDIX_PDK_Mismatch_Anatomy.md)
- 📌 [APPENDIX_OpenLane1_vs_OpenLane2_Separation.md](./APPENDIX_OpenLane1_vs_OpenLane2_Separation.md)
- 📌 [APPENDIX_Classic_OpenLane_Failure.md](./APPENDIX_Classic_OpenLane_Failure.md)
- 📌 [APPENDIX_Operational_Rules.md](./APPENDIX_Operational_Rules.md)

---

## ⚠️ Final Warning

This repository is **not friendly**.  
It is **not flexible**.  
It is **reliable**.

If you want novelty, **leave**.  
If you want OpenLane to **stop breaking**, **stay**.

---

## 👤 Author

| 📌 Item | Details |
|--------|---------|
| **Name** | Shinichi Samizo |
| **Expertise** | Semiconductor devices (logic, memory, high-voltage mixed-signal)<br>Thin-film piezo actuators for inkjet systems<br>Printhead productization, BOM management, ISO training |
| **GitHub** | [![GitHub](https://img.shields.io/badge/GitHub-Samizo--AITL-black?logo=github)](https://github.com/Samizo-AITL) |

---

## 📄 License

[![Hybrid License](https://img.shields.io/badge/license-Hybrid-blueviolet)](https://samizo-aitl.github.io/openlane-guide/#---license)

| 📌 Item | License | Description |
|--------|---------|-------------|
| **Source Code** | [**MIT License**](https://opensource.org/licenses/MIT) | Free to use, modify, and redistribute |
| **Text Materials** | [**CC BY 4.0**](https://creativecommons.org/licenses/by/4.0/) or [**CC BY-SA 4.0**](https://creativecommons.org/licenses/by-sa/4.0/) | Attribution required; share-alike applies for BY-SA |
| **Figures & Diagrams** | [**CC BY-NC 4.0**](https://creativecommons.org/licenses/by-nc/4.0/) | Non-commercial use only |
| **External References** | Follow the original license | Cite the original source properly |

---

## 💬 Feedback

> Suggestions, improvements, and discussions are welcome via GitHub Discussions.

[![💬 GitHub Discussions](https://img.shields.io/badge/💬%20GitHub-Discussions-brightgreen?logo=github)](https://github.com/Samizo-AITL/openlane-guide/discussions)

