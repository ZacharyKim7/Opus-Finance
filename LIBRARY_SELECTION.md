# Opus Finance - React Library Selection

This document outlines the selected libraries, frameworks, and tools for building the Opus Finance frontend.

## Core Framework

### React 19.2.0 + Vite
- **Why:** Modern React with latest features, Vite provides fast HMR and optimal build performance
- **Already installed:** ✅

## Styling & UI Foundation

### Tailwind CSS
- **Purpose:** Utility-first CSS framework for rapid UI development
- **Why:** Provides flexibility to match the custom design in wireframes, excellent for creating the clean, modern interface
- **Packages:** `tailwindcss`, `postcss`, `autoprefixer`

### Shadcn/ui
- **Purpose:** Component library built on Radix UI primitives with Tailwind
- **Why:**
  - Highly customizable, copy-paste components (not a dependency)
  - Modern design system perfect for finance apps
  - Accessible by default (Radix UI primitives)
  - Full control over component styling
- **Packages:** `@radix-ui/*` (various), `class-variance-authority`, `clsx`, `tailwind-merge`

## Routing

### React Router v6
- **Purpose:** Client-side routing for multi-page navigation
- **Why:** Industry standard, powerful API, supports nested routes for Dashboard/Accounts/Budget/etc.
- **Package:** `react-router-dom`

## Charts & Data Visualization

### Recharts
- **Purpose:** Primary charting library for line, area, bar, and donut charts
- **Why:**
  - React-native API, composable components
  - Perfect for financial charts (net worth, spending trends, budget progress)
  - Responsive and customizable
- **Package:** `recharts`

### D3.js + react-d3-sankey
- **Purpose:** Sankey diagrams for cash flow visualization
- **Why:** D3 is the gold standard for complex visualizations, sankey component matches your cash flow wireframe
- **Packages:** `d3`, `d3-sankey`, `d3-scale`, `d3-shape`

## State Management

### Zustand
- **Purpose:** Global state management
- **Why:**
  - Lightweight (1kb), simple API
  - Perfect for managing app-wide state (user data, accounts, budgets, goals)
  - No boilerplate, easy to test
- **Package:** `zustand`

### TanStack Query (React Query)
- **Purpose:** Server state management, data fetching, and caching
- **Why:**
  - Handles async operations, caching, refetching
  - Perfect for Plaid data, transaction syncing
  - Automatic background updates
- **Package:** `@tanstack/react-query`

## Data Tables

### TanStack Table
- **Purpose:** Headless table library for transaction lists and budget tables
- **Why:**
  - Powerful sorting, filtering, pagination
  - Headless = full styling control
  - Great TypeScript support
- **Package:** `@tanstack/react-table`

## Forms & Validation

### React Hook Form
- **Purpose:** Form state management and validation
- **Why:**
  - Performant (uncontrolled components)
  - Great DX, minimal re-renders
  - Perfect for budget entry, goal creation, custom categories
- **Package:** `react-hook-form`

### Zod
- **Purpose:** Schema validation
- **Why:**
  - TypeScript-first validation
  - Integrates seamlessly with React Hook Form
  - Ensures data integrity for financial data
- **Package:** `zod`

## Icons

### Lucide React
- **Purpose:** Icon library
- **Why:**
  - Modern, consistent design (matches your wireframe style)
  - Large collection of finance-relevant icons
  - Lightweight, tree-shakeable
- **Package:** `lucide-react`

## Date Handling

### date-fns
- **Purpose:** Date manipulation and formatting
- **Why:**
  - Modern, functional API
  - Tree-shakeable (small bundle size)
  - Perfect for financial date ranges, budget periods, transaction dates
- **Package:** `date-fns`

## Utilities

### clsx + tailwind-merge
- **Purpose:** Conditional className management
- **Why:** Clean conditional styling, Tailwind class merging
- **Packages:** `clsx`, `tailwind-merge`

### currency.js
- **Purpose:** Currency formatting and calculations
- **Why:**
  - Handles floating-point precision issues
  - Consistent currency formatting
  - Essential for financial calculations
- **Package:** `currency.js`

## Development Tools

### TypeScript (Already installed) ✅
- **Purpose:** Type safety
- **Why:** Critical for financial applications to prevent calculation errors

### ESLint (Already installed) ✅
- **Purpose:** Code quality and consistency

## Additional Recommendations

### React Transition Group or Framer Motion
- **Purpose:** Animations and transitions
- **Why:** Smooth page transitions, micro-interactions for polished UX
- **Package:** `framer-motion` (recommended for modern API)

### Sonner or React Hot Toast
- **Purpose:** Toast notifications
- **Why:** User feedback for actions (sync complete, budget saved, etc.)
- **Package:** `sonner` (recommended - beautiful defaults)

## Summary

This stack provides:
- ✅ Modern, fast development experience (Vite + React 19)
- ✅ Flexible, customizable UI (Tailwind + Shadcn/ui)
- ✅ Comprehensive charting capabilities (Recharts + D3)
- ✅ Robust state management (Zustand + TanStack Query)
- ✅ Type-safe development (TypeScript + Zod)
- ✅ Excellent performance (optimized libraries, tree-shaking)
- ✅ Great developer experience (minimal boilerplate)

## Installation Commands

See `package.json` for the complete list of installed dependencies.
