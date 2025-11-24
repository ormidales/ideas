# PairPerfect

PairPerfect is an advanced web tool designed to help designers achieve flawless font pairings and precise typographic metrics for any project. It moves beyond simple font previews by offering a sophisticated, real-time environment to adjust critical typographic elements like kerning, tracking, leading, and baseline shifts across multiple chosen fonts. The tool features an AI-powered suggestion engine that recommends harmonious font combinations based on specified project mood and target audience, ensuring aesthetic appeal and readability. Designers can visualize and test legibility across various screen sizes and dark/light modes, saving countless hours of manual adjustments and guaranteeing professional-grade, impactful typography.

## Technical prompt

```md
Develop a React web application using Vite for quick setup and Tailwind CSS for styling, named 'PairPerfect'.

**Core Libraries & Setup:**
*   Initialize a new React project with Vite.
*   Integrate Tailwind CSS for utility-first styling.
*   Install `lucide-react` for icons.
*   Utilize `react-colorful` for potential color picking features (e.g., text/background color).
*   Implement `webfontloader` or similar dynamic loading for Google Fonts.

**Application Structure & Components:**

1.  **`AppLayout.jsx`**: The main container component, setting up the basic layout (e.g., a header, a main content area divided into a control panel and a preview panel).

2.  **`Header.jsx`**: Top navigation bar.
    *   Displays the 'PairPerfect' logo/title.
    *   Includes an icon button for 'Save Project' (stores settings to local storage).
    *   Includes an icon button for 'Load Project' (loads settings from local storage).
    *   Includes an icon button for 'Export CSS' (copies current font/metric settings as CSS to clipboard).

3.  **`ControlPanel.jsx`**: A sidebar or left-hand panel containing all font selection and typographic adjustment controls.
    *   **`FontPairingSection.jsx`**: Contains two instances of `FontSelectionCard` for 'Heading' and 'Body' text types.
    *   **`TypographicControlsSection.jsx`**: Organizes various sliders and inputs for fine-tuning typography.
        *   **`SliderGroup.jsx` (reusable component)**: Takes a `label`, `min`, `max`, `step`, `value`, and `onChange` prop. Displays a label, a slider, and a numeric input field. Used for:
            *   Font Size (px, `min:10`, `max:120`, `step:1`)
            *   Line Height (unitless, `min:0.8`, `max:3`, `step:0.05`)
            *   Letter Spacing (em, `min:-0.1`, `max:0.2`, `step:0.005`)
            *   Word Spacing (em, `min:0`, `max:0.5`, `step:0.01`)
            *   Baseline Shift (px, `min:-20`, `max:20`, `step:1`)
            *   Kerning (checkbox/toggle for 'Optical Kerning' vs. 'Metric Kerning', potentially a manual kerning input for specific character pairs as a stretch goal).
        *   **Color Pickers**: Using `react-colorful`, allow selection of text color and background color for the preview.

4.  **`FontSelectionCard.jsx`**: Displays the currently selected font for either 'Heading' or 'Body'.
    *   Shows font name and a small preview of the alphabet.
    *   **`FontSelector.jsx`**: A searchable dropdown/modal.
        *   Lists popular Google Fonts (fetch dynamically via Google Fonts API).
        *   Includes an 'Upload Custom Font' button: Allows users to upload `.ttf`, `.otf`, `.woff`, `.woff2` files. These fonts should be dynamically loaded and applied to the preview.

5.  **`AIPairingButton.jsx`**: A button within the `ControlPanel` that, when clicked, opens the `AIPairingModal`.

6.  **`AIPairingModal.jsx`**: A modal component.
    *   Contains input fields (e.g., dropdowns, radio buttons) for users to specify project mood (e.g., 'Modern', 'Classic', 'Playful', 'Corporate') and target audience.
    *   A 'Suggest Pairings' button. On click, it will **simulate** an AI suggestion by displaying a few predefined, well-known harmonious font pairs based on the selected mood (e.g., for 'Modern': 'Montserrat + Open Sans'; for 'Classic': 'Playfair Display + Lato').
    *   'Apply' button for each suggested pair to set them as current Heading/Body fonts.

7.  **`PreviewArea.jsx`**: The main display panel where the typography is rendered live.
    *   **`PreviewTextEditor.jsx`**: An editable `div` (using `contentEditable='true'`) where users can type or paste text. The text content should persist with project saves.
        *   This `div` will dynamically apply all selected font styles and metric adjustments via inline styles or CSS variables.
    *   **`PreviewSettingsToolbar.jsx`**: A set of controls to manipulate the preview environment.
        *   **Dark/Light Mode Toggle**: Switches the background and text colors of the `PreviewTextEditor` to predefined light/dark themes.
        *   **Screen Size Buttons**: Buttons (e.g., 'Mobile', 'Tablet', 'Desktop Large') that apply specific `max-width` to the `PreviewTextEditor` to simulate responsiveness.
        *   **Text Block Presets**: Dropdown or buttons to instantly populate `PreviewTextEditor` with common text structures (e.g., 'Heading + Paragraph', 'List Item Example').

**State Management:**
*   Use React's `useState` for local component state.
*   Utilize `useContext` for global typography state (e.g., an object containing `headingFont`, `bodyFont`, `fontSize`, `lineHeight`, `letterSpacing`, `textColor`, `backgroundColor`, etc.). This context will be shared between the `ControlPanel` and `PreviewArea`.

**Functionality Details:**
*   **Dynamic Font Loading**: When a font is selected (from Google Fonts or custom upload), it must be loaded into the browser so it can be applied to the preview text.
*   **Real-time Updates**: Any change in the `ControlPanel` (font selection, slider adjustment, color pick) must immediately reflect in the `PreviewArea`.
*   **CSS Export**: The 'Export CSS' button should generate a block of CSS for the currently applied styles (e.g., `@font-face` rules for custom fonts, `font-family`, `font-size`, `line-height`, `letter-spacing`, `word-spacing`, `text-rendering: optimizeLegibility` etc.) and copy it to the clipboard.
*   **Local Storage Persistence**: Implement saving and loading of the entire typography state object to and from `localStorage`.

**Styling:**
*   All components must be styled using Tailwind CSS classes for a modern, clean UI.
*   Ensure responsive design for different screen sizes.
*   Use `lucide-react` icons consistently throughout the interface.

**Initial Content:**
*   The `PreviewTextEditor` should start with some default placeholder text (e.g., 'The quick brown fox jumps over the lazy dog.').
```