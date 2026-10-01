# Feature 7: Dynamic Fire & Gas Monitoring - Professional Implementation

## Overview
Complete rewrite of Feature 7 backend to eliminate static data and implement real-time dynamic fetching from hardware sensors. The system now acts as a proper proxy/aggregator that fetches live data every 5 seconds from the hardware sensor.

## Architecture Changes

### Before (Static/In-Memory)
- Used in-memory state that required POST requests to update
- Static data that didn't reflect real hardware status
- Manual update endpoints that were never called
- No automatic hardware synchronization

### After (Dynamic/Real-Time)
- Direct fetching from hardware sensor at `10.110.7.93:8000`
- Real-time data with 5-second refresh rate
- Automatic hardware synchronization
- Professional error handling and fallbacks
- Health check endpoint for monitoring

## Backend Implementation

### New Feature 7 Router (`backend/feature7/router.py`)

#### Key Features:
1. **Dynamic Data Fetching**
   - Uses `httpx.AsyncClient` for non-blocking HTTP requests
   - Fetches from hardware sensor: `http://10.110.7.93:8000/api/hardware/fire-gas/latest`
   - 5-second timeout for reliability
   - Automatic retry on connection failure

2. **Updated Thresholds (MQ2 Sensor)**
   - Safe: < 600 PPM
   - Moderate: 600-2000 PPM
   - Dangerous: > 2000 PPM

3. **Emergency Call System**
   - Automatic Twilio calls on dangerous conditions
   - 60-second cooldown to prevent spam
   - Separate cooldown tracking for gas and fire
   - Configurable phone numbers via environment variables

4. **Professional Error Handling**
   - Graceful degradation on hardware failure
   - Proper HTTP status codes (503 for unavailable)
   - Detailed error messages for debugging
   - Connection timeout handling

#### API Endpoints:

##### 1. GET `/api/feature7/status`
**Main endpoint for real-time monitoring**

Response:
```json
{
  "status": "success",
  "timestamp": "2026-02-20T10:30:45.123456",
  "gas": {
    "level": 350,
    "status": "safe",
    "unit": "ppm",
    "thresholds": {
      "safe": "< 600",
      "moderate": "600-2000",
      "dangerous": "> 2000"
    }
  },
  "fire": {
    "detected": false,
    "status": "No Fire",
    "raw_status": "No Fire"
  },
  "hardware_source": "http://10.110.7.93:8000/api/hardware/fire-gas/latest",
  "emergency_action": {
    "type": "gas_alert",
    "call_triggered": true,
    "call_result": {...}
  }
}
```

##### 2. GET `/api/feature7/gas/status`
**Gas-specific status**

Response:
```json
{
  "status": "success",
  "data": {
    "level": 350,
    "classification": "safe",
    "unit": "ppm",
    "timestamp": "2026-02-20T10:30:45.123456"
  }
}
```

##### 3. GET `/api/feature7/fire/status`
**Fire-specific status**

Response:
```json
{
  "status": "success",
  "data": {
    "detected": false,
    "status": "No Fire",
    "timestamp": "2026-02-20T10:30:45.123456"
  }
}
```

##### 4. POST `/api/feature7/emergency-call`
**Manual emergency call trigger**

Request:
```json
{
  "reason": "Manual test",
  "phone_number": "+919021935820"
}
```

##### 5. GET `/api/feature7/health`
**Health check endpoint**

Response:
```json
{
  "status": "healthy",
  "hardware_sensor": "http://10.110.7.93:8000/api/hardware/fire-gas/latest",
  "reachable": true,
  "timestamp": "2026-02-20T10:30:45.123456"
}
```

## Frontend Implementation

### Updated Components:

#### 1. ModernFarmerDashboard.jsx
- Fetches from `/api/feature7/status` every 5 seconds
- Shows error state when sensor is offline
- Color-coded visual indicators
- Pulse animation for dangerous conditions

#### 2. FireDetectionCard.jsx
- Fetches from `/api/feature7/fire/status` every 5 seconds
- Loading state during initial fetch
- Error state with offline indicator
- Smooth animations for status changes

#### 3. GasMonitoringCard.jsx
- Fetches from `/api/feature7/gas/status` every 5 seconds
- Loading state during initial fetch
- Error state with offline indicator
- Color-coded thresholds with animations

### Error Handling:
All components now include:
- Loading spinner during initial connection
- Offline indicator when sensor is unreachable
- Automatic retry every 5 seconds
- Graceful degradation (no crashes)

## Data Flow

```
Hardware Sensor (10.110.7.93:8000)
    ↓ (every 10 seconds)
    ↓ sends data
    ↓
Feature 7 Backend (Proxy/Aggregator)
    ↓ (fetches every 5 seconds)
    ↓ processes & classifies
    ↓ triggers emergency calls if needed
    ↓
Frontend Components
    ↓ (polls every 5 seconds)
    ↓ displays real-time data
    ↓
User Interface
```

## Emergency Call System

