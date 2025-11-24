# TerraSculpt

## Concept

TerraSculpt is an innovative web tool designed for moss terrarium enthusiasts and professional designers. It provides a virtual sandbox where users can plan, design, and visualize their terrarium creations before committing to physical materials. With a vast, categorize library of moss types, substrates, hardscape elements (rocks, wood), and decorative items, users can intuitively drag-and-drop components onto a customizable terrarium base. The tool offers intelligent suggestions for element compatibility, optimal placement, and basic care requirements, ensuring healthy and beautiful designs. Beyond basic design, TerraSculpt generates a detailed shopping list for all chosen materials and allows users to export high-quality images of their finished designs, making it the ultimate planning companion for anyone passionate about crafting their miniature green worlds.

## Technical prompt

```md
Build a React.js single-page application named 'TerraSculpt' using Vite for setup and Tailwind CSS for styling. Utilize `lucide-react` for icons. The application will serve as a virtual moss terrarium designer.

**1. Project Setup:**
   - Initialize a new React project with Vite: `npm create vite@latest terraculpt -- --template react-ts`
   - Install Tailwind CSS: Follow the official Tailwind CSS React setup guide.
   - Install `lucide-react`: `npm install lucide-react`
   - Install `html2canvas`: `npm install html2canvas` (for image export).
   - Clean up default Vite boilerplate files.

**2. Core Layout (App.tsx & Layout Components):**
   - Create a responsive layout consisting of:
     - A fixed `Header` component with the app name 'TerraSculpt', a 'New Design' button, 'Save Design' button (initially saves to local storage), 'Export Image' button, and 'Generate Material List' button.
     - A main content area divided into three vertical sections:
       - Left: `AssetPanel` (a sidebar for draggable terrarium elements).
       - Center: `DesignCanvas` (the main interactive terrarium design area).
       - Right: `PropertiesPanel` (a sidebar to display and edit properties of selected elements).
   - Use Tailwind CSS for all styling, ensuring a clean, modern, and intuitive UI.

**3. Asset Library (Data Structure):**
   - Create a TypeScript file (e.g., `src/assetsData.ts`) to mock a library of terrarium elements. This will serve as the initial data source.
   - Each element object should include:
     - `id`: Unique identifier (string).
     - `name`: Display name (e.g., 'Cushion Moss', 'Dragon Stone').
     - `category`: (e.g., 'Moss', 'Substrate', 'Hardscape', 'Decor').
     - `imageSrc`: URL to a simple icon or placeholder image for the asset. These images should be placed in the `public/` directory.
     - `description`: A short description.
     - `compatibilityTags`: An array of strings (e.g., ['highHumidity', 'lowLight', 'acidicSoil']) for basic compatibility checks.
     - `careInfo`: A string with basic care instructions.
     - `defaultWidth`, `defaultHeight`: Numbers representing the initial pixel dimensions for display on the canvas.

**Initial Mock Assets for `src/assetsData.ts`:**
```typescript
export const assets = [
  { id: 'm1', name: 'Cushion Moss', category: 'Moss', imageSrc: '/moss-cushion.png', description: 'A lush, green, domed moss, perfect for adding texture.', compatibilityTags: ['highHumidity', 'lowLight'], careInfo: 'Requires consistent moisture and indirect light. Do not let dry out.', defaultWidth: 80, defaultHeight: 80 },
  { id: 'm2', name: 'Sheet Moss', category: 'Moss', imageSrc: '/moss-sheet.png', description: 'Flat, spreading moss, great for ground cover.', compatibilityTags: ['mediumHumidity', 'lowLight'], careInfo: 'Tolerates drier periods but prefers consistent humidity. Mist regularly.', defaultWidth: 120, defaultHeight: 60 },
  { id: 'h1', name: 'Dragon Stone', category: 'Hardscape', imageSrc: '/hardscape-dragon.png', description: 'Unique porous rock with crevices, ideal for intricate layouts.', compatibilityTags: ['versatile'], careInfo: 'Wash thoroughly before use to remove debris.', defaultWidth: 100, defaultHeight: 70 },
  { id: 'h2', name: 'Spider Wood', category: 'Hardscape', imageSrc: '/hardscape-spider.png', description: 'Branching driftwood, perfect for creating dynamic scenes.', compatibilityTags: ['versatile'], careInfo: 'Soak before use to prevent buoyancy and tannin leeching.', defaultWidth: 150, defaultHeight: 100 },
  { id: 's1', name: 'Sphagnum Moss Substrate', category: 'Substrate', imageSrc: '/substrate-sphagnum.png', description: 'Excellent moisture retention for humid environments.', compatibilityTags: ['highHumidity'], careInfo: 'Provides good aeration and moisture. Forms a base layer.', defaultWidth: 200, defaultHeight: 100 },
  { id: 's2', name: 'Volcanic Soil', category: 'Substrate', imageSrc: '/substrate-volcanic.png', description: 'Porous soil, good for drainage and root aeration.', compatibilityTags: ['mediumHumidity'], careInfo: 'Provides essential minerals and good drainage. Use as an active layer.', defaultWidth: 200, defaultHeight: 100 },
  { id: 'd1', name: 'Miniature Mushroom', category: 'Decor', imageSrc: '/decor-mushroom.png', description: 'Cute decorative mushroom figurine, adds a touch of whimsy.', compatibilityTags: ['none'], careInfo: 'No special care required. Simply place and enjoy.', defaultWidth: 30, defaultHeight: 30 },
];
```

**4. AssetPanel Component (src/components/AssetPanel.tsx):**
   - Display assets grouped by 'Moss', 'Substrate', 'Hardscape', 'Decor' in collapsable sections.
   - Each asset should be a visually distinct, draggable item (e.g., a card with its image and name).
   - Implement a simple search bar at the top to filter assets by name or description.
   - Use `lucide-react` icons for categories (e.g., `Leaf`, `Mountain`, `Droplet`) and the search bar (`Search`).
   - When an asset is dragged, trigger a function in the `DesignCanvas` to add it upon drop. The drag event should carry the `asset.id` and its `defaultWidth`/`defaultHeight`.

**5. DesignCanvas Component (src/components/DesignCanvas.tsx):**
   - This will be the main interactive area. It should be a `div` element with a defined size (e.g., `w-[800px] h-[600px]`) and a subtle border/background to represent the terrarium container.
   - Maintain an array of `canvasElements` in its state, where each element object contains:
     - `id`: Unique ID for this *instance* on the canvas (e.g., `uuidv4()`).
     - `assetId`: The ID from `assetsData.ts`.
     - `x`, `y`: Position on the canvas (pixels).
     - `width`, `height`: Current dimensions (pixels).
     - `rotation`: Rotation angle (degrees).
     - `zIndex`: Layering order.
   - Implement drag-and-drop functionality for assets *from* `AssetPanel` *to* `DesignCanvas`.
   - Render each `canvasElement` as an absolutely positioned `div` containing its `imageSrc`.
   - **Element Interaction:**
     - When an element on the canvas is clicked, it becomes 'selected'. Add a visual indicator (e.g., a border) and update a `selectedElementId` state.
     - Selected elements should be draggable to new `x`, `y` positions on the canvas.
     - Implement basic resizing handles (e.g., on corners) for width and height adjustment.
     - Implement a rotation handle (e.g., a small circle above the element) for rotation.
     - Update the `canvasElements` state with new position, size, and rotation values.
   - Ensure `zIndex` is correctly applied to visual layering. New elements should typically start with a higher `zIndex`.
   - The canvas should have a ref (e.g., `useRef`) for `html2canvas` to target for export.

**6. PropertiesPanel Component (src/components/PropertiesPanel.tsx):**
   - This sidebar dynamically displays information based on the `selectedElementId` from `DesignCanvas`.
   - If no element is selected, display global canvas settings:
     - 'Terrarium Base Shape' (Radio buttons: Rectangle, Circle - visual change for the canvas background/border).
     - 'Base Size' (Dropdown: Small, Medium, Large - changes canvas `width`/`height` accordingly).
   - If an element is selected, display:
     - Read-only fields: Element Name, Category, Description from `assetsData.ts`.
     - Editable fields (using `input type="range"` or `number`):
       - `Width` and `Height` sliders/inputs (linked to element's scale).
       - `Rotation` slider/input (0-360 degrees).
       - `Z-index` input with up/down buttons.
     - Display `Compatibility Tags` and `Care Info` clearly.
     - A 'Delete Element' button (uses `lucide-react` `Trash2` icon) to remove the selected element from the canvas.

**7. Toolbar Functionality (Header Component):**
   - **New Design:** Clears all elements from `DesignCanvas` and resets canvas settings to default.
   - **Save Design:** Serializes the current `canvasElements` array and canvas settings (shape, size) to `localStorage` as a JSON string. Display a confirmation toast.
   - **Load Design (Implicit from Save):** On app load, check `localStorage` for a saved design and load it if found.
   - **Export Image:** On click, use `html2canvas` to capture the `DesignCanvas` element. The resulting image should be offered for download (e.g., as 'terrasculpt-design.png'). Ensure the canvas background is included in the export.
   - **Generate Material List:** Open a modal dialog (`MaterialListModal.tsx`).
     - In the modal, group and list all *unique* `asset.name`s currently present on the `DesignCanvas`.
     - For each unique asset, display its name, a count of its instances on the canvas, and its `careInfo`. (e.g., 'Cushion Moss (x3): Requires consistent moisture...').
     - Include a 'Close' button in the modal.

**8. Basic Compatibility Checker:**
   - When an element is added to or selected on the `DesignCanvas`, implement a simple check:
     - For the selected element, compare its `compatibilityTags` against other existing elements or a global canvas type (e.g., if a 'desert' terrarium base is chosen, flag 'highHumidity' moss).
     - Display a subtle warning or suggestion message in the `PropertiesPanel` if a potential conflict is detected (e.g., 'Warning: This moss prefers high humidity, which might conflict with existing low-humidity plants/substrate.'). This can be a simple hardcoded rule set or a lookup against predefined conflict pairs within your data.

**9. Styling and Responsiveness:**
   - Apply Tailwind CSS extensively for all components.
   - Ensure the main layout is responsive, allowing panels to adjust or collapse on smaller screens (though a desktop-first approach is acceptable for the main design canvas).
   - Provide clear visual feedback for interactive elements: hover states, active states, selected elements.
   - Use `lucide-react` for all appropriate icons (e.g., `Plus`, `Save`, `Download`, `List`, `Search`, `Trash2`, `RotateCw`, `Scale`, `Layers`, `Settings`).

**10. State Management:**
    - Use React's `useState` and `useReducer` hooks for managing local component state.
    - For global state like `canvasElements` and `selectedElementId`, consider using React's Context API to easily pass state and dispatch updates between `Header`, `DesignCanvas`, and `PropertiesPanel`.
```