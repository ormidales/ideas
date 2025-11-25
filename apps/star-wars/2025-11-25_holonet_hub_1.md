# HoloNet Hub

## Concept

HoloNet Hub is the ultimate interactive Star Wars lore repository, designed to immerse fans in the rich galaxy far, far away. This web tool allows users to deep-dive into characters, planets, vehicles, species, films, and technologies across canonical Star Wars content. It offers an interconnected web of information, enabling users to explore relationships between entities, visualize key events on a timeline, and discover fascinating trivia. Whether you're a new Padawan or a seasoned Jedi Master, HoloNet Hub provides a comprehensive, visually appealing, and user-friendly guide to expand your knowledge and navigate the vast Star Wars universe with ease.

## Technical prompt

```md
Build a React web application named 'HoloNet Hub' using Vite.js for development, TypeScript for type safety, and Tailwind CSS for styling. The application's primary goal is to provide an interactive and comprehensive Star Wars lore database.

**Core Technologies:**
*   React (with Vite.js for project setup)
*   TypeScript
*   Tailwind CSS
*   Lucide-React for icons
*   React Router DOM for navigation
*   SWAPI (swapi.dev) as the primary data source (assume local augmentation for richer details or relationships not directly in SWAPI where needed, but prioritize SWAPI).

**Key Features & Functionality:**
1.  **Homepage/Dashboard:**
    *   A welcoming banner and brief description.
    *   Quick links to main sections (Characters, Planets, Films, etc.).
    *   A 'Featured' or 'Trending' section displaying a few randomly selected or popular items (e.g., a character, a planet, a film).
2.  **Universal Search Bar:**
    *   Prominently placed in the navigation bar or homepage.
    *   Allows users to search across all data types (characters, planets, films, vehicles, species).
    *   Implement basic client-side filtering/suggestion as the user types (after initial data fetch).
3.  **Dedicated Content Sections (Main Navigational Routes):**
    *   **Characters:**
        *   **List View:** Displays characters as responsive cards (name, species, homeworld).
        *   **Detail View:** When a card is clicked, navigate to a detailed page showing: full bio (description), species, homeworld (clickable link to planet page), film appearances (clickable links to film pages), vehicles piloted (clickable links), starships owned (clickable links), and associated relationships/factions.
    *   **Planets:**
        *   **List View:** Displays planets as cards (name, climate, terrain, population).
        *   **Detail View:** Shows: full description, climate, terrain, population, residents (clickable links to character pages), film appearances (clickable links).
    *   **Films:**
        *   **List View:** Displays films as cards (title, episode number, release date, director).
        *   **Detail View:** Shows: opening crawl, release date, director, producer, characters (clickable links), planets (clickable links), starships (clickable links), vehicles (clickable links), species (clickable links).
    *   **Vehicles & Starships:**
        *   **List View:** Displays vehicles/starships as cards (name, model, manufacturer).
        *   **Detail View:** Shows: full specs (model, manufacturer, cost, crew, passengers, cargo capacity, atmospheric speed, hyperdrive rating), pilots (clickable links), film appearances (clickable links).
    *   **Species:**
        *   **List View:** Displays species as cards (name, classification, homeworld).
        *   **Detail View:** Shows: average height, average lifespan, language, homeworld (clickable link), associated characters (clickable links), film appearances (clickable links).
4.  **Interactive Timelines (for Films):**
    *   A dedicated section or a component on the homepage displaying films in chronological order of their release date.
    *   Use `recharts` if a simple horizontal bar chart/timeline visualization is desired, otherwise, a simple styled list is sufficient.
5.  **Cross-Referencing & Navigation:**
    *   All related entities within detail views (e.g., a character's homeworld, a film's appearing characters) must be clickable links, leading to the respective detail pages.
6.  **Responsive Design:**
    *   The entire application must be fully responsive and optimized for desktop, tablet, and mobile viewing.
7.  **Loading States & Error Handling:**
    *   Implement visual loading indicators (spinners) for data fetching.
    *   Display user-friendly error messages for API failures or data not found.

**Component Architecture & Styling Guidelines:**
*   **Layout:** Create a `Layout` component that includes a persistent `Navbar` and `Footer`.
*   **Navbar:** Contains the app logo/name, main navigation links (Characters, Planets, Films, Vehicles, Species), and the universal search bar.
*   **Footer:** Basic copyright information, 
```