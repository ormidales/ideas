# PebbleMind

## Concept

PebbleMind is a unique web tool designed to help users capture, organize, and rediscover bite-sized insights, facts, links, quotes, and ideas – their digital 'pebbles.' In an age of information overload, valuable nuggets of knowledge often get lost. PebbleMind provides a streamlined interface to quickly save these snippets, tag them for easy categorization, add source context, and attach personal notes. Beyond simple storage, it offers powerful search and filtering capabilities, allowing users to effortlessly resurface relevant information. The tool's core value lies in transforming scattered information into a structured, interconnected personal knowledge base, fostering deeper learning, sparking creativity, and ensuring that no valuable insight ever gets forgotten.

## Technical prompt

```md
Build a modern, single-page React application named 'PebbleMind' using Vite for project setup and Tailwind CSS for styling. The application will serve as a personal knowledge manager for 'pebbles' (small insights, links, quotes).

**Project Setup:**
1.  Initialize a new React project using Vite. Configure it for TypeScript if possible, otherwise plain JavaScript is fine.
2.  Integrate and configure Tailwind CSS according to the official documentation.
3.  Install necessary libraries: `lucide-react` for icons, `react-router-dom` for navigation, `react-hot-toast` for notifications.

**Core Application Structure & Pages:**
1.  **Layout Component:** Create a `Layout` component that includes a responsive navigation bar (header) and a main content area. The header should contain the app logo/name, and potentially a user profile/settings link.
2.  **Authentication Pages (Mock):**
    *   `LoginPage`: A simple form with username/email and password fields, and a link to `RegisterPage`.
    *   `RegisterPage`: A simple form for username/email, password, and confirm password fields.
    *   Implement basic client-side authentication logic (e.g., storing a mock `authToken` and `currentUser` in `localStorage` upon 'successful' login/register, and redirecting).
3.  **Protected Routes:** Ensure that `Dashboard`, `AddPebble`, `PebbleDetail`, and `Tags` pages are only accessible after successful mock authentication.
4.  **Dashboard Page (`/dashboard`):**
    *   Display a greeting to the user.
    *   Show a summary section: e.g., 'Total Pebbles', 'Most Used Tags', 'Recently Added Pebbles' (a small list/grid of PebbleCards).
    *   Include a prominent 'Add New Pebble' button that navigates to the `AddPebble` page.
5.  **Add/Edit Pebble Page (`/add-pebble` or `/pebble/:id/edit`):**
    *   A form for adding or editing a pebble with the following fields:
        *   `Content`: A large textarea for the main insight/quote/text. (Required)
        *   `Source URL`: An optional text input for a link.
        *   `Tags`: A multi-select or input field that allows users to add multiple tags (e.g., 'programming', 'philosophy', 'productivity'). Tags should be dynamically added/managed. Suggest using a `TagInput` component that converts input to distinct tags.
        *   `Notes`: An optional textarea for additional context.
    *   'Save Pebble' and 'Cancel' buttons.
6.  **Pebble List Page (Integrated into Dashboard or separate `/pebbles`):**
    *   Display all the user's pebbles in a responsive grid or list view.
    *   **Search Bar:** A text input to filter pebbles by content, source, or tags.
    *   **Tag Filter:** A section displaying all unique tags, allowing users to click a tag to filter the list.
    *   Each pebble in the list should be a `PebbleCard` component.
7.  **Pebble Detail Page (`/pebble/:id`):**
    *   Display the full content, source URL (clickable), tags (clickable to filter), and notes of a specific pebble.
    *   'Edit' and 'Delete' buttons (using a `Modal` for deletion confirmation).
8.  **Tag Management Page (`/tags`):**
    *   List all unique tags used by the user.
    *   Option to rename or delete a tag. (Deleting a tag should remove it from all associated pebbles).

**Components:**
*   `PebbleCard`: Displays a preview of a pebble (e.g., first few lines of content, tags). Should be clickable to navigate to `PebbleDetail`.
*   `TagPill`: A small, styled component for displaying individual tags, possibly with a close button if used in an input context.
*   `Button`: Reusable button component with primary/secondary styles.
*   `Input`, `TextArea`: Reusable form input components.
*   `Modal`: A generic modal component for confirmations (e.g., delete).

**State Management & Data Persistence:**
*   Use React's `useState`, `useEffect`, and `useContext` hooks for local and global state management (e.g., `AuthContext` for user, `PebbleContext` for managing pebble data).
*   **Crucially, all data (user info, pebbles, tags) should be stored and managed in `localStorage` for development purposes.** This simulates a backend without requiring one. Ensure `localStorage` updates are synchronized with React state.

**Styling & Responsiveness:**
*   Utilize Tailwind CSS extensively for all styling. Focus on a clean, minimalist, and modern aesthetic.
*   Ensure the application is fully responsive and looks good on desktop, tablet, and mobile devices.
*   Use `lucide-react` for all icons (e.g., add, edit, delete, search, home, user).

**Notifications:**
*   Integrate `react-hot-toast` for showing success, error, or informational messages (e.g., 'Pebble saved successfully!', 'Login failed.').

**Implementation Details:**
*   When adding/editing pebbles, tags should be parsed from a comma-separated string or managed through a dynamic input array.
*   For filtering by tags, clicking a tag in the `PebbleList` or `PebbleDetail` should update the filter state.
*   Thoroughly comment the code for clarity.
```