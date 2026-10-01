# Sensor Integration Complete ✅

## Hardware Sensor IP: 10.110.7.93:8000

All sensor URLs have been updated to use the new hardware IP address.

---

## 📡 Updated Endpoints

### NPK & Soil Sensors
**Endpoint:** `http://10.110.7.93:8000/api/hardware/latest?user_id=HARDWARE_DEFAULT`

**Response Format:**
```json
{
  "status": "success",
  "data": {
    "soil_moisture": 45,
    "temperature": 28,
    "humidity": 65,
    "nitrogen": 55,
    "phosphorus": 35,
    "potassium": 42,
    "ph": 6.8,
    "created_at": "2026-02-20T10:00:00Z"
  }
}
```

### Fire & Gas Detection
**Endpoint:** `http://10.110.7.93:8000/api/hardware/fire-gas/latest`

**Response Format:**
```json
{
  "d0": 350,
  "status": "safe"
}
```

**Fields:**
- `d0`: MQ2 gas sensor value (PPM)
- `status`: Fire detection status ("safe", "fire", "detected")

---

## 🔄 Updated Files

### Frontend Components

1. **FarmerDashboard.jsx** ✅
   - Updated sensor data fetch URL
   - Displays NPK values in real-time

2. **CropRecommendation.jsx** ✅
   - Auto-fills form with sensor data
   - Polls every 5 seconds

3. **FarmDashboard.jsx** (Feature 3) ✅
   - Real-time sensor monitoring
   - Decision engine integration

4. **FireDetectionCard.jsx** ✅
   - Updated to use fire-gas endpoint
   - Reads `status` field for fire detection

5. **GasMonitoringCard.jsx** ✅
   - Updated to use fire-gas endpoint
   - Reads `d0` field for MQ2 gas value

6. **FireGasMonitor.jsx** (NEW) ✅
   - Combined fire and gas monitoring
   - Real-time alerts
   - Visual indicators with color coding

---

## 🎨 Fire & Gas Monitor Features

### Fire Detection
- **Status Indicators:**
  - ✅ Safe (Green) - No fire detected
  - 🔥 Alert (Red, Pulsing) - Fire detected

- **Data Source:** `status` field from API
- **Update Frequency:** Every 2 seconds

### Gas Detection (MQ2 Sensor)
- **Levels:**
  - 🟢 Safe: < 300 PPM
  - 🟡 Moderate: 300-600 PPM
  - 🟠 High: 600-900 PPM
  - 🔴 Critical: > 900 PPM

- **Data Source:** `d0` field from API
- **Update Frequency:** Every 2 seconds

### Visual Features
- Real-time value display
- Color-coded status indicators
- Progress bar showing gas levels
- Animated alerts for dangerous conditions
- Last updated timestamp

---

## 📊 Integration Points

### Where Sensors Are Used

1. **Farmer Dashboard**
   - Main dashboard with NPK cards
   - Real-time soil moisture, N, P, K values
   - Auto-refresh every 5 seconds

2. **Crop Recommendation**
   - Auto-fills soil parameters
   - Uses sensor data for ML predictions
   - Syncs with hardware every 5 seconds

3. **Autonomous Farm (Feature 3)**
   - Decision engine for irrigation
   - Fertilizer recommendations
   - Real-time monitoring

4. **Fire & Gas Safety**
   - Warehouse monitoring
   - Emergency alerts
   - Safety dashboard

---

## 🚀 How to Use

### Display Fire & Gas Monitor

Add to any page:
```jsx
import FireGasMonitor from './components/features/FireGasMonitor';

function MyPage() {
  return (
    <div>
      <FireGasMonitor />
    </div>
  );
}
```

### Access Sensor Data Directly

```javascript
// NPK & Soil Data
const response = await fetch('http://10.110.7.93:8000/api/hardware/latest?user_id=HARDWARE_DEFAULT');
const data = await response.json();
console.log(data.data.nitrogen); // N value
console.log(data.data.phosphorus); // P value
console.log(data.data.potassium); // K value

// Fire & Gas Data
const fireGasResponse = await fetch('http://10.110.7.93:8000/api/hardware/fire-gas/latest');
const fireGasData = await fireGasResponse.json();
console.log(fireGasData.d0); // MQ2 gas value
console.log(fireGasData.status); // Fire status
```

---

## ⚠️ Important Notes

### Network Requirements
- Frontend must be able to reach `10.110.7.93:8000`
- Ensure hardware device is on same network or accessible
- Check firewall rules if connection fails

### CORS Configuration
If you get CORS errors, the backend at `10.110.7.93:8000` needs to allow your frontend origin:

```python
# On hardware backend
app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],  # Or specific frontend URL
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

### Fallback Behavior
- If hardware is offline, components show "Sensor Offline" message
- Error handling prevents app crashes
- Loading states while fetching data

---

## 🧪 Testing

### Test NPK Sensors
```bash
curl http://10.110.7.93:8000/api/hardware/latest?user_id=HARDWARE_DEFAULT
```

### Test Fire & Gas
```bash
curl http://10.110.7.93:8000/api/hardware/fire-gas/latest
```

### Expected Responses

**NPK Sensors (Success):**
```json
{
  "status": "success",
  "data": {
    "nitrogen": 55,
    "phosphorus": 35,
    "potassium": 42,
    "soil_moisture": 45,
    ...
  }
}
```

**Fire & Gas (Success):**
```json
{
  "d0": 350,
  "status": "safe"
}
```

---

## 📝 Summary

✅ All sensor URLs updated to `10.110.7.93:8000`
✅ NPK values displayed in dashboard
✅ Fire detection integrated
✅ Gas monitoring (MQ2) integrated
✅ Real-time updates every 2-5 seconds
✅ Error handling and fallbacks
✅ Visual indicators and alerts
✅ New FireGasMonitor component created

**Status:** Production Ready 🎉

---

**Last Updated:** February 20, 2026
**Hardware IP:** 10.110.7.93:8000
**Integration:** Complete ✅
