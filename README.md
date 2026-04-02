# Zorvyn Finance Dashboard

A clean, interactive finance dashboard built with **React.js** and **Tailwind CSS**. This application allows users to track and understand their financial activity through visual summaries, transaction management, and insightful analytics.

![React](https://img.shields.io/badge/React-19-blue) ![TailwindCSS](https://img.shields.io/badge/Tailwind-4-06b6d4) ![Vite](https://img.shields.io/badge/Vite-8-646cff)

---

## Features

### Dashboard Overview
- **Summary cards** showing Total Balance, Income, Expenses, and Savings
- **Balance Trend chart** (time-based area chart tracking balance over months)
- **Spending Breakdown** (categorical pie/donut chart)
- **Income vs Expenses** (monthly bar chart comparison)
- **Recent Transactions** list

### Transactions
- Full transaction list with pagination
- **Search** by description or category
- **Filters** by type (income/expense), category, and date range
- **Sorting** by date, amount, or category
- Admin can **add, edit, and delete** transactions
- **Export to CSV or JSON**
- Responsive table (desktop) and card layout (mobile)

### Insights
- Highest and lowest spending categories
- Most expensive month and best savings month
- Average daily spending
- Savings rate with health indicator
- Month-over-month expense trend
- Spending pattern radar chart
- Category breakdown with progress bars

### Role-Based UI
- Toggle between **Admin** and **Viewer** roles via the sidebar
- **Admin**: Can add, edit, and delete transactions
- **Viewer**: Read-only access — action buttons are hidden

### Additional Features
- **Dark mode** toggle with localStorage persistence
- **Data persistence** via localStorage
- **Responsive design** — works on mobile, tablet, and desktop
- **Export functionality** — download transactions as CSV or JSON
- **Empty/no-data states** handled gracefully throughout

---

## Tech Stack

| Technology | Purpose |
|---|---|
| React 19 | UI framework |
| Tailwind CSS 4 | Styling |
| Vite 8 | Build tool and dev server |
| React Router 7 | Client-side routing |
| Recharts | Charts and visualizations |
| Lucide React | Icons |
| Context + useReducer | State management |

---

## Project Structure

```
src/
├── components/
│   ├── Layout.jsx              # Sidebar + topbar layout wrapper
│   ├── SummaryCard.jsx         # Reusable metric card
│   ├── BalanceTrendChart.jsx   # Area chart for balance over time
│   ├── SpendingBreakdownChart.jsx  # Donut chart for categories
│   ├── IncomeExpenseChart.jsx  # Bar chart income vs expenses
│   ├── RecentTransactions.jsx  # Recent transactions list
│   └── TransactionModal.jsx    # Add/edit transaction form
├── context/
│   └── AppContext.jsx          # Global state (transactions, role, theme, filters)
├── data/
│   └── transactions.js         # Mock data generation & localStorage helpers
├── pages/
│   ├── Dashboard.jsx           # Main overview page
│   ├── Transactions.jsx        # Transactions list + filters
│   └── Insights.jsx            # Analytics & observations
├── utils/
│   └── helpers.js              # Formatters, export utilities
├── App.jsx                     # Router setup
├── main.jsx                    # Entry point
└── index.css                   # Tailwind imports + base styles
```

---

## Getting Started

### Prerequisites

- **Node.js** 18+ and **npm**

### Installation

```bash
# Clone the repository
git clone <repository-url>
cd finance-dashboard

# Install dependencies
npm install

# Start development server
npm run dev
```

The app will be available at `http://localhost:5173`.

### Build for Production

```bash
npm run build
npm run preview
```

---

## Approach & Design Decisions

1. **State Management**: Used React Context + `useReducer` for centralized state. This keeps the app simple while properly managing transactions, filters, role, and theme in one place.

2. **Mock Data**: Transactions are auto-generated with realistic patterns (monthly salary, recurring bills, random expenses). Data persists in `localStorage` so it survives page refreshes.

3. **Role-Based UI**: Implemented as a frontend-only simulation via a sidebar toggle. The admin/viewer role controls visibility of add/edit/delete buttons — no routes are restricted, as RBAC is frontend-only per the requirements.

4. **Responsive Design**: The layout uses a collapsible sidebar (hidden on mobile with a hamburger menu). Tables switch to card layouts on smaller screens. All grid layouts adapt from 1 to 4 columns.

5. **Dark Mode**: Toggled via the header, persisted in `localStorage`. Uses Tailwind's `dark:` variant with a class-based strategy.

6. **Charts**: Used Recharts for visualizations — area chart (balance trend), pie/donut chart (spending categories), bar chart (income vs expenses), radar chart (spending patterns), and bar chart (monthly savings).

---

## Evaluation Mapping

| Criteria | Implementation |
|---|---|
| Dashboard Overview | Summary cards, 3 charts, recent transactions |
| Transactions Section | Full CRUD, search, filter, sort, pagination, export |
| Role-Based UI | Admin/Viewer toggle changes add/edit/delete visibility |
| Insights | 4 insight cards, 3 key metrics, 2 charts, category breakdown |
| State Management | Context + useReducer for all app state |
| Responsiveness | Mobile sidebar, adaptive grids, card/table switching |
| Dark Mode | Theme toggle with persistence |
| Data Persistence | localStorage for transactions and preferences |
| Export | CSV and JSON download |
