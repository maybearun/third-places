# Project: Free Third Places Map

## 1. Project Overview

An interactive web application to help users discover and tag "Third Places" (libraries, parks, community centers, public plazas) that are free to enter and spend time in.

**Core Tech Stack:**

- **Frontend:** React/Next.js (or Vite)
- **Mapping:** OpenStreetMap (OSM) via Leaflet.js
- **Database/Backend:** Supabase (PostgreSQL + PostGIS for spatial data)
- **Styling:** Tailwind CSS

---

## 2. Feature Requirements

- **Interactive Map:** Display markers for verified free third places.
- **Location Tagging:** Users can click on the map to "Suggest a Place."
- **Filtering:** Filter by type (e.g., Indoor, Outdoor, Quiet, Social).
- **Crowdsourcing:** A simple form to submit a name, description, and "vibe" tags.
- **OSM Integration:** Use Leaflet to render tiles and handle coordinate placement.

---

## 3. Data Schema (PostgreSQL)

The database needs to store spatial coordinates. Use the following structure:

| Column        | Type      | Description                                 |
| :------------ | :-------- | :------------------------------------------ |
| `id`          | UUID      | Primary Key                                 |
| `name`        | String    | Name of the place                           |
| `description` | Text      | Brief description                           |
| `category`    | Enum      | e.g., 'library', 'park', 'community_center' |
| `lat`         | Float     | Latitude                                    |
| `lng`         | Float     | Longitude                                   |
| `is_free`     | Boolean   | Hard constraint for this app                |
| `created_at`  | Timestamp | Date added                                  |

---

## 4. Implementation Instructions for AI

### Phase 1: Basic Map Setup

1. Initialize a React project with Tailwind CSS.
2. Install `react-leaflet` and `leaflet`.
3. Create a `MapContainer` centered on a default city.
4. Set up the OpenStreetMap tile layer.

### Phase 2: Adding Markers

1. Fetch data from the `places` table.
2. Map through the data to render `<Marker>` components.
3. Add a `<Popup>` to each marker showing the place name and "Free" status.

### Phase 3: "Tag a Place" Logic

1. Implement a `useMapEvents` hook to capture clicks on the map.
2. When the map is clicked, open a modal with a form.
3. The form should auto-fill the Latitude/Longitude based on the click.
4. On submit, send a POST request to the database.

---

## 5. UI/UX Style Guide

- **Vibe:** Minimalist, community-focused, and accessible.
- **Colors:** Earthy greens and soft blues to feel "public" and welcoming.
- **Mobile First:** The map must be easily navigable on a smartphone.
