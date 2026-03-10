# TASNI Cloud Dashboard

Live plant moisture monitoring — accessible from anywhere in the world.

**Live URL:** `https://tasni-cloud.github.io`

---

## How It Works

```
ESP32 Sensor  →  HiveMQ Cloud (MQTT)  →  This page (WebSocket)  →  Customer's phone
```

- ESP32 publishes a JSON payload to `tasni/<deviceID>/state` every 30 seconds
- This page subscribes via MQTT over WebSocket (no server needed)
- Everything runs in the browser — zero backend, zero hosting cost

---

## Deploy in 5 Minutes

1. Create a free account at [hivemq.com/mqtt-cloud-broker](https://www.hivemq.com/mqtt-cloud-broker/)
2. Create a cluster — get your broker hostname, username, password
3. Fork this repo → rename to `<your-github-username>.github.io`
4. Enable GitHub Pages → Source: main branch, root folder
5. Enter broker details in your TASNI device Setup page → Cloud Dashboard section
6. Share `https://<your-username>.github.io?device=<deviceID>` with your customer

---

## URL Parameters

The device's **My URL** button opens the dashboard with the device ID prefilled:

```
https://tasni-cloud.github.io?device=A1B2C3
```

Customers enter their broker credentials once — stored in browser localStorage.

---

## Data Format (MQTT Payload)

Topic: `tasni/<deviceID>/state`

```json
{
  "device": "A1B2C3",
  "name": "Soil Sensor",
  "moisture": 65,
  "status": "Good",
  "raw": 512,
  "trend": "^",
  "rssi": -58,
  "heap": 187432,
  "uptime": 3720,
  "cal": 1,
  "dry": 850,
  "wet": 400,
  "boot": 3,
  "ts": "11-03-2026 14:32:10",
  "fw": "11.2.0-SINGLE"
}
```

---

## Files

| File | Purpose |
|---|---|
| `index.html` | Complete single-page dashboard (HTML + CSS + JS) |
| `README.md` | This file |

No build step. No npm. No dependencies except Paho MQTT JS from CDN.
