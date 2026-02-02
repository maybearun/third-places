# Project: Raw OSM Third Places Tracker

## 1. Architecture Goals

- Use **OpenLayers** (the direct engine for OSM) for maximum control.
- Avoid "wrapper" libraries; interact with the Map API directly via refs.
- Focus on "Free" urban spaces (Third Places).

**Tech Stack:**

- **Framework:** Next.js (App Router)
- **Maps:** OpenLayers (`ol` package)
- **Data:** Supabase (PostgreSQL/PostGIS)
- **Styling:** Tailwind CSS

---

## 2. Technical Context for AI

When generating code, follow these rules:

- Use `ol/Map`, `ol/View`, and `ol/layer/Tile` with `OSM` as the source.
- Manage the map instance inside a `useEffect` or `useLayoutEffect` to prevent memory leaks.
- Use **Vector Layers** for user-contributed markers (Third Places).

---

## 3. Data Schema (PostGIS Optimized)

```sql
CREATE TABLE public.third_places (
  id uuid DEFAULT gen_random_uuid() PRIMARY KEY,
  name text NOT NULL,
  category text, -- e.g., 'plaza', 'library', 'garden'
  geom geography(Point, 4326), -- Spatial data for mapping
  tags text[], -- e.g., ['quiet', 'wifi', 'outdoors']
  created_at timestamptz DEFAULT now()
);
```
