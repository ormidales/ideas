# BrickFolio

## Concept

BrickFolio is the ultimate web-based portfolio tracker and analytics tool designed specifically for serious LEGO set investors. It aggregates market data from key sources like BrickLink and Brickset (or similar data providers), allowing users to accurately track the real-time value and performance of their LEGO investment portfolio. Users can add sets they own, log purchase prices and dates, and monitor their return on investment (ROI). The platform provides historical price charts, estimated retirement dates, and valuable insights to help investors make informed decisions on when to buy, hold, or sell, transforming their passion for bricks into a more strategic and profitable financial endeavor.

## Technical prompt

```md
You are tasked with building a web application called 'BrickFolio' for LEGO set investing. This will be a React application using Vite for setup, styled with Tailwind CSS, and using specific libraries for icons and charting.

**Project Setup:**
1.  Initialize a new React project using Vite: `npm create vite@latest brickfolio -- --template react`.
2.  Install necessary dependencies:
    *   Tailwind CSS: Follow the official Tailwind CSS installation guide for Vite (postcss, autoprefixer).
    *   Icons: `npm install lucide-react`.
    *   Charting: `npm install recharts`.
    *   Routing: `npm install react-router-dom`.
3.  Configure `tailwind.config.js` with basic theme extensions (e.g., custom colors if desired, but default Tailwind is fine).

**Core Data Model (Client-side Simulation for V1):**
For initial development, create mock JSON data files in `src/data/`.
*   `mockLegoSets.json`: An array of LEGO set objects.
    *   `id`: string (unique identifier)
    *   `name`: string (e.g., 'Millennium Falcon')
    *   `setNumber`: string (e.g., '75192')
    *   `image`: string (URL to set image)
    *   `theme`: string (e.g., 'Star Wars')
    *   `releaseDate`: string (ISO date format)
    *   `retirementDate`: string | null (estimated, ISO date format)
    *   `MSRP`: number
    *   `currentMarketValue`: {"new": number, "used": number}
    *   `historicalPrices`: array of {"date": string (ISO date), "price": number} (for charts)
*   `portfolio.json` (Initially empty, will be managed by `localStorage`):
    *   `id`: string (unique ID for portfolio item)
    *   `setId`: string (references `LegoSet.id`)
    *   `purchasePrice`: number
    *   `purchaseDate`: string (ISO date format)
    *   `quantity`: number
*   `watchlist.json` (Initially empty, will be managed by `localStorage`):
    *   `id`: string (unique ID for watchlist item)
    *   `setId`: string (references `LegoSet.id`)

**Global State/Data Management:**
*   Create a React Context (`src/context/LegoDataContext.jsx`) to manage the `portfolio` and `watchlist` arrays globally.
*   The context provider (`LegoDataProvider`) should initialize these arrays from `localStorage` on component mount and update `localStorage` whenever they change.
*   Provide functions through the context for `addSetToPortfolio`, `updatePortfolioItem`, `removePortfolioItem`, `addSetToWatchlist`, `removeSetFromWatchlist`.
*   All data fetching (initially from mock data using `setTimeout` to simulate async calls) should be handled within the context or utility functions.

**Main Application Structure (src/App.jsx):**
*   Use `react-router-dom` for routing.
*   Implement a main layout that includes a `Sidebar` and renders different page components based on the route.

**Key Pages/Routes:**
1.  **`/` (Dashboard - `src/pages/Dashboard.jsx`):**
    *   Displays an overview of the user's portfolio.
    *   **Portfolio Summary Card:** Show total portfolio value, total ROI (absolute and percentage), and the number of sets owned. Use Tailwind for styling (e.g., `bg-white p-6 rounded-lg shadow-md`).
    *   **Top Performers Card:** List the top 3 best-performing sets from the user's portfolio (based on ROI).
    *   **Upcoming Retirements Card:** List sets from the portfolio or watchlist with approaching estimated retirement dates.

2.  **`/search` (Set Search - `src/pages/Search.jsx`):**
    *   **Search Bar Component (`src/components/SearchBar.jsx`):** An input field (styled with Tailwind) for entering a LEGO set number or name, and a search button. Use a `lucide-react` search icon.
    *   **Search Results Grid:** Display search results in a responsive grid. Each result should be a `SetCard` component.
        *   `SetCard` (`src/components/SetCard.jsx`): Shows set image, name, number, current market value (new). Includes buttons for "View Details" (links to `/set/:id`), "Add to Portfolio", and "Add to Watchlist" (using `lucide-react` icons).

3.  **`/set/:id` (Set Detail - `src/pages/SetDetail.jsx`):**
    *   Fetches detailed information for the LEGO set specified by the `:id` parameter in the URL (from mock data).
    *   **Set Info Section:** Display large image, set name, set number, theme, MSRP, release date, and estimated retirement date.
    *   **Current Market Value Section:** Show current market values for new and used conditions.
    *   **Price History Chart:** Use `recharts` (`LineChart`, `XAxis`, `YAxis`, `Tooltip`, `ResponsiveContainer`) to display historical price data for the set. X-axis should be dates, Y-axis should be price.
    *   **Actions Section:** Buttons to "Add to Portfolio" (opens a modal/form) and "Add to Watchlist".

4.  **`/portfolio` (My Portfolio - `src/pages/Portfolio.jsx`):**
    *   Displays all LEGO sets the user owns in a sortable table.
    *   Columns: Set Name, Set Number, Quantity, Purchase Price, Purchase Date, Current Value, ROI (absolute and percentage).
    *   Each row should have action buttons: "Edit" (to modify quantity, purchase price/date) and "Remove" (from portfolio). Use `lucide-react` edit and trash icons.
    *   An "Add New Set to Portfolio" button (e.g., in the header of the table) that opens a modal with the `AddPortfolioItemForm`.
    *   **Add Portfolio Item Form (`src/components/AddPortfolioItemForm.jsx`):** A form (can be a modal) with fields for Set Name/Number (could use a simple text input or integrate search), Quantity, Purchase Price, and Purchase Date.

5.  **`/watchlist` (Watchlist - `src/pages/Watchlist.jsx`):**
    *   Displays sets the user is tracking in a table similar to the portfolio.
    *   Columns: Set Name, Set Number, Current Market Value (new), Estimated Retirement Date.
    *   Each row should have action buttons: "Move to Portfolio" (opens the `AddPortfolioItemForm` pre-filled with set details) and "Remove from Watchlist". Use `lucide-react` icons.

**Components Breakdown & Styling:**
*   **Sidebar (`src/components/Sidebar.jsx`):**
    *   Fixed-position navigation on the left side, full height.
    *   Links to Dashboard, Search, Portfolio, Watchlist. Each link should use an appropriate `lucide-react` icon (e.g., `Home`, `Search`, `Briefcase`, `List`).
    *   Apply Tailwind for styling (e.g., `bg-gray-800 text-white w-64 h-screen fixed`).
*   **Header (`src/components/Header.jsx`):**
    *   A simple top bar displaying the app name "BrickFolio".
    *   Tailwind styling (e.g., `bg-white shadow-sm p-4`).
*   **Button (`src/components/Button.jsx`):** A reusable button component with primary, secondary, and destructive variants using Tailwind CSS classes.
*   **Input (`src/components/Input.jsx`):** A reusable input component with basic styling.
*   **Modal (`src/components/Modal.jsx`):** A generic modal component for forms like "Add to Portfolio" or "Edit Portfolio Item".
*   **Card (`src/components/Card.jsx`):** A generic card component for displaying information sections.

**Styling Guidelines:**
*   Use Tailwind CSS for all styling. Prioritize utility classes over custom CSS files.
*   Ensure responsive design for all major components (e.g., using `md:`, `lg:` prefixes).
*   Maintain a consistent visual hierarchy and color palette (e.g., shades of gray, a prominent accent color like LEGO red).
*   Use `lucide-react` for all relevant icons throughout the application.

**Development Steps for AI Engineer:**
1.  **Project Initialization & Dependencies**: Set up the React project with Vite, install Tailwind CSS, `lucide-react`, `recharts`, and `react-router-dom`. Configure Tailwind.
2.  **Mock Data Creation**: Create `src/data/mockLegoSets.json` with at least 10 realistic LEGO set entries, including `historicalPrices` data.
3.  **Context and Global State**: Implement `LegoDataContext` to manage and persist portfolio and watchlist data in `localStorage`.
4.  **Layout Components**: Build `Sidebar` and `Header` components, integrate them into `App.jsx` with `react-router-dom` for navigation.
5.  **Search Feature Development**: Create `SearchBar` and `SetCard`. Implement the `/search` page to display results from `mockLegoSets.json`.
6.  **Set Detail Page**: Develop the `/set/:id` page, including `recharts` `LineChart` for historical prices. Ensure "Add to Portfolio" and "Add to Watchlist" buttons correctly interact with the global state via forms/modals.
7.  **Portfolio Page**: Build the `/portfolio` page with the sortable table. Implement `AddPortfolioItemForm` and integrate edit/remove functionalities with the global state.
8.  **Watchlist Page**: Develop the `/watchlist` page with its table and associated actions.
9.  **Dashboard Page**: Implement the `/` Dashboard page, dynamically displaying summaries and top performers based on the global portfolio state.
10. **Refinement**: Review and ensure all components are styled consistently with Tailwind, icons are correctly implemented, and the application is responsive and user-friendly. Add basic error handling and loading states where appropriate (e.g., for mock data fetching).
```