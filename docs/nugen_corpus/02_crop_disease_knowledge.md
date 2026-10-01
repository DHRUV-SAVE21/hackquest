# Crop Disease Knowledge

This document details all crop disease classification and diagnostic knowledge extracted from `backend/feature2/model_service.py`, `backend/feature2/agronomist_chat.py`, `notebooks/crop_disease.ipynb`, and related backend services.

---

## 1. System Architecture Boundary

```
┌─────────────────────────────────────────┐
│       Vision Layer (TFLite CNN)         │
│  - Input: 224x224x3 RGB Image           │
│  - Output: Raw Class Name + Softmax Conf │
│  - Image Quality (Blur/Brightness)      │
│  - HSV Stress Heatmap Base64            │
└────────────────────┬────────────────────┘
                     │ Raw Diagnosis Payload
                     ▼
┌─────────────────────────────────────────┐
│     Agricultural Advisory Layer         │
│  - Input: Diagnosis + Farmer Context    │
│  - Output: Organic/Chemical Remedies    │
│  - Safety & Dosage Warnings             │
│  - Government Scheme Integration        │
└─────────────────────────────────────────┘
```

---

## 2. CNN Model Disease Classes (38 PlantVillage Classes)

Below are the exact 38 plant and disease classes defined in `backend/feature2/model_service.py` (`CLASS_NAMES` list):

| Index | Raw Class Code | Formatted Display Name | Target Crop | Condition |
| :--- | :--- | :--- | :--- | :--- |
| 0 | `Apple___Apple_scab` | Apple - Apple Scab | Apple | Disease |
| 1 | `Apple___Black_rot` | Apple - Black Rot | Apple | Disease |
| 2 | `Apple___Cedar_apple_rust` | Apple - Cedar Apple Rust | Apple | Disease |
| 3 | `Apple___healthy` | Apple - Healthy | Apple | Healthy |
| 4 | `Blueberry___healthy` | Blueberry - Healthy | Blueberry | Healthy |
| 5 | `Cherry_(including_sour)___Powdery_mildew` | Cherry - Powdery Mildew | Cherry | Disease |
| 6 | `Cherry_(including_sour)___healthy` | Cherry - Healthy | Cherry | Healthy |
| 7 | `Corn_(maize)___Cercospora_leaf_spot Gray_leaf_spot` | Corn - Gray Leaf Spot | Corn (Maize) | Disease |
| 8 | `Corn_(maize)___Common_rust_` | Corn - Common Rust | Corn (Maize) | Disease |
| 9 | `Corn_(maize)___Northern_Leaf_Blight` | Corn - Northern Leaf Blight | Corn (Maize) | Disease |
| 10 | `Corn_(maize)___healthy` | Corn - Healthy | Corn (Maize) | Healthy |
| 11 | `Grape___Black_rot` | Grape - Black Rot | Grape | Disease |
| 12 | `Grape___Esca_(Black_Measles)` | Grape - Esca (Black Measles) | Grape | Disease |
| 13 | `Grape___Leaf_blight_(Isariopsis_Leaf_Spot)` | Grape - Leaf Blight | Grape | Disease |
| 14 | `Grape___healthy` | Grape - Healthy | Grape | Healthy |
| 15 | `Orange___Haunglongbing_(Citrus_greening)` | Orange - Citrus Greening | Orange | Disease |
| 16 | `Peach___Bacterial_spot` | Peach - Bacterial Spot | Peach | Disease |
| 17 | `Peach___healthy` | Peach - Healthy | Peach | Healthy |
| 18 | `Pepper,_bell___Bacterial_spot` | Bell Pepper - Bacterial Spot | Bell Pepper | Disease |
| 19 | `Pepper,_bell___healthy` | Bell Pepper - Healthy | Bell Pepper | Healthy |
| 20 | `Potato___Early_blight` | Potato - Early Blight | Potato | Disease |
| 21 | `Potato___Late_blight` | Potato - Late Blight | Potato | Disease |
| 22 | `Potato___healthy` | Potato - Healthy | Potato | Healthy |
| 23 | `Raspberry___healthy` | Raspberry - Healthy | Raspberry | Healthy |
| 24 | `Soybean___healthy` | Soybean - Healthy | Soybean | Healthy |
| 25 | `Squash___Powdery_mildew` | Squash - Powdery Mildew | Squash | Disease |
| 26 | `Strawberry___Leaf_scorch` | Strawberry - Leaf Scorch | Strawberry | Disease |
| 27 | `Strawberry___healthy` | Strawberry - Healthy | Strawberry | Healthy |
| 28 | `Tomato___Bacterial_spot` | Tomato - Bacterial Spot | Tomato | Disease |
| 29 | `Tomato___Early_blight` | Tomato - Early Blight | Tomato | Disease |
| 30 | `Tomato___Late_blight` | Tomato - Late Blight | Tomato | Disease |
| 31 | `Tomato___Leaf_Mold` | Tomato - Leaf Mold | Tomato | Disease |
| 32 | `Tomato___Septoria_leaf_spot` | Tomato - Septoria Leaf Spot | Tomato | Disease |
| 33 | `Tomato___Spider_mites Two-spotted_spider_mite` | Tomato - Two-Spotted Spider Mite | Tomato | Pest/Mite |
| 34 | `Tomato___Target_Spot` | Tomato - Target Spot | Tomato | Disease |
| 35 | `Tomato___Tomato_Yellow_Leaf_Curl_Virus` | Tomato - Yellow Leaf Curl Virus | Tomato | Viral |
| 36 | `Tomato___Tomato_mosaic_virus` | Tomato - Mosaic Virus | Tomato | Viral |
| 37 | `Tomato___healthy` | Tomato - Healthy | Tomato | Healthy |

