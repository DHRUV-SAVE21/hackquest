# Irrigation and Weather Knowledge

This document details all irrigation decision rules, physiological moisture thresholds, and seasonal weather knowledge extracted from `backend/feature3/decision_engine.py`, `backend/hardware/arduino/`, `backend/crop_yield_prediction/router.py`, and `backend/feature4_drl/enhanced_agriculture_dataset.csv`.

---

## 1. Irrigation Decision Engine Rules

In `backend/feature3/decision_engine.py`, irrigation automation is governed by deterministic physiological thresholds:

```
┌────────────────────────────────────────────────────────────────────────┐
│                   IRRIGATION TRIGGER DECISION MATRIX                   │
├─────────────────┬───────────────────┬───────────────────┬──────────────┤
│ Soil Moisture % │ Rain Forecast 24h │ Action Triggered  │ Pump Command │
├─────────────────┼───────────────────┼───────────────────┼──────────────┤
│ < 25%           │ 0 mm              │ Immediate Irrigate│ PUMP_ON      │
│ < 25%           │ > 10 mm           │ Hold (Rain Expected) PUMP_OFF    │
│ 25% - 45%       │ 0 mm              │ Moderate Irrigate │ PUMP_ON      │
│ 45% - 70%       │ Any               │ Optimal (No Action) PUMP_OFF    │
│ > 70%           │ Any               │ Over-watered Risk │ PUMP_OFF     │
└─────────────────┴───────────────────┴───────────────────┴──────────────┘
```

---

## 2. Stage-Wise Irrigation Requirements

Irrigation demand varies dynamically across physiological crop development stages:

| Crop Growth Stage | Water Sensitivity | Irrigation Rule / Strategy |
| :--- | :--- | :--- |
| **Germination / Sowing** | Moderate | Light surface irrigation to promote seedling emergence. Avoid waterlogging. |
| **Vegetative Phase** | High | Regular irrigation interval to maintain soil moisture between $45\% - 60\%$. |
| **Flowering Stage** | **CRITICAL HIGH** | Moisture stress during flowering causes flower drop and yield reduction. Maintain moisture $> 55\%$. |
| **Grain Filling / Fruit Set** | High | Adequate water needed to support fruit development and seed weight accumulation. |
| **Maturity / Pre-Harvest** | Low | Stop irrigation $10 - 15$ days prior to harvest to allow uniform ripening. |

---

## 3. Indian Agricultural Seasons (Cropping Calendar)

The codebase binds crop intelligence to India's three major cropping seasons:

### A. Kharif Season (Monsoon Crops)
- **Sowing Period**: June – July (Onset of South-West Monsoon).
- **Harvesting Period**: September – October.
- **Climatic Characteristics**: Warm, high humidity, heavy rainfall.
- **Key Crops**: Rice, Maize, Cotton, Soybean, Groundnut, Sugarcane.

### B. Rabi Season (Winter Crops)
- **Sowing Period**: October – November (Post-Monsoon).
- **Harvesting Period**: March – April.
- **Climatic Characteristics**: Cool temperatures, dry climate, moderate moisture.
- **Key Crops**: Wheat, Mustard, Potato, Gram (Chickpea), Barley, Oats.

### C. Zaid Season (Summer Crops)
- **Sowing Period**: March – April.
- **Harvesting Period**: May – June.
- **Climatic Characteristics**: Hot, dry weather, low humidity, relies on drip/pump irrigation.
- **Key Crops**: Watermelon, Muskmelon, Cucumber, Vegetables, Fodder crops.

---

## 4. Weather Precautions & Adverse Condition Advisory

Derived from `backend/feature_agent/prompts/annadata_prompt.txt` and `backend/crop_yield_prediction/router.py`:

- **Excess Rainfall / Flood Warning**: Ensure proper farm drainage channels to prevent root rot (*Phytophthora*). Delay fertilizer application to prevent nutrient runoff.
- **Drought / Heatwave Warning**: Apply mulch (straw or plastic) to conserve soil moisture. Irrigate during early morning or evening to minimize evaporative loss.
- **Frost / Cold Wave Warning**: Apply light evening irrigation to raise soil thermal mass and protect tender foliage from frost burn.

---

## 5. Static Knowledge vs Real-Time Data Boundary

```
┌────────────────────────────────────────────────────────────────────────┐
│                      STATIC DOMAIN KNOWLEDGE                           │
│                      (Used for Nugen Corpus)                           │
│                                                                        │
│ - Kharif season runs from June to October.                             │
│ - Flowering stage is the most water-sensitive phase for grain crops.   │
│ - Soil moisture < 25% with 0mm rain forecast triggers pump activation. │
└────────────────────────────────────────────────────────────────────────┘

                                  vs

┌────────────────────────────────────────────────────────────────────────┐
│                    REAL-TIME RUNTIME WEATHER DATA                      │
│                     (Excluded from Static Corpus)                      │
│                                                                        │
│ - "Current temperature in Nashik is 32.4°C with 62% humidity."         │
│ - "Rainfall forecast for tomorrow in District X is 12.5 mm."           │
└────────────────────────────────────────────────────────────────────────┘
```

---

## 6. Usage Classification

- **Irrigation Threshold Rules & Matrix**: ALIGNMENT
- **Cropping Calendar (Kharif/Rabi/Zaid)**: ALIGNMENT & RAG
- **Stage-Wise Irrigation Rules**: ALIGNMENT & RAG
- **Weather Advisory Guidelines**: ALIGNMENT
- **Live Weather Forecast Feeds**: RUNTIME ONLY (Dynamic)

---

## External Sources To Be Added Later
- IEEE/research papers: NOT YET PROVIDED
- Official agricultural guidelines: NOT YET PROVIDED unless already present
- Official government documents: NOT YET PROVIDED unless already present
