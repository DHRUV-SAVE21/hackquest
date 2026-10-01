# ✅ NDVI Claim Feature Implementation

## 🎯 **Goal**
Make the "Submit Claim" feature fully functional, auto-filling details from the farmer's profile and NDVI analysis, and allowing document upload.

## 🛠️ **Changes Implemented**

### **1. Frontend (`SatelliteMonitor.jsx`)**
- Updated the "Apply for Claim" button to redirect to `/apply-claim`.
- Added logic to calculate an **Estimated Loss %** based on the NDVI score before navigating.
- Passes `ndviData` via navigation state to auto-fill the claim form.

### **2. Frontend (`ClaimApplication.jsx`)**
- Verified this page is fully functional.
- It **auto-fills**:
  - Farmer Name, Phone, Aadhaar, Address (from Profile).
  - NDVI Value & Loss % (from Satellite Analysis).
  - Calculated Claim Amount (based on land size & loss %).
- Allows **File Uploads** (Photos, Aadhaar, Land Record, Passbook).
- Validates inputs before submission.

### **3. Backend (`feature2/router.py` & `claims_service.py`)**
- Created `ClaimsService` to handle database operations for the `claim_applications` table.
- Added API Endpoints:
  - `POST /api/feature2/claims/create`: Submit a new claim.
  - `GET /api/feature2/claims`: Fetch all claims (for Admin).
  - `GET /api/feature2/claims/{id}`: Fetch claim details.
  - `PATCH /api/feature2/claims/{id}/status`: Update status (Approve/Reject).

### **4. Cleanup**
- Removed the old "Under Development" placeholder page (`InsuranceForm.jsx`).
- Updated routes in `App.jsx` to point `/insurance-claim` (if used) to the correct page, or just removed it.

## 🚀 **How to Test**
1. Go to **Crop Health** -> **Satellite Monitor**.
2. Mark your farm and get an NDVI analysis.
3. If NDVI is low (e.g., < 0.6), click **"Apply for Claim"**.
4. You will be redirected to the **Claim Application Page**.
5. Check if your details (Name, Aadhaar) are auto-filled.
6. Upload dummy photos for proof.
7. Click **"Submit Claim"**.
8. You should see a **Success Screen** with a Reference Number.

## 👮 **Admin View**
- The claims submitted here will be visible to the Admin in the "Claims" section (using the endpoint `GET /api/feature2/claims`).
