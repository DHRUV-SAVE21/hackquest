# 📄 Viewing Claim Documents
I have fixed the issue where documents were not viewable in the Admin Panel.

## 🛠️ The Fix
- **Previously:** The system was only saving "metadata" (e.g., "Has Land Doc: Yes") instead of the actual file.
- **Now:** The system converts your uploaded photos (and the satellite proof) into **secure digital formats (Base64)** and stores them directly with the claim.

## 🔄 How to Verify
1.  **Submit a NEW Claim**:
    *   Old claims will still show broken/empty docs because the data wasn't saved.
    *   Go to **Satellite Monitor** -> Apply Claim.
    *   Ensure the "Satellite Proof" is attached.
    *   (Optional) Upload another photo.
    *   Submit.
2.  **Go to Admin Panel**:
    *   Navigate to `/admin/claims`.
    *   Find your **NEW** claim (top of the list usually, or search).
3.  **View Docs**:
    *   Click **View**.
    *   Scroll to "Uploaded Documents".
    *   Click the **"View" button** next to any document.
    *   It should verify the satellite image or any photo you uploaded! 📸

## ⚠️ Note on File Size
Since we are storing files directly in the database for this demo, please upload **small files** or rely on the auto-captured satellite proof to keep specific actions fast.
