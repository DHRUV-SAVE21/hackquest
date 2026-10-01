# Government Agricultural Schemes and Subsidies

This document preserves the official government scheme records extracted directly from the Annadata Saathi database schema (`backend/database/supabase_master_schema.sql`), scheme search tools (`backend/feature4/tools.py`), and subsidy calculation services (`backend/feature5/subsidy_service.py`).

> **DATA STATUS WARNING**: Government scheme policies, financial caps, and application URLs are dynamic and subject to policy updates. The records below represent **existing project database information** and should be retrieved via RAG for live accuracy.

---

## 1. Scheme Directory

### PM-KISAN (Pradhan Mantri Kisan Samman Nidhi)

- **Purpose**: Direct income support scheme providing financial assistance to all landholding farmer families across India.
- **Eligibility**:
  - Landholding farmer family with cultivable land in their name.
  - Indian citizen.
  - Non-income tax payer in the preceding assessment year.
  - Excludes institutional landholders, serving/retired government officers.
- **Benefits**: ₹6,000 per year transferred in 3 equal installments of ₹2,000 every 4 months directly into the farmer's bank account via DBT.
- **Subsidy / Financial Information**: Fixed financial grant of ₹6,000/year ($0\%$ subsidy, direct cash transfer).
- **Applicable State**: All States and Union Territories (Central Sector Scheme).
- **Equipment / Crop Applicability**: Universal (All crops/equipment).
- **Required Documents**: Aadhaar Card, Land ownership deed / Khasra-Khatauni, Bank Passbook, Mobile number.
- **Application Information**: Official portal: `https://pmkisan.gov.in/`
- **Source**: `backend/database/supabase_master_schema.sql` (`available_schemes` table)
- **Data Status**: Existing project database record.
- **Recommended Usage**: RAG (Dynamic lookup) & ALIGNMENT (Eligibility rules baseline).

---

### PM-KUSUM Solar Pump Scheme (Component B)

- **Purpose**: Installation of standalone solar powered agriculture water pumps to replace diesel pumps and ensure reliable daytime irrigation in off-grid rural areas.
- **Eligibility**:
  - Individual farmers, water user associations, cooperatives, panchayats.
  - Must possess cultivable land with a valid water source (well/borewell).
  - Preference given to small and marginal farmers.
- **Benefits**: Subsidized installation of 3 HP, 5 HP, or 7.5 HP standalone solar pumps.
- **Subsidy / Financial Information**: Up to **60% total subsidy** (30% Central Government + 30% State Government). Farmer pays remaining 40% (bank loans available for 30%). Maximum subsidy cap up to ₹2,500,000 for community projects.
- **Applicable State**: Central Scheme with State implementations (e.g., Maharashtra MSEDCL / MEDA).
- **Equipment / Crop Applicability**: Standalone Solar Pumps, Submersible Solar Water Pumps.
- **Required Documents**: Aadhaar Card, Land Deed (7/12 extract), Bank Account details, Electricity bill / NOC (confirming no grid connection).
- **Application Information**: Official portal: `https://pmkusum.mnre.gov.in/`
- **Source**: `backend/database/supabase_master_schema.sql`, `backend/feature5/subsidy_service.py`
- **Data Status**: Existing project database record.
- **Recommended Usage**: RAG & ALIGNMENT.

---

### SMAM (Sub-Mission on Agricultural Mechanization)

- **Purpose**: Promoting agricultural mechanization among small and marginal farmers by subsidizing individual machinery purchases and setting up Custom Hiring Centers (CHC).
- **Eligibility**:
  - Small, Marginal, SC, ST, and Women farmers receive higher priority.
  - Must own cultivable land and have valid identity verification.
- **Benefits**: Financial assistance for purchasing tractors, power tillers, rotavators, sprayers, harvesters, and laser land levelers.
- **Subsidy / Financial Information**: **40% to 50% subsidy** for individual farmers (up to 50% for SC/ST/Women/Small farmers). Custom Hiring Centers receive up to 80% subsidy (max financial cap ₹1,200,000).
- **Applicable State**: All Indian States.
- **Equipment / Crop Applicability**: Tractors, Rotavators, Power Tillers, Seed Drills, Harvesters, Drone Sprayers.
- **Required Documents**: Aadhaar Card, Land Deed, Bank Passbook, Category Certificate (if SC/ST), Quotation from authorized machinery dealer.
- **Application Information**: Official portal: `https://agrimachinery.nic.in/`
- **Source**: `backend/database/supabase_master_schema.sql`, `backend/feature4/tools.py`
- **Data Status**: Existing project database record.
- **Recommended Usage**: RAG & ALIGNMENT.

---

### RKVY (Rashtriya Krishi Vikas Yojana)

- **Purpose**: Holistic development of agriculture and allied sectors by empowering states to choose localized agricultural infrastructure and farming projects.
- **Eligibility**:
  - Farmers engaged in agriculture, horticulture, dairy, goat farming, or organic farming.
  - Registered farmer producer organizations (FPO) or self-help groups (SHG).