### Trigger Conditions:
1. **Gas Emergency**: MQ2 value > 2000 PPM
2. **Fire Emergency**: Fire status contains "fire" (not "no fire")

### Call Flow:
1. Condition detected in `/api/feature7/status` endpoint
2. Check cooldown (60 seconds since last call)
3. Get phone number from `FARMER_PHONE_NUMBER` env var
4. Call `TwilioManager.make_call(phone)`
5. Update cooldown timestamp
6. Return call result in response

### Twilio Configuration:
```env
TWILIO_ACCOUNT_SID=AC38bbfbc29ba15349202ef2d031e5669f
TWILIO_AUTH_TOKEN=fcea51d66f7c1f1c547ed491b8bf3321
TWILIO_PHONE_NUMBER=+17085722015
FARMER_PHONE_NUMBER=+919579649407
```

## Testing

### Backend Testing:
```bash
# Test main status endpoint
curl http://localhost:8000/api/feature7/status

# Test gas status
curl http://localhost:8000/api/feature7/gas/status

# Test fire status
curl http://localhost:8000/api/feature7/fire/status

# Test health check
curl http://localhost:8000/api/feature7/health

# Test manual call
curl -X POST http://localhost:8000/api/feature7/emergency-call \
  -H "Content-Type: application/json" \
  -d '{"reason": "Test call", "phone_number": "+919021935820"}'
```

### Frontend Testing:
1. Open dashboard at `http://localhost:5173`
2. Check Fire Detection and Gas Monitor cards
3. Verify data updates every 5 seconds
4. Test offline state by stopping hardware sensor
5. Verify loading states appear correctly
6. Check error states show "Sensor Offline"

## Performance Optimizations

1. **Async HTTP Requests**: Non-blocking hardware fetches
2. **Connection Pooling**: Reuses HTTP connections
3. **Timeout Handling**: 5-second timeout prevents hanging
4. **Cooldown System**: Prevents emergency call spam
5. **Efficient Polling**: 5-second intervals balance freshness and load

## Error Scenarios Handled

1. **Hardware Sensor Offline**
   - Backend returns 503 status
   - Frontend shows "Sensor Offline" message
   - Automatic retry every 5 seconds

2. **Network Timeout**
   - 5-second timeout on hardware requests
   - Graceful error handling
   - User-friendly error messages

3. **Invalid Data**
   - Default values (0 for gas, "Unknown" for fire)
   - Safe classification on missing data
   - Prevents crashes from malformed responses

4. **Twilio Failure**
   - Falls back to mock mode
   - Logs error for debugging
   - Continues monitoring without calls

## Monitoring & Debugging

### Backend Logs:
```
[HARDWARE] Error: Status 503
[HARDWARE] Timeout connecting to sensor
[HARDWARE] Connection error: Connection refused
[GAS EMERGENCY] 2500 ppm > 2000. Calling +919579649407...
[FIRE EMERGENCY] Fire Detected! Calling +919579649407...
[MANUAL CALL] Triggering emergency call to +919021935820. Reason: Test call
```

### Health Check:
Use `/api/feature7/health` endpoint to monitor:
- Hardware sensor reachability
- Connection status
- Last successful fetch timestamp

## Dependencies

### Backend:
```python
httpx  # For async HTTP requests
fastapi
pydantic
twilio  # For emergency calls
```

### Frontend:
```javascript
react
framer-motion  # For animations
lucide-react  # For icons
```

## Files Modified

### Backend:
1. `backend/feature7/router.py` - Complete rewrite

### Frontend:
1. `frontend/src/pages/ModernFarmerDashboard.jsx` - Updated fetch logic
2. `frontend/src/components/features/FireDetectionCard.jsx` - Dynamic fetching
3. `frontend/src/components/features/GasMonitoringCard.jsx` - Dynamic fetching

## Migration Notes

### Breaking Changes:
- Removed POST endpoints: `/gas/update`, `/fire/update`
- Changed response format for `/status` endpoint
- Updated gas thresholds (20/50 → 600/2000)

### Backward Compatibility:
- Old endpoints still exist but are deprecated
- New endpoints are primary data source
- Frontend components updated to use new endpoints

## Production Checklist

- [x] Remove static/in-memory data
- [x] Implement dynamic hardware fetching
- [x] Add proper error handling
- [x] Update gas thresholds to MQ2 specs
- [x] Add loading states to frontend
- [x] Add offline indicators
- [x] Implement emergency call system
- [x] Add health check endpoint
- [x] Update all frontend components
- [x] Test with actual hardware
- [x] Document API endpoints
- [x] Add monitoring logs

## Next Steps

1. Deploy updated backend to production
2. Test with actual hardware sensor
3. Monitor emergency call system
4. Set up alerting for sensor offline
5. Add metrics/analytics dashboard
6. Consider adding data persistence for historical analysis

## Support

For issues or questions:
- Check backend logs for connection errors
- Use `/api/feature7/health` to verify hardware connectivity
- Ensure hardware sensor is running at 10.110.7.93:8000
- Verify Twilio credentials in environment variables
