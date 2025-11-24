# StrukturScan

StrukturScan is a unique web tool designed for enthusiasts, architects, and students fascinated by Soviet Brutalist architecture. It empowers users to upload images of buildings for analysis, providing a 'Brutalist Score' and identifying characteristic features such as monolithic concrete forms, repetitive modular elements, and exposed functional components. Beyond analysis, the platform features a curated, searchable database of iconic Soviet Brutalist structures, complete with detailed information, historical context, and geographical locations. StrukturScan aims to demystify and foster a deeper appreciation for this often-misunderstood architectural style, serving as both an analytical utility and a comprehensive educational resource.

## Technical prompt

```md
Build a modern React web application named 'StrukturScan' using Vite for project setup and Tailwind CSS for all styling. The application should be a single-page application (SPA) with routing handled by `react-router-dom`. All icons should be sourced from `lucide-react`.

**I. Project Setup:**
1.  Initialize a new React project using Vite.
2.  Configure Tailwind CSS for the project.
3.  Install `react-router-dom`, `lucide-react`, and `react-dropzone`.
4.  For map functionality, install `react-map-gl` (ensure proper setup for Mapbox GL JS token if needed, or suggest using OpenStreetMap tiles for simplicity).

**II. Core Layout Components:**
1.  **Header Component (`components/Header.jsx`):**
    *   Display the app name 'StrukturScan'.
    *   Include navigation links: 'Home', 'Analyze', 'Database', 'About'. Use `NavLink` from `react-router-dom` for active state styling.
    *   Style with Tailwind CSS for a clean, brutalist-inspired look (e.g., strong lines, clear typography, dark/light contrast).
2.  **Footer Component (`components/Footer.jsx`):**
    *   Display copyright information.
    *   Simple, unobtrusive styling with Tailwind CSS.

**III. Pages & Routing:**
Set up `react-router-dom` in `App.jsx` to route to the following pages:
1.  **Home Page (`pages/HomePage.jsx`):**
    *   A hero section with a compelling headline (e.g., 'Discover the Monolith: Your Guide to Soviet Brutalism').
    *   A brief introduction to the app's purpose.
    *   Call-to-action buttons leading to the 'Analyze' and 'Database' pages.
    *   Responsive design using Tailwind CSS.
2.  **Image Analyzer Page (`pages/AnalyzePage.jsx`):**
    *   **Image Upload Zone (`components/ImageUploadZone.jsx`):**
        *   Implement a drag-and-drop file upload area using `react-dropzone`.
        *   Display a preview of the uploaded image.
        *   Clear button for removing the uploaded image.
    *   **Analysis Display (`components/AnalysisDisplay.jsx`):**
        *   Upon a user clicking an 'Analyze' button (initially, this will trigger a mock analysis).
        *   Display a 'Brutalist Score' (e.g., a percentage from 0-100%).
        *   List identified 'Features' (e.g., 'Monolithic Form', 'Exposed Concrete', 'Repetitive Modules', 'Geometric Shapes').
        *   Include a placeholder message indicating that this functionality would typically integrate with a backend ML model.
        *   Add a 'Share Results' button (functionality can be a simple alert or copy to clipboard).
3.  **Database Page (`pages/DatabasePage.jsx`):**
    *   **Building Data (`data/buildings.json`):** Create a JSON file with at least 5-10 example Soviet Brutalist buildings. Each entry should include: `id`, `name`, `city`, `country`, `year`, `architect` (if known), `description`, `mainImage` (URL), `galleryImages` (array of URLs), `latitude`, `longitude`.
    *   **Search and Filter Bar (`components/SearchBar.jsx`):**
        *   Input field for searching by building name, city, or architect.
        *   Dropdowns or checkboxes for filtering by country or a range of years.
    *   **Building Grid (`components/BuildingGrid.jsx`):**
        *   Display `BuildingCard` components in a responsive grid layout.
    *   **Building Card (`components/BuildingCard.jsx`):**
        *   For each building: display a thumbnail image, name, and location.
        *   Make the entire card clickable, linking to the `BuildingDetailPage` via `react-router-dom`.
4.  **Building Detail Page (`pages/BuildingDetailPage.jsx`):**
    *   Display all information for a selected building (from `buildings.json`).
    *   Large main image and a small gallery/carousel of additional images.
    *   Detailed description and historical context.
    *   Display a map using `react-map-gl` centered on the building's `latitude` and `longitude`, with a marker.
5.  **About Page (`pages/AboutPage.jsx`):**
    *   Provide information about Soviet Brutalist architecture, its history, key characteristics, and notable examples.
    *   Explain the purpose of StrukturScan and its mission.

**IV. Styling and UI/UX:**
*   **Overall Aesthetic:** Embrace a brutalist-inspired design philosophy: strong lines, clear hierarchy, functional typography (e.g., sans-serif), minimal ornamentation, grayscale palette with subtle concrete textures or accent colors (e.g., deep red, dark blue) for calls to action.
*   **Responsiveness:** Ensure the application is fully responsive and looks good on various screen sizes (mobile, tablet, desktop) using Tailwind CSS utilities.
*   **Icons:** Use `lucide-react` for all icons (e.g., upload, search, map marker, info, share).

**V. Data Handling (Initial):**
*   All building data will be read from the local `data/buildings.json` file.
*   Image analysis results will be mocked client-side for the initial build.

**VI. Development Workflow:**
1.  Set up the project with Vite, React, and Tailwind CSS.
2.  Implement `Header` and `Footer` components.
3.  Configure `react-router-dom` and create placeholder page components.
4.  Develop `HomePage`.
5.  Create `buildings.json` with sample data.
6.  Implement `DatabasePage` including `SearchBar`, `BuildingGrid`, and `BuildingCard`.
7.  Develop `BuildingDetailPage` with `react-map-gl` integration.
8.  Implement `ImageAnalyzerPage` with `ImageUploadZone` and `AnalysisDisplay` (mocked analysis).
9.  Develop `AboutPage`.
10. Refine all styling with Tailwind CSS to match the brutalist aesthetic and ensure responsiveness.
11. Integrate `lucide-react` for appropriate icons across the application.
```