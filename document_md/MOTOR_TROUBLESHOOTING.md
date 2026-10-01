# 🚜 Motor Control Troubleshooting

If your hardware motor is not turning on, follow these steps:

## 1. The Fix Introduced
We have switched from **Direct Browser Control** to **Backend Proxy Control**.
-   **Old Way:** Browser -> Motor IP (Blocked by Chrome/CORS/HTTPS) ❌
-   **New Way:** Browser -> Backend API -> Motor IP (Reliable) ✅

## 2. Requirements
-   **Backend Must Be Running:** Ensure `python main.py` is active.
-   **Same Network:** The computer running the backend MUST be on the same Wi-Fi/LAN as the Motor (IP `172.16.30.185`).
-   **IP Reachability:** Try pinging `172.16.30.185` from your terminal.

## 3. How to Test
1.  **Dashboard -> Primary Action:** Click **"Start Irrigation"**.
2.  **Dashboard -> Smart Controls:** Click **"P-1"** button.
3.  Check the **Backend Terminal**. You should see:
    ```
    📡 Sending command to Motor: http://172.16.30.185/motor/on
    ✅ Motor Response: 200
    ```
    If you see `❌ Motor Connection Failed`, the backend cannot see the device. Check your Wi-Fi connection.

## 4. Features Enabled
-   **Irrigate Button:** Start/Stop Motor.
-   **Pump 1 (P-1):** Start/Stop Motor (Synced with Irrigate backend logic).
-   **Pump 2 & 3 (P-2, P-3):** Simulated only (UI toggle).
