# Staff Travel Route Mapper

An interactive route mapping tool for staff travel (ID90 / ZED) showing routes available across your permitted airline network, filtered by travel class.

## Project Structure

```
/
├── index.html                        # The application — everything runs from here
└── data/
    ├── permitted_airlines.json       # YOUR data — edit this to match your entitlements
    └── permitted_airlines.schema.json  # JSON schema for reference/validation
```

## Data Sources (fetched live, no setup needed)

| Source | Data | URL |
|--------|------|-----|
| OurAirports | Airport names, IATA codes, coordinates | `davidmegginson.github.io/ourairports-data/airports.csv` |
| Jonty/airline-route-data | Airline routes (updated weekly) | `raw.githubusercontent.com/Jonty/airline-route-data/main/airline_routes.json` |

## Setup for GitHub Pages

1. **Fork or clone** this repository
2. **Edit `data/permitted_airlines.json`** with your actual airline entitlements (see schema below)
3. In your GitHub repo → **Settings → Pages → Source: Deploy from branch → main / root**
4. Your app will be live at `https://YOUR-USERNAME.github.io/REPO-NAME/`

> No build step. No npm install. No API keys. It's a single HTML file.

## Editing `permitted_airlines.json`

### Required fields per airline
| Field | Type | Description |
|-------|------|-------------|
| `iata_code` | string | 2-char IATA code e.g. `"QF"` |
| `airline_name` | string | Full name e.g. `"Qantas"` |
| `permitted_classes` | array | One or more of `"F"`, `"J"`, `"W"`, `"Y"` |

### Optional fields
| Field | Type | Description |
|-------|------|-------------|
| `country` | string | Country of operation |
| `alliance` | string | `"oneworld"`, `"Star Alliance"`, `"SkyTeam"`, `"none"` |
| `staff_fare_type` | string | `"ID90"`, `"ID75"`, `"ID50"`, `"ZED"`, `"myIDTravel"`, `"Other"` |
| `listing_required` | boolean | Whether listing is required before travel |
| `booking_platform` | string | e.g. `"myIDTravel"`, `"Sabre"`, `"direct"` |
| `notes` | string | Free text — any conditions or caveats |

### Class codes
| Code | Cabin |
|------|-------|
| `F` | First Class |
| `J` | Business Class |
| `W` | Premium Economy |
| `Y` | Economy |

### Example entry
```json
{
  "iata_code": "EK",
  "airline_name": "Emirates",
  "country": "United Arab Emirates",
  "alliance": "none",
  "permitted_classes": ["J", "Y"],
  "staff_fare_type": "ID90",
  "listing_required": true,
  "booking_platform": "myIDTravel",
  "notes": "First class not available on ID90."
}
```

## Using the App

- **Airport tab** — search by airport name, city, or IATA code. Click an airport to see all routes served by your permitted airlines. Use the class filter pills to narrow to specific cabin types.
- **Airline tab** — browse your permitted airlines. Click an airline to see its full route network drawn on the map.
- **Info panel** (bottom of sidebar) — shows route count and airport count for your selection.
- **Clear selection** button (bottom right of map) — resets the view.

## Local Development

Just open `index.html` in a browser — but note that fetching local files (`data/permitted_airlines.json`) may be blocked by browser security. To develop locally, run a simple server:

```bash
# Python
python3 -m http.server 8080

# Node
npx serve .
```

Then open `http://localhost:8080`.

## Updating Route Data

Route data is fetched live from `Jonty/airline-route-data` on every page load — it updates weekly automatically. No action needed on your part.

## Attribution

- Route data: [Jonty/airline-route-data](https://github.com/Jonty/airline-route-data)
- Airport data: [OurAirports](https://ourairports.com/data/) (Public Domain)
- Map tiles: [Stadia Maps](https://stadiamaps.com/) + [OpenStreetMap](https://openstreetmap.org)
- Map library: [Leaflet](https://leafletjs.com/)
