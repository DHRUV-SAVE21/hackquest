# Crop Knowledge

This document contains all crop-related agricultural facts directly extracted from the Annadata Saathi codebase and datasets (`backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`, `notebooks/hybrid_agri_dataset_2000rows.csv`, and `backend/crop_yield_prediction/router.py`).

---

## 1. Crop Knowledge Inventory

### Rice
- **Crop Category**: Cereal / Staple Crop
- **Season**: Kharif
- **Growth Duration**: ~120 - 150 days (`crop_info` average in dataset)
- **Water Requirement**: High
- **Soil Suitability**: Alluvial, Clay, Loam (`soil_type` in dataset)
- **Temperature Range**: 20°C - 35°C
- **Humidity Range**: 60% - 80%
- **Rainfall Requirement**: High (1000 - 1500 mm)
- **Historical Average Yield**: ~3.5 - 4.5 tonnes/hectare (`avg_yield` benchmark)
- **Market Price Baseline**: ₹22,000 / Tonne (INR 2024 baseline in `pipeline.py`)
- **Risk Assessment Benchmark**: `avg_risk` score ~0.25 (Low to Medium)
- **Recommended Usage**: ALIGNMENT (agronomic parameters) & RAG (financial baseline)
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Wheat
- **Crop Category**: Cereal / Staple Crop
- **Season**: Rabi
- **Growth Duration**: ~110 - 130 days
- **Water Requirement**: Medium
- **Soil Suitability**: Alluvial, Clay Loam
- **Temperature Range**: 12°C - 25°C
- **Humidity Range**: 50% - 70%
- **Rainfall Requirement**: Moderate (450 - 650 mm)
- **Historical Average Yield**: ~3.2 - 4.0 tonnes/hectare
- **Market Price Baseline**: ₹22,750 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.20 (Low)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Maize (Corn)
- **Crop Category**: Coarse Cereal / Grain
- **Season**: Kharif / Rabi
- **Growth Duration**: ~90 - 110 days
- **Water Requirement**: Medium
- **Soil Suitability**: Well-drained Alluvial, Red, Black soil
- **Temperature Range**: 18°C - 30°C
- **Humidity Range**: 55% - 75%
- **Rainfall Requirement**: 500 - 800 mm
- **Historical Average Yield**: ~2.8 - 3.8 tonnes/hectare
- **Market Price Baseline**: ₹20,900 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.22 (Low)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Cotton
- **Crop Category**: Cash Crop / Fiber
- **Season**: Kharif
- **Growth Duration**: ~150 - 180 days
- **Water Requirement**: High
- **Soil Suitability**: Black Cotton Soil (Regur), Deep Alluvial
- **Temperature Range**: 21°C - 35°C
- **Humidity Range**: 50% - 70%
- **Rainfall Requirement**: 500 - 1000 mm
- **Historical Average Yield**: ~1.8 - 2.5 tonnes/hectare
- **Market Price Baseline**: ₹60,000 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.38 (Medium-High)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Sugarcane
- **Crop Category**: Cash Crop / Commercial
- **Season**: Perennial / Kharif
- **Growth Duration**: ~300 - 365 days
- **Water Requirement**: Very High
- **Soil Suitability**: Heavy Alluvial, Loamy Soil
- **Temperature Range**: 20°C - 38°C
- **Humidity Range**: 60% - 85%
- **Rainfall Requirement**: 1500 - 2500 mm
- **Historical Average Yield**: ~60.0 - 80.0 tonnes/hectare
- **Market Price Baseline**: ₹3,150 / Tonne (Fair and Remunerative Price FRP)
- **Risk Assessment Benchmark**: `avg_risk` score ~0.18 (Low)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Groundnut (Peanut)
- **Crop Category**: Oilseed / Legume
- **Season**: Kharif
- **Growth Duration**: ~105 - 120 days
- **Water Requirement**: Medium
- **Soil Suitability**: Sandy Loam, Red Soil
- **Temperature Range**: 22°C - 30°C
- **Humidity Range**: 50% - 65%
- **Rainfall Requirement**: 500 - 700 mm
- **Historical Average Yield**: ~1.5 - 2.2 tonnes/hectare
- **Market Price Baseline**: ₹63,770 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.30 (Medium)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Soybean
- **Crop Category**: Oilseed / Legume
- **Season**: Kharif
- **Growth Duration**: ~95 - 110 days
- **Water Requirement**: Medium
- **Soil Suitability**: Black Cotton Soil, Well-drained Loam
- **Temperature Range**: 20°C - 32°C
- **Humidity Range**: 60% - 75%
- **Rainfall Requirement**: 600 - 900 mm
- **Historical Average Yield**: ~1.8 - 2.5 tonnes/hectare
- **Market Price Baseline**: ₹46,000 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.28 (Medium)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Mustard
- **Crop Category**: Oilseed
- **Season**: Rabi
- **Growth Duration**: ~110 - 130 days
- **Water Requirement**: Low
- **Soil Suitability**: Alluvial, Loamy, Sandy Loam
- **Temperature Range**: 10°C - 25°C
- **Humidity Range**: 45% - 65%
- **Rainfall Requirement**: 250 - 400 mm
- **Historical Average Yield**: ~1.2 - 1.8 tonnes/hectare
- **Market Price Baseline**: ₹56,500 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.22 (Low)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Chilli (Dry Chilli)
- **Crop Category**: Spices / Horticulture
- **Season**: Kharif / Rabi
- **Growth Duration**: ~140 - 160 days
- **Water Requirement**: Medium
- **Soil Suitability**: Well-drained Red, Black, Sandy Loam
- **Temperature Range**: 20°C - 32°C
- **Humidity Range**: 55% - 70%
- **Rainfall Requirement**: 600 - 1000 mm
- **Historical Average Yield**: ~1.5 - 2.5 tonnes/hectare
- **Market Price Baseline**: ₹180,000 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.42 (High - price/disease volatility)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Tomato
- **Crop Category**: Vegetable / Horticulture
- **Season**: Kharif / Rabi / Zaid
- **Growth Duration**: ~90 - 120 days
- **Water Requirement**: Medium
- **Soil Suitability**: Well-drained Sandy Loam, Clay Loam (pH 6.0 - 7.0)
- **Temperature Range**: 18°C - 30°C
- **Humidity Range**: 60% - 80%
- **Rainfall Requirement**: 400 - 600 mm
- **Historical Average Yield**: ~15.0 - 25.0 tonnes/hectare
- **Market Price Baseline**: ₹15,000 / Tonne (Conservative baseline average)
- **Risk Assessment Benchmark**: `avg_risk` score ~0.45 (High - disease susceptible)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Onion
- **Crop Category**: Vegetable / Horticulture
- **Season**: Rabi / Kharif
- **Growth Duration**: ~120 - 150 days
- **Water Requirement**: Medium
- **Soil Suitability**: Well-drained Deep Alluvial, Loamy Soil
- **Temperature Range**: 15°C - 28°C
- **Humidity Range**: 50% - 70%
- **Rainfall Requirement**: 350 - 500 mm
- **Historical Average Yield**: ~12.0 - 18.0 tonnes/hectare
- **Market Price Baseline**: ₹25,000 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.35 (Medium)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Potato
- **Crop Category**: Vegetable / Tuber
- **Season**: Rabi
- **Growth Duration**: ~90 - 120 days
- **Water Requirement**: Medium
- **Soil Suitability**: Well-drained Loose Loam, Sandy Loam (pH 5.2 - 6.4)
- **Temperature Range**: 15°C - 24°C
- **Humidity Range**: 55% - 75%
- **Rainfall Requirement**: 400 - 600 mm
- **Historical Average Yield**: ~18.0 - 25.0 tonnes/hectare
- **Market Price Baseline**: ₹12,000 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.32 (Medium)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Brinjal (Eggplant)
- **Crop Category**: Vegetable
- **Season**: Kharif / Rabi
- **Growth Duration**: ~120 - 140 days
- **Water Requirement**: Medium
- **Soil Suitability**: Well-drained Silt Loam, Clay Loam
- **Temperature Range**: 20°C - 32°C
- **Humidity Range**: 55% - 75%
- **Rainfall Requirement**: 500 - 800 mm
- **Historical Average Yield**: ~12.0 - 20.0 tonnes/hectare
- **Market Price Baseline**: ₹18,000 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.30 (Medium)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Cabbage
- **Crop Category**: Vegetable / Cole Crop
- **Season**: Rabi
- **Growth Duration**: ~80 - 100 days
- **Water Requirement**: Medium
- **Soil Suitability**: Well-drained Sandy Loam, Heavy Clay
- **Temperature Range**: 15°C - 22°C
- **Humidity Range**: 60% - 80%
- **Rainfall Requirement**: 400 - 600 mm
- **Historical Average Yield**: ~20.0 - 30.0 tonnes/hectare
- **Market Price Baseline**: ₹10,000 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.25 (Low-Medium)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

