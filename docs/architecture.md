# System Architecture

## Overview

The project separates the LED/display data source from the monitoring interface.

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
              MQTT Data Layer
                    │
                    ▼
             Monitoring Client
                    │
                    ▼
             HTML Dashboard
```

## Separation of Locations

The monitoring HTML does not need to be deployed at the same physical location as the LED controllers.

```text
SITE / FIELD                         REMOTE / CLIENT LOCATION

LED Controllers                      Monitoring Dashboard
       │                                      ▲
       ▼                                      │
NovaCloud / VNNox                           MQTT data
       │                                      │
       └──────────────► MQTT Layer ──────────┘
```

The same monitoring interface can be used from an authorized location that has access to the relevant MQTT data.

## Node-RED Responsibilities

The supplied Node-RED flow provides the integration and processing layer. It includes:

1. NovaCloud/VNNox authentication handling.
2. Player-list API requests.
3. Transformation of API records into a simplified player structure.
4. Player data caching.
5. Player statistics.
6. MQTT JSON payload validation and processing.
7. An HTTP endpoint at `/api/players` for the browser dashboard.
8. The HTML/JavaScript dashboard template.

## Normalized Player Data

The flow converts player records into a compact structure containing fields such as:

```json
{
  "name": "...",
  "model": "...",
  "resolution": "...",
  "onlineStatus": "Online",
  "lastSeen": "..."
}
```

The dashboard then uses this data for monitoring, filtering, sorting and analytics.

## Dashboard Data Path

```text
Node-RED /api/players
          │
          ▼
      fetch() in
      browser UI
          │
          ▼
   Dashboard State
          │
    ┌─────┼─────────────┐
    ▼     ▼             ▼
   KPI  Analytics   Player Views
                     │
              ┌──────┼──────┐
              ▼      ▼      ▼
             Grid   Table  Matrix
```

## Design Principle

The project is intentionally not treated as a static website. The browser interface is one presentation layer of a larger monitoring system whose data originates from LED/display infrastructure and is distributed through the project's data layer.
