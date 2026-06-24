# OpsGPT Frontend Service

The **OpsGPT Frontend Service** is a responsive React single-page application (SPA) acting as the primary operations portal for developers, senior engineers, and administrators. It connects to the core API to list incidents, manage teams, inspect knowledge base articles, and configure monitoring sources.

---

## Technical Stack

*   **UI Framework**: React 18 / React DOM (using ES modules via Vite)
*   **Routing**: React Router DOM (client-side routing)
*   **HTTP Client**: Axios (configured with intercepts for JWT token injection)
*   **Styling**: Tailwind CSS configuration alongside native component stylesheet files
*   **Icons**: Lucide React library

---

## Locked Design System & Aesthetic Palette

The visual layout adheres strictly to the locked OpsGPT design guidelines:

| Visual Token | Hex Code | Purpose / UI Placement |
| :--- | :--- | :--- |
| **Primary Teal** | `#0F766E` | Brand buttons, navigation highlights, header focus. |
| **Teal Hover** | `#115E59` | Interactive element hover states. |
| **Teal Accent** | `#0891B2` | Focus lines, tabs, highlighting elements. |
| **Dark Slate** | `#0F172A` | Background of sidebar navigation panels. |
| **Muted Text** | `#64748B` | Subtitles, disabled tabs, metadata timestamps. |
| **Background** | `#F8FAFC` | Global viewport background. |
| **Surface/Card** | `#FFFFFF` | Form panels, incident detail cards, modal backgrounds. |
| **Border** | `#E2E8F0` | Structural borders, card outlines. |
| **Success** | `#059669` | `resolved` status tags, confirmation states. |
| **Warning** | `#D97706` | `warning` severity tags, pending actions. |
| **Danger** | `#DC2626` | `critical` severity tags, fatal error notifications. |

---

## Key UI Components & Interactions

*   **Global Sidebar Layout**: Responsive sidebar panel that collapses on smaller viewport dimensions. Includes an accessible header panel, selected project switcher, dynamic breadcrumbs, and a skip-to-content accessibility hook.
*   **Responsiveness**: Tables automatically wrap inside horizontal scroll boxes (`overflow-x-auto`) to guarantee readability on mobile viewports.
*   **Webhook Copy Shortcut**: Prompts monitoring endpoints with helper copy mechanisms utilizing `navigator.clipboard.writeText` alongside custom fallback mechanisms.
*   **Async Debounced Search**: User assignment searches debounce requests to the Core API to limit database traffic.
*   **DevOps Alertmanager Receiver**: Documentation-only configuration instructions are included for Alertmanager integrations.

---

## Development Setup & Installation

To run this application locally, ensure you have **Node.js v18+** installed.

### 1. Configure Settings
Create a `.env` file in the root directory:
```env
VITE_CORE_API_URL=/api/core
```

### 2. Install Dependencies
Run the command below in the `frontend-service` folder:
```bash
npm install
```

### 3. Run Local Server
Launch the hot-reloading development server:
```bash
npm run dev
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

### 4. Build for Production
Bundle and optimize static assets into the `dist` directory:
```bash
npm run build
```

---

## Containerization & Nginx Hosting

For containerized environments (Kubernetes AKS, Docker Compose), the frontend is packaged using a multi-stage Docker build:
1.  **Stage 1 (Build)**: Compiles the Vite output.
2.  **Stage 2 (Run)**: Serves static pages using Nginx on Port **`3000`**.
3.  **Config**: The routing routes all requests back to `index.html` to allow React Router to handle page history updates.
