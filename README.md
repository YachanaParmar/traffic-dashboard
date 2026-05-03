# TRAFFIQ.AI — Predictive Traffic Congestion Intelligence System

A real-time, AI-powered traffic intelligence dashboard that fuses **CCTV computer vision**, **GPS/Maps API data**, and **LSTM neural networks** to predict urban traffic congestion 15–45 minutes in advance.

---

## 🚦 Live Demo

> Open `index.html` directly in any modern browser (Chrome / Edge recommended).

---

## 🧠 Problem Statement

Modern traffic management systems are **reactive** — they detect jams only after they have formed. This system solves that by building a **predictive, multi-source fusion model** that combines:

- **Macro-level GPS data** (Google Maps API) — city-wide speed and flow
- **Micro-level visual data** (CCTV + YOLOv8) — ground truth vehicle density and anomaly detection
- **Temporal forecasting** (LSTM) — predicts how a localized bottleneck will ripple across the road network

---

## ⚙️ Tech Stack & Architecture

| Layer | Technology | Role |
|---|---|---|
| Computer Vision | YOLOv8 / Faster R-CNN | Vehicle detection, density calculation, anomaly identification |
| Geospatial API | Google Maps Routes API | Network-wide traffic baseline, ETA, congestion alerts |
| Prediction Engine | LSTM / RNN | Forecasts standstill probability 15–45 min ahead |
| Fusion Layer | Cross-modal correlation | Validates GPS alerts against CCTV visual counts |
| Frontend | HTML5 Canvas + Chart.js | Real-time interactive geospatial dashboard |

---

## ✨ Key Features

- **Live Geospatial Map** — 14 traffic nodes color-coded by congestion level across Bengaluru Metro (124 km²)
- **CCTV Node Inspector** — Click any feed to open a detailed CV detection modal with vehicle count, speed, and anomaly notes
- **LSTM Prediction Bars** — Real-time standstill probability for 5 major corridors (8–45 min horizon)
- **Three Map Layers** — Traffic view, LSTM Predicted hotspots, and Heat Map overlay
- **15-Minute Forecast Chart** — Congestion index trend with danger threshold line
- **Cross-modal Fusion Status** — Live pipeline status for GPS sync, CV engine, LSTM, and fusion layer
- **Simulation Controls** — Adjust traffic volume and inject incidents to test prediction response
- **Live Event Feed** — Real-time anomaly alerts, jam predictions, and resolution notices

---

## 🗺️ System Architecture

```
┌─────────────────────────────────────────────────────┐
│                   Data Ingestion Layer               │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐ │
│  │ Google Maps │  │ CCTV Feeds  │  │  IoT / GPS  │ │
│  │ Routes API  │  │  (IP Cams)  │  │   Sensors   │ │
│  └──────┬──────┘  └──────┬──────┘  └──────┬──────┘ │
└─────────┼────────────────┼────────────────┼─────────┘
          │                │                │
┌─────────▼────────────────▼────────────────▼─────────┐
│                Cross-Modal Fusion Layer              │
│         GPS Congestion ←→ CV Vehicle Count          │
│              False Positive Elimination              │
└─────────────────────────┬───────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────┐
│              LSTM Prediction Engine                  │
│   Input: t-2, t-1 states → Output: t+15 to t+45    │
│   Standstill Probability per Road Corridor          │
└─────────────────────────┬───────────────────────────┘
                          │
┌─────────────────────────▼───────────────────────────┐
│           Interactive GIS Dashboard (UI)             │
│  Live Map · CCTV Feeds · Predictions · Event Feed   │
└─────────────────────────────────────────────────────┘
```

---

## 📊 Dashboard Panels

### Left Panel
- **Live Network Metrics** — Vehicle count, average speed, congestion zones, clear roads
- **CCTV Node Feeds** — 4 live simulated feeds with CV detection overlay
- **15-Min LSTM Forecast** — Congestion index chart with danger threshold
- **Fusion Pipeline Status** — Real-time status of all data sources

### Center — Geospatial Map
- Interactive node map with hover tooltips
- Three switchable layers: Traffic / Prediction / Heat Map
- Predicted hotspots shown as dashed cyan markers

### Right Panel
- **Standstill Probability** — Per-road LSTM predictions with confidence scores
- **YOLOv8 Detection Summary** — Cars, bikes, trucks, anomalies count
- **Live Event Feed** — Timestamped alerts and system events
- **Simulation Controls** — Volume slider + incident injection

---

## 🚀 How to Run

### Option 1 — Local (Instant)
```bash
# Just download and open
open index.html   # macOS
start index.html  # Windows
```
No server, no dependencies, no installation required.

### Option 2 — GitHub Pages (Live Link)
1. Fork or clone this repository
2. Go to **Settings → Pages → Source → main branch**
3. Your live URL: `https://yourusername.github.io/traffic-dashboard`

---

## 📁 Project Structure

```
traffic-dashboard/
│
├── index.html          # Complete dashboard (single-file application)
└── README.md           # Project documentation
```

---

## 🔬 Model Logic

### LSTM Prediction
The prediction engine uses the node's last two known states (t-2 and t-1) to forecast the congestion index at t+15 through t+45 minutes:

```
Input  → [density(t-2), speed(t-2), density(t-1), speed(t-1), road_type, time_of_day]
Output → [jam_probability(t+15), jam_probability(t+30), jam_probability(t+45)]
```

### Cross-Modal Validation
Before raising a congestion alert, the fusion layer cross-validates:
- GPS shows red segment (slow speed) **AND**
- CCTV CV detects high vehicle density (>60%)
- If only one source triggers → flagged as potential false positive

### Congestion Levels
| Level | Speed | Density | Action |
|---|---|---|---|
| Level 1 — Free Flow | >60 km/h | <20% | No action |
| Level 2 — Moderate | 40–60 km/h | 20–40% | Monitor |
| Level 3 — Heavy | 20–40 km/h | 40–70% | Alert issued |
| Level 4 — Severe | 8–20 km/h | 70–90% | Prediction triggered |
| Level 5 — Standstill | <8 km/h | >90% | Emergency alert |

---

## 📸 Screenshots

> Dashboard running in browser — live geospatial map with CCTV feeds, LSTM predictions, and event feed.

---

## 👤 Author

Built as part of an AI/ML engineering assessment.  
Stack: HTML5 · JavaScript · Canvas API · Chart.js · LSTM · YOLOv8 · Google Maps API

---

## 📄 License

MIT License — free to use and modify.
