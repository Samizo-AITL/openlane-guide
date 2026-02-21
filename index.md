# OpenLane Guide — Repository Index

This repository must be read **in order**.
It is intentionally strict.

---

## Phase 1 — Environment Survival

01. `01_WSL_Docker_Setup.md`  
WSL2 and Docker done correctly, with export/import survivability.

02. `02_OpenLane1_Setup.md`  
Install and freeze OpenLane1. This is the production flow.

03. `03_OpenLane2_Setup.md`  
OpenLane2 setup for evaluation only. Never mix.

04. `04_PDK_Setup.md`  
sky130 / gf180 PDK as an asset. Built once. Never rebuilt.

05. `05_Verification_Test.md`  
Smoke tests. Proof that the environment is real.

06. `06_Migration_WSL_Export.md`  
Disaster recovery. Hardware failure becomes irrelevant.

07. `07_Troubleshooting.md`  
Failure prevention checklist. Not a fix guide.

---

## Phase 2 — Physical Design Reality

08. `08_Placement.md`  
Global vs detailed placement. Density and convergence.

09. `09_CTS.md`  
Clock Tree Synthesis. Skew and insertion delay.

10. `10_Routing.md`  
Global and detailed routing. Congestion and DRC.

11. `11_DRC_LVS.md`  
Magic DRC and Netgen LVS. What “clean” actually means.

12. `12_STA.md`  
OpenSTA. WNS, TNS, setup and hold.

13. `13_GDS_Signoff.md`  
Final deliverables: GDS, LEF, SPEF, SDF, SPICE.

---

## Phase 3 — Integration and Verification

14. `14_Caravel_Hardening.md`  
User project integration and MPW preparation.

15. `15_GLS.md`  
Gate-level simulation. Functional and SDF.

16. `16_EndToEnd_Exercise.md`  
RTL → GDS → GLS → Caravel, end-to-end.

---

## Appendices — Hard-earned knowledge

- `APPENDIX_GLS_Failure_Patterns.md`
- `APPENDIX_Magic_KLayout.md`
- `APPENDIX_GDS_Analysis.md`
- `APPENDIX_OpenROAD_Failures.md`
- `APPENDIX_Layer_Mapping.md`

---

## Final warning

This repository is not friendly.
It is not flexible.
It is reliable.

If you want novelty, leave.
If you want OpenLane to stop breaking, stay.
