# Source Inventory

This document provides a comprehensive inventory of all source files, database schemas, code modules, prompts, and datasets utilized to construct the Annadata Saathi Agricultural Domain Corpus for Nugen alignment.

---

## 1. Corpus Source Traceability Table

| Category | Information Present | Source File / Database Table | Source Type | Data Nature | Destination Corpus File |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Crop Knowledge** | 15+ Indian crop growth duration, water req, soil suitability, historical yield, market price baseline. | `backend/feature4_drl/pipeline.py`<br>`backend/feature4_drl/enhanced_agriculture_dataset.csv` | Python Code / CSV Dataset | Static Benchmark | `01_crop_knowledge.md` |
| **Crop Disease** | 38 PlantVillage disease classes, OpenCV quality logic, HSV green-loss stress heatmap overlay, treatment advisory guidelines. | `backend/feature2/model_service.py`<br>`backend/feature2/agronomist_chat.py`<br>`notebooks/crop_disease.ipynb` | Python Code / Jupyter Notebook | Static Taxonomy & Advisory | `02_crop_disease_knowledge.md` |
| **Soil & Fertilizer** | Soil types (Alluvial, Black, Red), NPK measurement scales, pH ranges, fertilizer deficit calculation rules. | `backend/feature3/soil_data.json`<br>`backend/crop_yield_prediction/router.py`<br>`backend/database/supabase_master_schema.sql` | JSON / Python Code / SQL Schema | Static Rules vs Dynamic Telemetry | `03_soil_fertilizer_knowledge.md` |
| **Irrigation & Weather** | Irrigation decision matrix, stage-wise water sensitivity, Indian cropping calendar (Kharif, Rabi, Zaid). | `backend/feature3/decision_engine.py`<br>`backend/hardware/arduino/`<br>`backend/feature4_drl/enhanced_agriculture_dataset.csv` | Python Code / Arduino Sketch / CSV | Static Rules vs Real-time Weather | `04_irrigation_weather_knowledge.md` |
| **Government Schemes** | PM-KISAN, PM-KUSUM, SMAM, RKVY, NFSM, AIF, PMFBY eligibility rules, financial caps, subsidy formulas. | `backend/database/supabase_master_schema.sql` (`available_schemes`) <br>`backend/feature4/tools.py`<br>`backend/feature5/subsidy_service.py` | SQL Schema / Python Tools | Dynamic Database Records | `05_government_schemes.md` |
| **Farmer FAQ & Advisory** | AI identity (Annadata Saathi), multilingual protocol (Hindi, Marathi, English), pesticide safety rules, category Q&A. | `backend/feature_agent/prompts/annadata_prompt.txt`<br>`backend/feature2/agronomist_chat.py`<br>`backend/feature4/agent.py` | System Prompt / Python LangChain | Static Guidelines | `06_farmer_faq_and_advisory.md` |
| **Best Practices** | Crop rotation rules, IPM guidelines, 6-month farm equipment maintenance schedules, post-harvest grain moisture limits. | `backend/crop_yield_prediction/router.py`<br>`backend/feature5/equipment_analyzer.py`<br>`backend/feature6_blockchain/trust_engine.py` | Python Code | Static Standards | `07_agricultural_best_practices.md` |
| **Project Context** | Project overview, component analysis, ML models inventory, current RAG flow, proposed Nugen cognitive role. | `PROJECT_STRUCTURE.md`<br>`backend/main.py`<br>`C:\Users\DHRUV\.gemini\antigravity\brain\aa9e5068-3467-483d-9b0f-5e0332f8241b\nugen_integration_report.md` | Codebase Architecture & Integration Report | Reference Architecture | `08_annadata_project_context.md` |

---

## 2. Excluded Data Categories (Security & Alignment Protection)

In strict accordance with corpus guidelines, the following categories were **EXCLUDED** from all domain corpus files:

1. **User Personal Identifiable Information (PII)**: Farmer names, phone numbers, Aadhaar numbers, PAN numbers, bank account numbers, IFSC codes, voter IDs, and personal home addresses (`farmer_profiles` table).
2. **Security & Authentication Secrets**: Passwords, password hashes, JWT secrets, Supabase service-role keys, Vapi API keys, OpenRouter keys, and environment variables (`.env` files).
3. **Raw Media & Binary Assets**: Base64 encoded strings, raw JPEG/PNG/WebP image files, and PDF certificate binary buffers.
4. **Dynamic Real-Time Data**: Live weather forecasts, current telemetry sensor readings, and daily Mandi market prices (marked for runtime reference/RAG).
5. **Project Administrative Info**: Team member names, university presentation scripts, and hackathon documentation.

---

## External Sources To Be Added Later
- IEEE/research papers: NOT YET PROVIDED
- Official agricultural guidelines: NOT YET PROVIDED unless already present
- Official government documents: NOT YET PROVIDED unless already present
