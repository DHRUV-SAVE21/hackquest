# 🧭 Navbar Update

I have reorganized the navigation bar to provide a cleaner, more professional header.

## 1. New Structure
The navigation is now grouped as follows:

-   **Priority Tabs (Left-to-Right):**
    1.  **Dashboard** (`/dashboard`)
    2.  **Crop AI** (`/crop-recommendation`)
    3.  **Schemes** (`/schemes-assistant`)
    4.  **Land Map** (`/mark-my-land`)
-   **Services Dropdown:** A clean dropdown menu containing:
    -   Disaster News
    -   Autonomous Farm
    -   Equipment
    -   Inventory
    -   Marketplace

## 2. Technical Changes
-   **Split Logic:** Separated `NAV_Links` into `MAIN_LINKS` and `SERVICE_LINKS`.
-   **Dropdown Component:** Added a state-driven/hover-driven dropdown for "Services" using `lucide-react` icons.
-   **Mobile Layout:** The mobile menu automatically merges all links into a single list for ease of access on small screens.

## 3. How to Modify
If you need to move a tab from **Services** to **Main** (or vice versa), edit `frontend/src/components/layout/GooeyNavbar.jsx`:
-   Move the object from `SERVICE_LINKS` array to `MAIN_LINKS` array.
