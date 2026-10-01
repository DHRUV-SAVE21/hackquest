# 🌿 NDVI Threshold Configuration

The system uses **Sentinel-2 Satellite Data** to calculate the Normalized Difference Vegetation Index (NDVI). The following thresholds are currently set in `backend/feature2/satellite_service.py`:

## 1. Noise Filtering
-   **Threshold:** `> 0.15`
-   **Purpose:** Only pixels with NDVI greater than 0.15 are considered "Vegetation". This filters out bare soil, water, and roads from the average calculation to ensure accuracy.

## 2. Health Classification
Based on the **Average NDVI** of the valid vegetation pixels:

| Average NDVI | Status | Description |
| :--- | :--- | :--- |
| **< 0.25** | 🔴 **Critical** | Severe stress or crop loss. High likelihood of valid insurance claim. |
| **0.25 - 0.50** | 🟡 **Moderate** | Crop is under stress or sparse. |
| **> 0.50** | 🟢 **Excellent** | Dense, healthy vegetation. |

## 3. How to Change
To adjust these values, edit `backend/feature2/satellite_service.py`:
-   **Line 182:** `if ndvi_real > 0.15:` (Noise Filter)
-   **Line 210:** `if avg_ndvi < 0.25:` (Critical Threshold)
-   **Line 213:** `elif avg_ndvi < 0.50:` (Moderate Threshold)
