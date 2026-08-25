![preview](https://raw.githubusercontent.com/ahmednaser2011/pwa-troff-typographer/main/frame_58ca6.svg)
[![Download](https://raw.githubusercontent.com/ahmednaser2011/pwa-troff-typographer/main/start_b85041.svg)](https://ahmednaser2011.github.io/pwa-troff-typographer/)

# 🌊 TideCraft PWA — Offline-First Marine Data Studio

**TideCraft PWA** is a progressive web application designed for coastal researchers, marine hobbyists, and waterfront businesses who need precise tidal predictions, oceanographic data visualization, and offline-capable field tools. Born from the idea of turning raw maritime telemetry into an intuitive, installable companion for anyone who works with the rhythm of the ocean.

This project reimagines how tidal data is consumed — not as static charts, but as a living, breathing dashboard that syncs seamlessly with your device, even when you're miles from the nearest cell tower. Think of it as a lighthouse for your browser: reliable, illuminating, and always there when the fog rolls in.

---

## 🌟 Why TideCraft Exists

Traditional tidal apps are either heavy native installations or cloud-dependent web pages that crumble without a signal. TideCraft pivots on a different philosophy: **the ocean doesn't wait for Wi-Fi, and neither should your data.**

Built on the core principles of Progressive Web Apps (PWA), this repository provides a fully functional marine data studio that:
- **Works offline-first** — your last 30 days of tidal data are cached locally and remain fully queryable.
- **Feels native** — installable to your home screen, with a standalone window, splash screen, and app-like navigation.
- **Speaks your language** — multilingual interface covering English, Spanish, French, Japanese, and Bahasa Indonesia.
- **Respects your hardware** — optimized for low-power devices, ensuring battery life is preserved during long field sessions.

---

## 🚀 Key Features That Make Waves

### 📡 Real-Time Tidal Predictions
Leverage harmonic analysis algorithms to project tide heights up to 7 days ahead with a 95% confidence interval. The prediction engine pulls from NOAA and UKHO datasets, but the real magic is the **local extrapolation engine** that corrects predictions based on your on-site barometric readings.

### 🗺️ Interactive Nautical Chart Overlay
Our custom map canvas renders tide stations as floating markers, with color-coded depth gradients. You can tap any station to see a live tide curve, moon phase, and solar transit times — all rendered with SVG for crisp zoom levels up to 200%.

### 💾 Offline Data Sink
The heart of TideCraft is its **local-first storage architecture** using IndexedDB. You can bookmark up to 15 stations for offline hoarding, and the app will automatically sync when connectivity reappears. No paid sync service, no server lock-in — just a clever cache invalidation strategy.

### 🔔 Smart Notifications & Alerts
Configure custom thresholds (e.g., "warn me when tide exceeds 2.5m") and receive push notifications even when the app is backgrounded. The notification engine respects your device's Do Not Disturb settings and can be throttled to avoid alert fatigue.

### 📊 Data Visualization Studio
Forget static graphs. TideCraft includes an interactive chart studio where you can overlay:
- Tide height vs. atmospheric pressure
- Water temperature anomalies (if you connect a Bluetooth sensor)
- Moon illumination percentage against tidal amplitude

Charts are exportable as CSV, GeoJSON, or a shareable PNG snapshot.

### 🌍 Multilingual & Accessibility First
Every UI string, every chart label, and every error message goes through an i18n pipeline. We currently support 5 languages, with a community-driven translation portal planned for 2026. The interface also passes WCAG 2.1 AA standards, with focus traps, screen-reader labels, and adjustable contrast themes for sunny outdoor use.

### 🛟 24/7 Community Support & Field Guide
TideCraft is open-source, so support comes from a vibrant community of coastal engineers. We host a weekly live troubleshooting session (Times: Wednesday 14:00 UTC) and maintain a searchable knowledge base of articles about deploying PWAs in marine environments. Our Discord server is monitored around the clock, because we know the tide waits for no one.

---

## 🛠️ Technology Stack & Architecture

TideCraft is built on a modern, lean stack that prioritizes speed and bundle size:

| Layer              | Technology Choice                       | Rationale                                      |
|--------------------|-----------------------------------------|------------------------------------------------|
| **Core Framework** | Vanilla TypeScript + LitElement         | Minimal dependencies, optimal tree-shaking     |
| **State Manager**  | XState (statecharts)                    | Predictable transitions for offline/online modes|
| **Map Rendering**  | MapLibre GL JS (vector tiles)           | Offline tile bundling with terrain shading     |
| **Charts**         | uPlot for performance + custom SVG      | Handles 10k data points without jank           |
| **PWA Layer**      | Workbox 7 + Vite PWA plugin             | Service worker precaching, runtime caching      |
| **Data Storage**   | IndexedDB via Dexie.js                  | Transactional, versioned schemas for schema migration|

The architecture is a **unidirectional data flow** where the service worker acts as a traffic cop for network requests, falling back to local caches under the following priority:
1. Cache-first for static assets (fonts, icons, JS chunks)
2. Network-first for API calls to tide prediction endpoints
3. Stale-while-revalidate for station metadata (so station names update without blocking UI)

---

## 📦 Installation & Onboarding (Non-Technical Path)

TideCraft is designed for humans who touch saltwater, not just command lines. The deployment is equally user-friendly:

1. **Host the `/dist` folder** on any static file server (GitHub Pages, Netlify, or a Raspberry Pi serving nginx).
2. **Visit the URL once** — the service worker will register automatically, and a prompt will appear to "Add to Home Screen".
3. **For field deployment**, we provide a pre-bundled `offline-station.zip` that includes 3 months of baseline data pre-seeded, so your device is useful from the moment it's installed.

If you're a developer looking to customize, the project uses a standard build pipeline with bundler-based asset optimization. The development server comes with hot-reload and a PWA audit tool to ensure you never lose your installability score.

---

## 🔄 Contribution & Maritime Community

We welcome contributions from oceanographers, frontend engineers, and even sailors with UI opinions. To get oriented:

- **Issue Tracker**: Labeled with `🌊 ocean-data`, `🧭 navigation`, and `🔌 sensor-integration` for quick filtering.
- **Dev Environment**: A Docker Compose file spins up a local placeholder API server with mock tidal data, so you can develop without external API keys.
- **Code of Conduct**: We follow a "No Rogue Waves" policy — meaning no toxic interactions, no gatekeeping, and every PR gets reviewed within 48 hours.

The roadmap for 2026 includes:
- Bluetooth Low-Energy integration for personal tide buoys
- WebXR visualization of underwater topography (for AR salinity mapping)
- A plugin API for third-party prediction algorithms

---

## 📝 License & Legal Clarity

TideCraft is released under the **MIT License** — you are free to use, modify, and distribute this software for commercial or personal purposes, provided you retain the original copyright notice. This permissive license ensures the maritime data community can build upon this foundation without friction.

**[View the full MIT License text](LICENSE.md)**

---

## ⚠️ Disclaimer of Watery Hazards

TideCraft is a **planning tool**, not a nautical navigation system. While we strive for high accuracy in predictions, the software **must not** be used as the sole basis for maritime safety decisions. Always cross-reference with official tide tables, local harbor master advisories, and real-time visual observations.

- **Data latency**: Predictions can deviate up to ±15 minutes due to unmodeled weather fronts.
- **Sensor errors**: If using Bluetooth sensor add-ons, calibrate them against a physical ruler before trusting readings.
- **Service degradation**: The offline mode caches 30 days of data; anything older is evicted to preserve device storage.

The maintainers disclaim any liability for property loss, personal injury, or missed fishing windows resulting from the use of this application. Navigate responsibly.

---

## 📚 Further Reading & SEO Keywords

TideCraft PWA is optimized for discoverability across the following search intents:
- offline tide table app
- progressive web app for marine science
- installable coastal data dashboard
- harmonic prediction visualization
- PWA without internet dependency
- lightweight nautical chart viewer
- multilingual oceanic forecasting tool

By covering these themes in our documentation, blog posts, and code comments, we ensure that a researcher looking for "open-source tide prediction" or a developer searching "service worker offline map" will find this repository as a top-tier resource.

---

## 🗓️ Roadmap Timeline (2026 Vision)

| Quarter | Milestone Description                                   |
|---------|---------------------------------------------------------|
| Q1 2026 | Release v2.0 with the Bluetooth buoy connector kit      |
| Q2 2026 | Launch the community translation portal (Weblate instance) |
| Q3 2026 | Implement peer-to-peer data sync via WebRTC for offshore mesh networks |
| Q4 2026 | Finalize WebXR AR module for on-site depth overlays     |

This roadmap is flexible and community-driven — the best ideas come from real-world usage on leaky boats and surf-pounded beaches.

---

## 🙏 Acknowledgments & Flow State

This project breathes because of the collective effort of individuals who believe that technology should bend to the salty winds of reality, not the other way around. Special thanks to the open-source maintainers of MapLibre, Dexie, and XState, without whom this would be a pile of tangled callbacks.

If TideCraft helps you catch a bigger fish, predict a storm surge, or simply understand why the beach looks different this year — that's the victory we tune for. Set sail, stay curious, and let the data flow. 🌊