### Cauliflower
- **Crop Category**: Vegetable / Cole Crop
- **Season**: Rabi
- **Growth Duration**: ~85 - 105 days
- **Water Requirement**: Medium
- **Soil Suitability**: Deep Loam, Moisture Retentive Soil
- **Temperature Range**: 12°C - 20°C
- **Humidity Range**: 60% - 80%
- **Rainfall Requirement**: 450 - 650 mm
- **Historical Average Yield**: ~15.0 - 22.0 tonnes/hectare
- **Market Price Baseline**: ₹15,000 / Tonne
- **Risk Assessment Benchmark**: `avg_risk` score ~0.28 (Medium)
- **Recommended Usage**: ALIGNMENT & RAG
- **Source**: `backend/feature4_drl/pipeline.py`, `backend/feature4_drl/enhanced_agriculture_dataset.csv`

---

## 2. Additional Crops Referenced in Yield Models (55 Crops Total)
The `crop_yield_prediction` neural network module handles 55 Indian crop varieties. Key varieties with baseline data present include:
- Pulses: Arhar (Tur), Gram (Chana), Moong, Urad.
- Spices: Turmeric, Ginger, Garlic, Cumin, Coriander.
- Commercial: Tobacco, Jute, Tea, Coffee.

---

## 3. Crop Recommendation & Scoring Logic

In `backend/feature4_drl/pipeline.py`, crop recommendation scores are calculated using environmental vectors:
$$\text{Score} = \left( \frac{\text{Yield}_{\text{predicted}}}{\text{Yield}_{\text{historical\_avg}}} \times 100 \right) \times (1 - \text{Risk}_{\text{predicted}})$$
- **Expected Revenue ($INR/Ha$)** = $\text{Predicted Yield (t/ha)} \times \text{Market Price (INR/t)}$
- **Value at Risk ($INR/Ha$)** = $\text{Expected Revenue} \times \text{Risk Score}$

---

## External Sources To Be Added Later
- IEEE/research papers: NOT YET PROVIDED
- Official agricultural guidelines: NOT YET PROVIDED unless already present
- Official government documents: NOT YET PROVIDED unless already present
