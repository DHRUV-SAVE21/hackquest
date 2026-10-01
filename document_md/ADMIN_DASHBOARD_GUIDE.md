# 📊 Admin Dashboard: Full Integration
The Admin Dashboard is now connected to live satellite claim data.

## ✅ Live Data Sources
1.  **Total Claims & Pending Approvals:** Counts directly from `claim_applications` table.
2.  **Recent Claims List:** Shows the last 100 submissions with:
    -   Farmer Name
    -   Scheme & Crop
    -   Amount
    -   Status
3.  **Claims Velocity Chart:** Visualizes submission trends over the last 7 days.

## 👁️ Features
-   **View Button:** Each row in "Recent Claims" has an **Eye Icon**.
    -   Clicking it navigates to the main `/admin/claims` page where you can see full details and approve/reject.
-   **Auto-Update:** Dashboard polls for new data every 30 seconds.

## 🔄 How to Verify
1.  Submit a new claim from **Satellite Monitor**.
2.  Go to **Admin Dashboard**.
3.  You should see the "Total Claims" count increase.
4.  You should see your new claim at the top of "Recent Claims".
5.  Click the **Eye Icon** to manage it.
