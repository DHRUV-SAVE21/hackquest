# 👮 Admin: Managing Claims & Dashboard
The Admin Panel is now **fully connected** to the live `claim_applications` database.

## 📊 Admin Dashboard
The main dashboard now reflects **real-time data** from the satellite claims system:
-   **Total Claims:** Counts submissions from the Satellite Monitor.
-   **Pending Approvals:** Shows claims waiting for your review.
-   **Disbursed Amount:** Sum of approved claim amounts.
-   **Recent Claims Table:** Shows the latest 10 submissions with:
    -   Farmer Name
    -   Scheme (e.g., PMFBY) & Crop
    -   Claim Amount (₹)
    -   Live Status (Submitted/Approved)

## 📍 Managing Claims (Claims Page)
1.  Navigate to `/admin/claims`.
2.  **Default View:** Shows **Submitted** claims.
3.  **Actions:**
    -   **View:** See full details & **Satellite Proof Image**.
    -   **Review:** Move to "Under Review".
    -   **Approve/Reject:** Finalize the claim.

## ⚙️ Technical Details
-   **Endpoint:** `/api/feature2/claims` & `/api/admin/recent-claims`
-   **Table:** `claim_applications`
-   **Docs:** Stored as Base64 Data URLs for instant viewing.
