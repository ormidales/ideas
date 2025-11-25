# Hyperspace Navigator

## Concept

Hyperspace Navigator is an interactive web tool designed for Star Wars enthusiasts who dream of exploring the galaxy far, far away. Users can visualize, plan, and simulate journeys between iconic Star Wars planets, understanding hyperlane routes, estimated travel times, and potential encounters. It leverages a comprehensive, fan-sourced database of canonical planets, hyperlanes, and key galactic regions to offer a rich, immersive planning experience, making it useful for role-playing game campaigns, fan fiction writers, or simply satisfying curiosity about galactic logistics within the Star Wars universe.

## Technical prompt

```md
Build a React web application named 'Hyperspace Navigator'. The application should utilize Tailwind CSS for styling and `lucide-react` for icons. The core functionality revolves around an interactive galaxy map and route planning within the Star Wars universe.

**Project Setup:**
1.  Initialize a new React project using Vite.
2.  Install and configure Tailwind CSS.
3.  Install `lucide-react` for all icons.
4.  Optionally, install `react-svg-pan-zoom` or similar for robust map interaction if custom SVG manipulation proves too complex initially.

**Data Structure & Integration:**
1.  Create a `data` directory at the project root.
2.  Within `data`, create `planets.json` and `hyperlanes.json`.
    *   `planets.json`: An array of objects, each representing a planet with properties like `id` (unique string), `name` (string), `coordinatesX` (number, for map position), `coordinatesY` (number, for map position), `climate` (string), `terrain` (string), `population` (string), `majorFactions` (array of strings), `firstAppearance` (string, e.g., 'Episode IV').
    *   `hyperlanes.json`: An array of objects, each representing a hyperlane with properties like `id` (unique string), `startPlanetId` (string, matching `planet.id`), `endPlanetId` (string, matching `planet.id`), `lengthUnits` (number, representing hypothetical travel time/distance), `safetyRating` (string, e.g., 'Safe', 'Dangerous', 'Pirate Infested').
3.  Implement data loading logic to import these JSON files into the application state upon startup.

**Core Components Development:**

1.  **`Header.jsx`**:
    *   Display the app name 'Hyperspace Navigator'.
    *   Include a theme toggle (light/dark mode) using Tailwind CSS classes and `useState` for theme management.

2.  **`GalaxyMap.jsx`**:
    *   Render an SVG element as the main interactive map canvas.
    *   Plot planets as clickable circles or simple icons at their respective `coordinatesX` and `coordinatesY`.
    *   Render hyperlanes as lines connecting planets based on `startPlanetId` and `endPlanetId`.
    *   Implement pan and zoom functionality for the SVG (can use `react-svg-pan-zoom` or manual SVG `transform` manipulation).
    *   Highlight selected planets and active route segments (calculated later).
    *   On planet click, set the globally selected planet.

3.  **`PlanetSearch.jsx`**:
    *   A reusable component with an input field for searching planet names.
    *   Implement an autocomplete/suggest dropdown feature as the user types.
    *   Use a `lucide-react` search icon inside the input.
    *   When a planet is selected from the suggestions, emit its `id` to the parent component.

4.  **`PlanetDetailsCard.jsx`**:
    *   Display comprehensive information about a currently selected planet.
    *   Include its name, climate, terrain, population, major factions, and first appearance.
    *   Style as an overlay or sidebar card using Tailwind CSS.

5.  **`RoutePlannerForm.jsx`**:
    *   Contains two instances of `PlanetSearch` for 'Origin Planet' and 'Destination Planet'.
    *   A 'Calculate Route' button. `lucide-react` icon for calculation/route.
    *   On button click, trigger the route calculation logic using the selected origin and destination planet IDs.

6.  **`RouteDisplay.jsx`**:
    *   Display the calculated route as an ordered list of intermediate planets.
    *   Show the estimated total travel time (sum of `lengthUnits` for hyperlanes in the route).
    *   Provide visual feedback on the `GalaxyMap` by highlighting the entire route path.

7.  **`JourneyNarrativePanel.jsx`**:
    *   Generate and display a short, descriptive narrative of the calculated journey.
    *   This narrative should incorporate details like the `safetyRating` of hyperlanes and mention major factions from planets along the route. It can be a simple templated string or a randomized selection of sentences based on route characteristics.

**State Management:**
*   Utilize React's `useState` and `useContext` (or a simple global state object) to manage application-wide state, including:
    *   The currently selected planet for `PlanetDetailsCard`.
    *   The origin and destination planet IDs for `RoutePlannerForm`.
    *   The calculated route (an array of hyperlane and planet IDs).
    *   The map's pan and zoom state.
    *   The current theme (light/dark).

**Route Calculation Logic:**
*   Implement a shortest path algorithm (e.g., Dijkstra's algorithm) to find the most efficient hyperlane route between two planets.
*   The 'weight' for pathfinding should primarily be `lengthUnits` from `hyperlanes.json`.
*   This logic should reside in a dedicated utility file or a custom hook.

**Styling & Responsiveness:**
*   Apply Tailwind CSS consistently across all components to achieve a sleek, functional Star Wars-themed UI.
*   Ensure the application layout is fully responsive and user-friendly on various screen sizes (mobile, tablet, desktop).

**Initial Data Placeholder (Example for `planets.json` and `hyperlanes.json`):**
// planets.json example
[
  {
    "id": "coruscant",
    "name": "Coruscant",
    "coordinatesX": 500,
    "coordinatesY": 300,
    "climate": "Urban, Temperate",
    "terrain": "Cityscape",
    "population": "Trillions",
    "majorFactions": ["Galactic Republic", "Galactic Empire", "New Republic"],
    "firstAppearance": "Return of the Jedi (Special Edition)"
  },
  {
    "id": "tatooine",
    "name": "Tatooine",
    "coordinatesX": 100,
    "coordinatesY": 700,
    "climate": "Arid",
    "terrain": "Desert",
    "population": "Sparse",
    "majorFactions": ["Hutts", "Galactic Empire"],
    "firstAppearance": "A New Hope"
  }
]

// hyperlanes.json example
[
  {
    "id": "coruscant-tatooine-1",
    "startPlanetId": "coruscant",
    "endPlanetId": "tatooine",
    "lengthUnits": 100,
    "safetyRating": "Pirate Infested"
  }
]

**Final Deliverable:** A functional React application demonstrating all specified features, with a clean codebase and responsive design.
```