---

## 3. Computer Vision Quality & Stress Features

### A. OpenCV Quality Validation Logic
- **Blur Detection**: Calculated using Laplacian Variance (`cv2.Laplacian(gray, cv2.CV_64F).var()`). Threshold $< 100$ flags image as blurry.
- **Brightness Detection**: Calculated using mean pixel intensity (`np.mean(gray)`). Threshold $< 50$ flags image as underexposed/dark.

### B. HSV Non-Green Stress Heatmap Generation
- **Green Range (Healthy)**: HSV Hue 35 to 85, Saturation 40 to 255, Value 40 to 255.
- **Stress Detection**: OpenCV inverts green mask (`cv2.bitwise_not(mask_green)`) to locate non-green foliage regions (yellowing, browning, necrosis).
- **Color Overlay**: OpenCV applies JET colormap (`cv2.COLORMAP_JET`) over original image at $0.3$ weight.

---

## 4. Agricultural Advisory & Treatment Protocol

When a raw CNN diagnosis is emitted, the Advisory Layer (`feature2/agronomist_chat.py`) generates treatment responses according to the following instructions:

### A. Potato Late Blight / Early Blight
- **Symptoms**: Dark brown concentric spots on leaves, water-soaked lesions.
- **Organic Remedy**: Neem oil spray (5ml/L water) for early prevention.
- **Chemical Remedy**: Copper Oxychloride or Mancozeb spray (`[NOT PRESENT IN CURRENT PROJECT SOURCES — EXTERNAL VERIFIED SOURCE REQUIRED FOR EXACT DOSAGE FORMULAS]`).
- **Safety Warning**: Wear gloves and mask during chemical application.

### B. Tomato Early Blight / Late Blight / Leaf Mold
- **Symptoms**: Yellow halos around leaf spots, wilting leaves, mold spores.
- **Organic Remedy**: Baking soda solution or bio-fungicide (Trichoderma viride).
- **Chemical Remedy**: Chlorothalonil or Mancozeb (`[NOT PRESENT IN CURRENT PROJECT SOURCES — EXTERNAL VERIFIED SOURCE REQUIRED FOR EXACT DOSAGE FORMULAS]`).

### C. Citrus Greening / Huanglongbing (Orange)
- **Symptoms**: Asymmetric yellow mottling on leaves, stunted fruit growth.
- **Management**: Vector control (Citrus Psyllid control); remove infected branches.

---

## 5. Usage Classification

- **38 Disease Taxonomy**: ALIGNMENT (Model vocabulary & category mapping)
- **Quality & HSV Heatmap Logic**: RUNTIME ONLY (Computed dynamically per frame)
- **Treatment Guidelines & Advisory Prompts**: ALIGNMENT & RAG

---

## External Sources To Be Added Later
- IEEE/research papers: NOT YET PROVIDED
- Official agricultural guidelines: NOT YET PROVIDED unless already present
- Official government documents: NOT YET PROVIDED unless already present
