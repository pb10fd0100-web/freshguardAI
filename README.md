# FreshGuard — AI Multi-Zone Cold Storage Digital Twin

**FreshGuard** is an AI-driven multi-zone cold-storage retrofit controller designed for small and mid-size fruit and vegetable cold rooms in India. This repository contains the complete, self-contained 3D WebGL digital twin, headless physics & benchmark suite, and exportable pure-JS controller (`controller.js`).

## Key Capabilities
- **Split-Screen 3D Digital Twin (Three.js r128):** Side-by-side comparison of a fair baseline (**Tuned Thermostat**, **Rule-Based Expert**, or **Naive Legacy**) vs. **FreshGuard AI** across 3 PVC-partitioned produce zones:
  - **Zone A — Leafy Greens** (0–4 °C, 95–100% RH, overhead mist sprayers)
  - **Zone B — Mature-Green Tomatoes** (12–13 °C, >10 °C chilling limit, overhead ethylene exhaust hood)
  - **Zone C — Bananas** (13–14 °C, >12 °C chilling limit, yellow grow/ripening lights + gas manifold)
- **Real Perceive → Estimate → Learn → Decide → Act Pipeline:**
  - `Sensors`: Noisy, drifting, quantized SHT31/MQ-style readings with dropouts and optional stuck-sensor faults.
  - `Estimator`: Per-zone Kalman Filter with innovation-gated fault detection and redundant-sensor fallback.
  - `Controllers`: Online diagonal RLS spoilage learner + rolling-horizon Model Predictive Control (MPC) with weather/outage forecast anticipation, explainability log, **Remove AI** ablation toggle, **Shadow Mode**, and hard safety interlocks.
- **Headless Paired Benchmark & Self-Tests:** Runs 5–100 paired deterministic seeds × 7 simulated days across 9 stress scenarios without freezing the UI, with CSV/JSON export and 5 automated PASS/FAIL self-tests.
- **Sim-to-Real Layer:** Pure `decide(obs, state, cfg)` function exportable as standalone `controller.js`, live MQTT-style JSON telemetry stream, and ~₹12,500 3-zone ESP32 retrofit BOM.

## Quick Deploy (GitHub + Netlify)
1. Upload all files in this folder (`index.html`, `netlify.toml`, `README.md`, `.gitignore`) to a new GitHub repository.
2. Open [Netlify](https://app.netlify.com/) → **Add new site** → **Import an existing project** → connect your GitHub repo.
3. Leave **Build command** empty and set **Publish directory** to `.` (auto-detected from `netlify.toml`), then click **Deploy site**.

## Local Run
Open `index.html` directly in Chrome, Edge, or Safari (desktop or mobile). No build step or `npm install` required.

## Honest Note
All benchmark metrics and savings displayed in the simulator are **simulation results, not field data**, based on post-harvest literature ranges and assumed wholesale/tariff values (editable in the **Biz/Info** tab).

## Team
- **Bhavya Jain** — Tech, Simulation & AI Controller
- **Arjun Kashyap** — Customer Research & Pitch