- **Benefits**: Grants and equipment subsidies for micro-irrigation, polyhouse setup, cold storage, organic farming infrastructure.
- **Subsidy / Financial Information**: **25% to 50% subsidy** depending on project type and state guidelines.
- **Applicable State**: All States (State-executed scheme).
- **Equipment / Crop Applicability**: Polyhouses, Drip/Sprinkler Systems, Organic Inputs, Storage Infrastructure.
- **Required Documents**: Project report, Land documents, Aadhaar Card, Bank Passbook.
- **Application Information**: Official portal: `https://rkvy.nic.in/`
- **Source**: `backend/database/supabase_master_schema.sql`, `backend/feature4/tools.py`
- **Data Status**: Existing project database record.
- **Recommended Usage**: RAG & ALIGNMENT.

---

### NFSM (National Food Security Mission)

- **Purpose**: Increasing production of rice, wheat, pulses, coarse cereals, and commercial crops through area expansion and productivity enhancement.
- **Eligibility**:
  - Farmers growing focus crops in notified NFSM districts.
  - Priority for small and marginal landholders.
- **Benefits**: Subsidized high-yielding variety (HYV) seeds, soil amenders (micronutrients/gypsum), plant protection chemicals, and farm machinery.
- **Subsidy / Financial Information**: Direct financial subsidy ranging from **₹1,000 to ₹5,000 per hectare** or up to 50% on inputs.
- **Applicable State**: Specific notified districts across Indian states.
- **Equipment / Crop Applicability**: High-yielding Seeds, Bio-fertilizers, Micronutrients, Seed Drills.
- **Required Documents**: Farmer Registration ID, Land Deed, Aadhaar Card.
- **Application Information**: Official portal: `https://nfsm.gov.in/`
- **Source**: `backend/database/supabase_master_schema.sql`, `backend/feature4/tools.py`
- **Data Status**: Existing project database record.
- **Recommended Usage**: RAG & ALIGNMENT.

---

### AIF (Agriculture Infrastructure Fund)

- **Purpose**: Medium-to-long term debt financing facility for investment in viable projects for post-harvest management infrastructure and community farming assets.
- **Eligibility**:
  - Primary Agricultural Credit Societies (PACS), FPOs, Agri-entrepreneurs, Startups, Individual farmers.
- **Benefits**: Interest subvention of 3% per annum on loans up to ₹2 Crores for a maximum period of 7 years. Credit guarantee coverage under CGTMSE.
- **Subsidy / Financial Information**: **3% Interest Subvention** on bank loans up to ₹20,000,000.
- **Applicable State**: All States and UTs.
- **Equipment / Crop Applicability**: Warehouses, Silos, Cold Chain Infrastructure, Sorting & Grading Units.
- **Required Documents**: Detailed Project Report (DPR), Bank Loan Application, Land Deed/Lease Agreement, PAN Card, Aadhaar Card.
- **Application Information**: Official portal: `https://agriinfra.dac.gov.in/`
- **Source**: `backend/database/supabase_master_schema.sql`, `backend/feature4/tools.py`
- **Data Status**: Existing project database record.
- **Recommended Usage**: RAG & ALIGNMENT.

---

### PMFBY (Pradhan Mantri Fasal Bima Yojana - Crop Insurance)

- **Purpose**: Financial support to farmers suffering crop loss/damage arising out of unforeseen natural calamities, pests, and diseases.
- **Eligibility**:
  - All farmers including sharecroppers and tenant farmers growing notified crops in notified areas.
- **Benefits**: Comprehensive risk coverage for pre-sowing to post-harvest crop loss.
- **Subsidy / Financial Information**: Farmer pays nominal premium: **1.5% for Rabi crops, 2.0% for Kharif crops, and 5.0% for Commercial/Horticultural crops**. Remaining premium subsidized equally by Central and State Governments.
- **Applicable State**: Participating States.
- **Equipment / Crop Applicability**: Notified Food Crops, Oilseeds, Annual Commercial/Horticultural Crops.
- **Required Documents**: Land 7/12 extract / Sowing certificate, Aadhaar Card, Bank Passbook, Proposal form.
- **Application Information**: Official portal: `https://pmfby.gov.in/`
- **Source**: `backend/database/supabase_master_schema.sql` (`claim_applications` table)
- **Data Status**: Existing project database record.
- **Recommended Usage**: RAG & ALIGNMENT.

---

## 2. Subsidy Calculation Formulas

In `backend/feature5/subsidy_service.py`, subsidy calculation logic is implemented as:
$$\text{Subsidy Amount} = \min\left( \text{Equipment Cost} \times \frac{\text{Subsidy Percentage}}{100}, \text{Max Amount Cap} \right)$$
$$\text{Farmer Out-of-Pocket Share} = \text{Equipment Cost} - \text{Subsidy Amount}$$

---

## External Sources To Be Added Later
- IEEE/research papers: NOT YET PROVIDED
- Official agricultural guidelines: NOT YET PROVIDED unless already present
- Official government documents: NOT YET PROVIDED unless already present
