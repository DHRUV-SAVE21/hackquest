# Agricultural Best Practices

This document compiles all agricultural best practices, crop management guidelines, machinery maintenance standards, and post-harvest handling rules extracted from `backend/crop_yield_prediction/router.py`, `backend/feature5/equipment_analyzer.py`, `backend/feature3/decision_engine.py`, and `backend/feature6_blockchain/trust_engine.py`.

---

## 1. Crop & Field Management Best Practices

### A. Crop Rotation Strategy
- **Rule**: Rotate cereal crops (Wheat, Maize, Rice) with leguminous crops (Soybean, Groundnut, Gram) to break pest cycles and naturally fix atmospheric nitrogen into the soil.
- **Source**: `backend/feature4_drl/pipeline.py` (`previous_crop` feature encoding)

### B. Seed Selection & Treatment
- **Rule**: Use certified high-yielding variety (HYV) or hybrid seeds resistant to regional pests. Treat seeds with *Trichoderma viride* (organic) or Thiram/Carbendazim prior to sowing to prevent seed-borne fungal infections.
- **Source**: `backend/crop_yield_prediction/router.py`

---

## 2. Water & Irrigation Management Best Practices

### A. Micro-Irrigation (Drip & Sprinkler)
- **Rule**: Prefer drip irrigation for row crops and vegetables (Tomato, Chilli, Sugarcane) to achieve up to 90% water-use efficiency and deliver water directly to root zones.
- **Source**: `backend/feature3/decision_engine.py`

### B. Evaporation Reduction
- **Rule**: Schedule irrigation during early morning (05:00 - 08:00 AM) or late evening to minimize evaporative losses caused by midday high temperatures and wind.
- **Source**: `backend/feature3/decision_engine.py`

---

## 3. Integrated Pest & Disease Management (IPM)

### A. Early Detection & Monitoring
- **Rule**: Inspect farm fields twice weekly for early signs of leaf spot, mold, or insect infestation. Use sticky yellow cards for monitoring whiteflies and aphids.
- **Source**: `backend/feature2/model_service.py`

### B. Biological & Organic Control First
- **Rule**: Use Neem-based bio-pesticides (1500 PPM Neem oil) as first-line preventative defense before escalating to synthetic chemical sprayers.
- **Source**: `backend/feature2/agronomist_chat.py`

---

## 4. Farm Equipment Preventative Maintenance

From `backend/feature5/equipment_analyzer.py` (6-Month Maintenance Rules):

```
┌────────────────────────────────────────────────────────────────────────┐
│               MACHINERY PREVENTATIVE MAINTENANCE SCHEDULE              │
├───────────────────┬─────────────────────┬──────────────────────────────┤
│ Equipment Type    │ Inspection Interval │ Maintenance Action           │
├───────────────────┼─────────────────────┼──────────────────────────────┤
│ Tractor Engine    │ Every 250 Hours     │ Replace oil & fuel filter    │
│ Rotavator Blades  │ Pre-Season / 100 Hr │ Check L-blade wear & torque  │
│ Hydraulic System  │ Monthly             │ Top up hydraulic fluid level │
│ Irrigation Pump   │ Bi-Weekly           │ Check impeller seal & wiring │
│ Spraying Nozzles  │ Post-Use            │ Flush with clean water       │
└───────────────────┴─────────────────────┴──────────────────────────────┘
```

---

## 5. Post-Harvest Handling & Quality Preservation

From `backend/feature6_blockchain/trust_engine.py`:

- **Moisture Content at Storage**: Ensure grain moisture is reduced below $12\%$ for cereals (Wheat, Rice) prior to bagging/warehousing to prevent aflatoxin contamination and grain rot.
- **Batch Traceability**: Assign unique Blockchain Batch IDs to harvested lots to maintain harvest date, quality grade, and origin transparency for premium marketplace pricing.

---

## 6. Usage Classification

- **Crop Management & IPM Rules**: ALIGNMENT
- **Equipment Maintenance Standards**: ALIGNMENT & RAG
- **Post-Harvest Handling Rules**: ALIGNMENT

---

## External Sources To Be Added Later
- IEEE/research papers: NOT YET PROVIDED
- Official agricultural guidelines: NOT YET PROVIDED unless already present
- Official government documents: NOT YET PROVIDED unless already present
