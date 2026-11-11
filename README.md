# Mars Explorer

A standalone Mars exploration dashboard with an interactive map, modeled surface conditions, a paged NASA rover-image archive, and a mission-history planner.

## Run locally

From this folder, run:

```bash
python -m http.server 5050 --bind 127.0.0.1
```

Then open [http://localhost:5050](http://localhost:5050). Python's built-in server is enough; the standalone site does not need Node.js or a NASA API key. An internet connection is required for map tiles, charts, fonts, and NASA images.

## 🌐 Features

| Feature | Description |
|---|---|
| 🗺️ Interactive Mars Map | Leaflet.js with NASA/USGS Mars tile layers |
| 📍 Route Planner | Click-to-add waypoints, auto distance & EVA duration |
| 🌡️ Atmospheric Conditions | Elysium Planitia climate estimates and a 7-sol history |
| 📸 Rover Photo Gallery | Paged NASA image archive for Curiosity, Perseverance, Opportunity, Spirit, and Sojourner |
| 🚀 Mission Planner | Active and historical rover records, waypoint export, and a science checklist |
| ♂ Mars Image Archive | NASA archive images filtered for real Mars surface scenes, with optional year search |
| 📊 Telemetry Charts | Temperature, pressure, wind trends |
| 💨 Wind Rose | Directional wind visualization |
| 🧑‍🚀 EVA Advisory | Go/No-Go system for extravehicular activities |

## Data notes

- Rover photos are historical images fetched from NASA's public Images and Video Library. They are not live rover-camera feeds. Use **Load more photos** to page through results.
- Rover dates, mission lengths, and distances are mission-history facts with links to NASA references.
- Mars weather and telemetry are modeled estimates, not live station readings. NASA's InSight weather service is retired.
- The optional Express API uses NASA's Mars Rover Photos endpoints and can be rate-limited when configured with `DEMO_KEY`. It is not required by this standalone page.

## 🖥️ Backend (Optional — Requires Node.js)

If you install Node.js, you can run the full Express backend:

```bash
cd server
npm install
npm run dev
```

The backend proxies all NASA API calls securely through:
- `GET /api/photos` — Mars Rover Photos
- `GET /api/weather` — InSight Weather
- `GET /api/apod` — Astronomy Picture of the Day
- `GET /api/mars-data` — Landing sites & regions
- `GET /api/manifest?rover=curiosity` — Rover manifests

## 📡 NASA APIs Used

1. **Mars Rover Photos API** — `api.nasa.gov/mars-photos`
2. **NASA Image and Video Library** — Mars surface and rover image archive
3. **Mars WMTS Tiles** — NASA/USGS Mars Viking Global Color Mosaic

## 🎮 How to Use

### Surface Map
- Toggle layers (landing sites, regions of interest)
- Click **Add Waypoint** to enter route planning mode
- Click anywhere on Mars to place waypoints
- Route distance and EVA time are auto-calculated

### Rover Gallery
- Choose Curiosity, Perseverance, Opportunity, Spirit, or Sojourner and select **Find photos**
- Browse archived NASA images and use **Load more photos** to fetch another page
- Click a photo to view its full-resolution NASA image

### Mission Planner
- Review active and completed rover missions, landing sites, milestones, and NASA source links
- Browse photos for any rover directly from its mission card
- Track your planned route waypoints
- Check off science objectives with progress tracking
- Export a route as JSON after adding waypoints on the Surface Map

### Atmospheric Conditions
- Mars local solar time at Elysium Planitia and consistent modeled surface conditions
- Seven-sol temperature, pressure, and wind history; estimates are not live telemetry
- EVA planning guidance is illustrative, not operational safety advice
- Wind rose directional diagram

### Mars Image Archive
- Browse NASA Mars landscape and surface scenes; concept art, Earth-based tests, and hardware-only images are filtered out
- Optionally filter by archive year, or choose a random matching scene
- Click **Random Mars Image** to discover another Mars scene

### Telemetry Dashboard
- Charts for temperature, pressure, and wind over 7 sols
- Mars planetary fact sheet

## 📁 Project Structure

```
mars-explorer/
├── index.html          # Main HTML (standalone web app)
├── styles.css          # Optional legacy stylesheet
├── app.js              # Optional legacy NASA API integration
├── README.md           # This file
└── server/             # Optional Express API backend
    ├── .env            # API keys (NASA_API_KEY)
    ├── index.js        # Express server
    ├── package.json
    └── routes/
        ├── apod.js
        ├── mars-data.js
        ├── mars-photos.js
        ├── rover-manifest.js
        └── weather.js
```
