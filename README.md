# Zorvyn Finance Dashboard

A clean, interactive finance dashboard built with **React.js** and **Tailwind CSS** that allows users to track and understand their financial activity through visual summaries, transaction management, and insightful analytics.

This is a **frontend-only** application — no backend or database required. It runs entirely in the browser using mock data and localStorage for persistence.

---

## Setup Instructions

### Prerequisites

- **Node.js** 18+ and **npm** installed ([download here](https://nodejs.org))


Open **(https://zorvyn-fintech-dashboard.vercel.app/)** in your browser.

## Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| React | 19 | UI framework (components, hooks, rendering) |
| Vite | 8 | Build tool & dev server (fast HMR) |
| Tailwind CSS | 4 | Utility-first CSS styling |
| React Router | 7 | Client-side page routing |
| Recharts | 3 | Data visualizations (area, bar, pie, radar charts) |
| Lucide React | 1.7 | Lightweight SVG icon library |
| Context + useReducer | built-in | Centralized state management |
| localStorage | browser API | Data & preference persistence |

---

## Features Overview

### 1. Dashboard Overview (`/`)

- **4 Summary Cards** — Total Balance, Income, Expenses, and Savings with month-over-month trend indicators
- **Balance Trend Chart** — Time-based area chart showing balance progression over 6 months
- **Spending Breakdown** — Categorical donut/pie chart with percentage legend
- **Income vs Expenses** — Monthly bar chart comparison
- **Recent Transactions** — Quick-view list of the 5 most recent transactions

### 2. Transactions Page (`/transactions`)

- Full paginated transaction list (10 per page)
- **Search** — Filter by description or category keywords
- **Multi-filter panel** — Filter by type (income/expense), category, and date range
- **Column sorting** — Sort by date, amount, or category (ascending/descending)
- **CRUD operations** — Add, edit, and delete transactions via a modal form (admin only)
- **Export** — Download filtered results as CSV or JSON
- **Responsive** — Desktop table view switches to mobile card layout

### 3. Insights Page (`/insights`)

- **4 Insight Cards** — Highest spending category, lowest spending category, most expensive month, best savings month
- **3 Key Metrics** — Average daily spending, savings rate (with health indicator), month-over-month expense trend
- **Monthly Savings Chart** — Bar chart of net savings per month
- **Spending Pattern Radar** — Radar chart visualizing top spending categories
- **Category Breakdown** — Progress bars showing each category's share of total expenses

### 4. Role-Based UI

Simulated RBAC via a sidebar toggle — no backend auth required:

| Role | Capabilities |
|---|---|
| **Admin** | View all data + Add, Edit, Delete transactions |
| **Viewer** | View all data only (action buttons hidden) |

Switch roles instantly using the Admin/Viewer toggle in the sidebar.

### 5. State Management

All application state is managed via **React Context + useReducer**:

- `transactions` — The full transaction list
- `filters` — Search query, type, category, date range, sort column/order
- `role` — Current user role (admin/viewer)
- `darkMode` — Theme preference

A single `appReducer` handles all state transitions (add/update/delete transactions, filter changes, role switch, theme toggle). This approach avoids external dependencies while keeping state centralized and predictable.

### 6. Additional Features

- **Dark Mode** — Toggle via header button, persisted in localStorage, uses Tailwind `dark:` variants
- **Data Persistence** — Transactions and theme preference survive page refreshes via localStorage
- **Responsive Design** — Collapsible sidebar on mobile, adaptive grid layouts (1–4 columns), table-to-card switching
- **Export** — Download filtered transactions as CSV or JSON files
- **Empty States** — Graceful handling when no data or no filter matches
- **Favicon** — Custom branded SVG favicon

---

## Project Structure

```
finance-dashboard/
├── public/
│   └── favicon.svg
├── src/
│   ├── components/
│   │   ├── Layout.jsx                 # App shell: sidebar + topbar + responsive nav
│   │   ├── SummaryCard.jsx            # Reusable metric card with trend indicator
│   │   ├── BalanceTrendChart.jsx      # Area chart — balance over time
│   │   ├── SpendingBreakdownChart.jsx # Donut chart — expense categories
│   │   ├── IncomeExpenseChart.jsx     # Bar chart — monthly income vs expenses
│   │   ├── RecentTransactions.jsx     # List of 5 most recent transactions
│   │   └── TransactionModal.jsx       # Add/edit transaction form modal
│   ├── context/
│   │   └── AppContext.jsx             # Global state provider (Context + useReducer)
│   ├── data/
│   │   └── transactions.js            # Mock data generator + localStorage helpers
│   ├── pages/
│   │   ├── Dashboard.jsx              # Main overview with cards + charts
│   │   ├── Transactions.jsx           # Transaction list with filters + CRUD
│   │   └── Insights.jsx               # Analytics and financial observations
│   ├── utils/
│   │   └── helpers.js                 # Currency/date formatters, CSV/JSON export
│   ├── App.jsx                        # Router configuration
│   ├── main.jsx                       # Application entry point
│   └── index.css                      # Tailwind imports + base styles
├── index.html
├── vite.config.js
├── package.json
└── README.md
```

---

## Approach & Design Decisions

1. **Why Vite over CRA?** — Vite offers significantly faster dev server startup and hot module replacement. Create React App is deprecated and slower.

2. **Why Context + useReducer over Redux/Zustand?** — The app's state is straightforward (transactions, filters, role, theme). A single reducer keeps it centralized without adding external dependencies. For a larger app, Redux or Zustand would be appropriate.

3. **Why Recharts?** — Most popular React charting library with a declarative JSX API, built-in responsive containers, and good variety of chart types (area, bar, pie, radar).

4. **Mock Data Strategy** — Transactions are auto-generated on first load with realistic patterns: monthly salary, recurring utilities, random expenses across categories. Data persists in localStorage so the experience is consistent across page refreshes.

5. **Role-Based UI** — Implemented as frontend-only simulation per the assignment spec. The role state controls conditional rendering of add/edit/delete UI elements. No routes are restricted — both roles can navigate freely.

6. **Responsive Approach** — Mobile-first using Tailwind's responsive breakpoints (`sm:`, `lg:`). The sidebar collapses to a hamburger menu on mobile. The transaction table switches to a card layout on small screens. Grids adapt from 1 to 4 columns.

7. **Dark Mode** — Class-based dark mode using Tailwind's `dark:` variant. Toggled by adding/removing the `dark` class on `<html>`. Preference persisted in localStorage.

---

## Evaluation Criteria Mapping

| Criteria | Implementation |
|---|---|
| **Design & Creativity** | Clean card-based layout, color-coded categories, branded sidebar, donut + area + bar + radar charts |
| **Responsiveness** | Collapsible sidebar, adaptive grids, table/card switching, mobile-optimized filters |
| **Functionality** | Dashboard overview, full CRUD transactions, search/filter/sort, insights analytics, role-based UI |
| **User Experience** | Intuitive navigation, clear visual hierarchy, empty state handling, export options |
| **Technical Quality** | Modular component structure, single-responsibility files, centralized state, no prop drilling |
| **State Management** | Context + useReducer managing transactions, filters, role, and theme in one place |
| **Documentation** | This README — setup, features, structure, approach, and design decisions |
| **Attention to Detail** | Trend indicators, percentage labels, formatted currencies, pagination, dark mode persistence |
