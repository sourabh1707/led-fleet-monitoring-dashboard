# LED Fleet Monitoring Dashboard

**Node-RED · NovaCloud / VNNox · MQTT · HTML / JavaScript**

A remote LED display monitoring project that separates the onsite LED-controller environment from the monitoring interface. Display/player information is obtained through NovaCloud/VNNox, processed as JSON, transferred through an MQTT data layer, and consumed by a web-based monitoring dashboard.

## Project Overview

The project is designed around a distributed monitoring architecture:

```text
LED Display Controllers / Onsite Infrastructure
                    │
                    ▼
             NovaCloud / VNNox
                    │
                    ▼
                JSON Data
                    │
                    ▼
                MQTT Layer
                    │
          ┌─────────┴─────────┐
          │                   │
          ▼                   ▼
   Node-RED Processing   Monitoring Dashboard
                              │
                              ▼
                       Client / Remote Location
```

The dashboard does not need to be physically located at the LED display site. It can be deployed at an authorized client, monitoring, or support location that has access to the relevant data source.

## What the Project Demonstrates

- NovaCloud/VNNox API integration
- API authentication and request signing using SHA-256
- JSON data processing in Node-RED
- LED player/display information normalization
- MQTT JSON payload processing
- Cached player data and operational statistics
- HTTP API exposure from Node-RED
- Standalone HTML/JavaScript monitoring interface
- Fleet-level online/offline monitoring
- Search, filtering and sorting
- Grid, table and matrix monitoring views
- Hardware-model and resolution analytics
- CSV and JSON data export
- Automatic dashboard synchronization

## Data Flow

The core data flow is:

```text
NovaCloud / VNNox
       │
       ▼
   Node-RED
       │
       ├── Player data normalization
       ├── Statistics
       ├── Data caching
       └── MQTT JSON processing
       │
       ▼
   Monitoring Data
       │
       ▼
 /api/players
       │
       ▼
 HTML Dashboard
```

## Dashboard

The embedded dashboard provides an operations-oriented view of the LED/player fleet.

### Main capabilities

- Total display/player count
- Online and offline counts and percentages
- Dominant controller model
- Resolution profiles
- Fleet analytics charts
- Search across player data
- Status filtering
- Model filtering
- Resolution filtering
- Sorting by status, name, last seen and resolution
- Grid view
- Data table view
- Compact matrix/topology view
- CSV export
- JSON export
- Manual synchronization
- Automatic synchronization

## Node-RED Flow

The Node-RED flow contains the integration and processing logic as well as the HTML dashboard template.

The flow includes API authentication, player-list retrieval, player-data transformation, caching, statistics processing, MQTT JSON handling, and the `/api/players` HTTP endpoint used by the dashboard.

The original Node-RED export is intentionally retained as the project source. The repository presentation does not require the flow to be converted into a conventional web application.

## Deployment Concept

A key design characteristic is the separation between the onsite infrastructure and the monitoring UI.

```text
                    ONSITE / FIELD
              ┌─────────────────────┐
              │ LED Controllers     │
              │ Display Players     │
              └──────────┬──────────┘
                         │
                         ▼
                  NovaCloud/VNNox
                         │
                         ▼
                    JSON / Data
                         │
                         ▼
                    MQTT Layer
                         │
              ┌──────────┼──────────┐
              │          │          │
              ▼          ▼          ▼
          Client UI   Support UI   Monitoring UI
```

This makes the dashboard reusable as a remote monitoring interface rather than tying it to a particular onsite machine.

## Technology Stack

| Layer | Technology |
|---|---|
| Integration / automation | Node-RED |
| Cloud platform | NovaCloud / VNNox |
| API | REST / JSON |
| Messaging / data layer | MQTT |
| Backend endpoint | Node-RED HTTP endpoint |
| Frontend | HTML / CSS / JavaScript |
| UI framework | Tailwind CSS CDN |
| Charts | Chart.js |
| Icons | Lucide |

## Project Structure

```text
led-fleet-monitoring-dashboard/
│
├── README.md
├── docs/
│   └── architecture.md
└── node-red/
    └── VMSHIRE-Dashboard.json
```

## Running the Project

The primary project implementation is a Node-RED flow. Import the Node-RED JSON flow into a Node-RED installation and provide the required environment, API access and data-layer configuration for the intended deployment.

The HTML dashboard is part of the Node-RED implementation and communicates with the Node-RED `/api/players` endpoint for dashboard data.

## Important Note

This repository presents an integration and monitoring system rather than a static GitHub Pages website. GitHub is used to document and distribute the project source and architecture; the production dashboard depends on its Node-RED/data environment.

## Project Focus

This project is intended as a practical example of combining LED display monitoring, cloud APIs, Node-RED automation, MQTT data distribution, JSON processing and a browser-based operational interface into one remotely accessible monitoring workflow.
