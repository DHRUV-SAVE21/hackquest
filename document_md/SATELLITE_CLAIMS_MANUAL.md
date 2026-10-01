# 🛰️ Satellite-Based Claim Application
This feature allows farmers to apply for crop loss insurance using **Real-Time Satellite Data** as proof.

## ✅ New Capabilities
1.  **Auto-Captured Satellite Proof**: When you click "Apply for Claim" from the Satellite Monitor, the system now **captures the satellite analysis image** and auto-attaches it to your claim form as proof.
2.  **Profile Data Integration**: Your personal details (Name, Aadhaar, Bank Info) are fetched securely from the backend.
3.  **Automatic Loss Calculation**: The system estimates your claim amount in **Indian Rupees (₹)**.
    *   **Formula:** `₹50,000 (Avg Value/Acre) × Land Size × Loss %`

## 🛠️ How to Test
1.  **Complete Profile**: Ensure your Farmer Profile is saved (refresh to verify persistence).
2.  **Monitor Crop**: Go to **Satellite Monitor** -> Select Area -> Get Analysis.
3.  **Apply**: Click **"Apply for Claim"**.
4.  **Verify**:
    *   Check that "Farmer Details" are auto-filled (check browser console if N/A).
    *   Check that the **Satellite Image** is attached in the documents section.
    *   Check the **Estimated Claim Amount** in ₹.
    *   Click Submit.

## 🐛 Troubleshooting "N/A" Errors
If you still see "N/A" in farmer details:
1.  Open Browser Console (F12).
2.  Look for logs starting with `Fetching profile for UserID:` and `Profile Data Received:`.
3.  If `userID` is "default" but you expected a real ID, try logging out/in or saving profile again.
4.  If `Profile Data Received` is correct but UI is N/A, check if fields like `full_name` vs `name` are matching.
