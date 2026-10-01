# 📢 SMS Broadcast System

I have implemented the **Admin Broadcast System**, allowing you to send SMS alerts to all registered farmers via Twilio.

## 🚀 Features
1.  **Region Targeting:** Send alerts to "All" or specific districts (Pune, Nashik, etc.).
2.  **Twilio Integration:** Uses Twilio SMS API for reliable delivery.
3.  **Automatic Simulation:** If Twilio keys are missing, the system **simulates** the broadcast (logging to console) so you can test the UI without cost.

## ⚙️ Configuration
To enable real SMS, add these to your `backend/.env`:
```env
TWILIO_ACCOUNT_SID=your_sid_here
TWILIO_AUTH_TOKEN=your_token_here
TWILIO_PHONE_NUMBER=your_twilio_number
```
If you have already "added them" (configured keys), the system will use them automatically.

## 📝 How to Use
1.  Go to **Admin Dashboard -> Broadcast**.
2.  Select **Region** (e.g., Pune) and **Alert Type** (e.g., Weather).
3.  Type your message.
4.  Click **"Send Broadcast"**.
5.  You will see a confirmation popup with the count of Sent/Failed messages.

## 🚜 Verification
-   **Real Mode:** Farmers will receive an SMS: `[WEATHER] Let's Go Alert: Heavy rain expected...`
-   **Sim Mode:** Check the backend terminal for logs: `📡 [SIMULATION] SMS to +9199...: ...`
