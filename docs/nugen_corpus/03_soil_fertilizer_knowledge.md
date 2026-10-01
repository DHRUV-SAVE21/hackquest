# Soil and Fertilizer Knowledge

This document contains all static soil and fertilizer domain knowledge extracted from `backend/feature3/soil_data.json`, `backend/feature3/decision_engine.py`, `backend/crop_yield_prediction/router.py`, and `backend/database/supabase_master_schema.sql`.

---

## 1. Soil Types and Suitability Baseline

The project categorizes Indian agricultural soils into six major types:

| Soil Type | Physical Characteristics | Dominant Indian Regions | Suitable Crops (Project Source Data) |
| :--- | :--- | :--- | :--- |
| **Alluvial Soil** | High fertility, rich in potash, soft texture | Indo-Gangetic plains, river deltas | Wheat, Rice, Sugarcane, Maize, Pulses |
| **Black Cotton Soil (Regur)** | High clay content, moisture retentive, rich in iron/calcium | Deccan plateau (Maharashtra, MP, Gujarat) | Cotton, Soybean, Groundnut, Wheat, Jowar |
| **Red Soil** | Porous, friable structure, high iron oxide content | Tamil Nadu, Karnataka, Odisha, AP | Groundnut, Millets, Pulses, Tobacco, Oilseeds |
| **Laterite Soil** | Leached, acidic, low organic matter | Western Ghats, Eastern Ghats | Tea, Coffee, Cashew, Rubber |
| **Clay Loam** | High water retention capacity, heavy texture | Lowland river basins | Rice, Wheat, Sugarcane, Vegetables |
| **Sandy Loam** | High drainage, well-aerated, low water holding | Coastal plains, arid/semi-arid regions | Potato, Onion, Groundnut, Vegetables, Spices |

---

## 2. NPK and Soil Telemetry Parameter Ranges

In `backend/crop_yield_prediction/router.py` and `backend/feature3/soil_data.json`, soil metrics are mapped to standardized measurement scales:

| Parameter | Raw Metric Unit | Normalization Scale ($0.0 - 1.0$) | Optimal Agronomic Range |
| :--- | :--- | :--- | :--- |
| **Soil Moisture** | Percentage ($\%$) | $\text{Moisture} / 100.0$ | $40\% - 65\%$ (Crop dependent) |
| **Nitrogen ($N$)** | $\text{mg/kg}$ (PPM) | $\text{Nitrogen} / 500.0$ | $280 - 450 \text{ mg/kg}$ |
| **Phosphorus ($P$)** | $\text{mg/kg}$ (PPM) | $\text{Phosphorus} / 100.0$ | $20 - 50 \text{ mg/kg}$ |
| **Potassium ($K$)** | $\text{mg/kg}$ (PPM) | $\text{Potassium} / 100.0$ | $150 - 300 \text{ mg/kg}$ |
| **Soil pH** | pH Index ($0 - 14$) | Direct float | $6.0 - 7.5$ (Slightly Acidic to Neutral) |
| **Electrical Conductivity (EC)** | $\text{dS/m}$ | Direct float | $< 2.0 \text{ dS/m}$ (Low Salinity) |

---

## 3. Static Agronomic Rules vs Dynamic Sensor Values

To ensure proper model alignment, dynamic real-time telemetry is explicitly separated from static domain knowledge:

```
┌────────────────────────────────────────────────────────────────────────┐
│                      STATIC DOMAIN KNOWLEDGE                           │
│                      (Used for Nugen Corpus)                           │
│                                                                        │
│ - Soil Moisture < 25% indicates Wilting Point (Triggers Irrigation).  │
│ - Nitrogen < 150 mg/kg indicates severe nitrogen deficiency.           │
│ - Soil pH < 5.5 requires Agricultural Lime (Calcitic Limestone).       │
│ - Soil pH > 8.5 requires Gypsum application for sodicity correction.   │
└────────────────────────────────────────────────────────────────────────┘

                                  vs

┌────────────────────────────────────────────────────────────────────────┐
│                     DYNAMIC RUNTIME SENSOR DATA                        │
│                     (Excluded from Static Corpus)                      │
│                                                                        │
│ - "Farmer User-102 currently has soil moisture = 18.5% at 09:30 AM."   │
│ - "Plot 4B current NPK telemetry reading = N:120, P:22, K:18."         │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 4. Fertilizer Recommendation Logic

In `backend/crop_yield_prediction/router.py` and marketplace listings (`main.py`), fertilizer recommendations follow NPK deficit ratios:

### A. Nitrogen Deficiency ($N < 200 \text{ mg/kg}$)
- **Recommendation**: Apply Urea ($46\% \text{ Nitrogen}$) or Ammonium Sulphate.
- **Application Method**: Split application (50% basal at sowing, 50% top dressing during vegetative growth).

### B. Phosphorus Deficiency ($P < 15 \text{ mg/kg}$)
- **Recommendation**: Apply Di-Ammonium Phosphate (DAP $18\% \text{ N}, 46\% \text{ P}$) or Single Super Phosphate (SSP).
- **Application Method**: Basal application at the time of field preparation.

### C. Potassium Deficiency ($K < 100 \text{ mg/kg}$)
- **Recommendation**: Apply Muriate of Potash (MOP $60\% \text{ } K_2O$).
- **Application Method**: Basal application to build disease resistance and tuber/grain filling.

### D. Organic Alternatives
- **Neem Coated Urea**: Reduces nitrogen leaching and slow-release regulation.
- **Vermicompost / Farmyard Manure (FYM)**: Applied at 5–10 tonnes/hectare to restore organic carbon.

---

## 5. Usage Classification

- **Soil Types & Crop Suitability Baseline**: ALIGNMENT & RAG
- **NPK & pH Threshold Definitions**: ALIGNMENT
- **Fertilizer Recommendation Rules**: ALIGNMENT & RAG
- **Live Sensor Telemetry Logs**: RUNTIME ONLY (Dynamic)

---

## External Sources To Be Added Later
- IEEE/research papers: NOT YET PROVIDED
- Official agricultural guidelines: NOT YET PROVIDED unless already present
- Official government documents: NOT YET PROVIDED unless already present
