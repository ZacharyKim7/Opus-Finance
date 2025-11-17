# Opus Finance - Frontend Setup Guide

This guide will help you get started with developing the Opus Finance frontend application.

## Libraries Installed ✅

All necessary libraries have been installed and configured. See [LIBRARY_SELECTION.md](./LIBRARY_SELECTION.md) for the complete rationale.

### Key Dependencies:
- **React 19.2.0** + **Vite** - Modern React with fast HMR
- **TypeScript** - Type safety for financial calculations
- **Tailwind CSS** - Utility-first styling
- **React Router v6** - Client-side routing
- **Recharts** + **D3.js** - Data visualization
- **Zustand** - Global state management
- **TanStack Query** - Server state & data fetching
- **TanStack Table** - Powerful tables for transactions
- **React Hook Form** + **Zod** - Forms & validation
- **Lucide React** - Modern icon library
- **Framer Motion** - Smooth animations
- **Sonner** - Toast notifications

## Project Structure

```
opus-frontend/
├── src/
│   ├── lib/
│   │   └── utils.ts          # Utility functions (cn helper)
│   ├── components/           # Create reusable UI components here
│   │   ├── ui/              # Base UI components (buttons, cards, etc.)
│   │   ├── layout/          # Layout components (sidebar, header)
│   │   ├── charts/          # Chart components
│   │   └── features/        # Feature-specific components
│   ├── pages/               # Page components (Dashboard, Accounts, etc.)
│   ├── hooks/               # Custom React hooks
│   ├── store/               # Zustand stores
│   ├── types/               # TypeScript type definitions
│   ├── App.tsx
│   ├── main.tsx
│   └── index.css            # Tailwind directives
├── tailwind.config.js       # Tailwind configuration
├── postcss.config.js        # PostCSS configuration
└── package.json
```

## Getting Started

### 1. Run the Development Server

```bash
cd opus-frontend
npm run dev
```

Visit `http://localhost:5173` to see your app.

### 2. Recommended Next Steps

#### A. Set Up Routing Structure

Create the main pages based on the wireframes:

```bash
mkdir -p src/pages
touch src/pages/Dashboard.tsx
touch src/pages/Accounts.tsx
touch src/pages/Transactions.tsx
touch src/pages/CashFlow.tsx
touch src/pages/Reports.tsx
touch src/pages/Budget.tsx
touch src/pages/Recurring.tsx
touch src/pages/Goals.tsx
touch src/pages/Investments.tsx
```

Then set up React Router in `src/App.tsx`:

```tsx
import { BrowserRouter, Routes, Route } from 'react-router-dom';
import Dashboard from './pages/Dashboard';
import Accounts from './pages/Accounts';
// ... import other pages

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Dashboard />} />
        <Route path="/accounts" element={<Accounts />} />
        {/* ... other routes */}
      </Routes>
    </BrowserRouter>
  );
}
```

#### B. Create Layout Components

Build the sidebar navigation and main layout:

```bash
mkdir -p src/components/layout
touch src/components/layout/Sidebar.tsx
touch src/components/layout/MainLayout.tsx
touch src/components/layout/Header.tsx
```

#### C. Set Up State Management

Create Zustand stores for your data:

```bash
mkdir -p src/store
touch src/store/accountStore.ts
touch src/store/budgetStore.ts
touch src/store/transactionStore.ts
```

Example store (`src/store/accountStore.ts`):

```tsx
import { create } from 'zustand';

interface Account {
  id: string;
  name: string;
  balance: number;
  type: 'checking' | 'savings' | 'credit' | 'investment';
}

interface AccountStore {
  accounts: Account[];
  addAccount: (account: Account) => void;
  updateAccount: (id: string, updates: Partial<Account>) => void;
}

export const useAccountStore = create<AccountStore>((set) => ({
  accounts: [],
  addAccount: (account) => set((state) => ({
    accounts: [...state.accounts, account]
  })),
  updateAccount: (id, updates) => set((state) => ({
    accounts: state.accounts.map((acc) =>
      acc.id === id ? { ...acc, ...updates } : acc
    ),
  })),
}));
```

#### D. Build UI Components

Start with basic components using Tailwind:

```bash
mkdir -p src/components/ui
touch src/components/ui/Button.tsx
touch src/components/ui/Card.tsx
touch src/components/ui/Input.tsx
```

Example Button component:

```tsx
import { cn } from '@/lib/utils';
import { ButtonHTMLAttributes, forwardRef } from 'react';

interface ButtonProps extends ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'primary' | 'secondary' | 'ghost';
}

const Button = forwardRef<HTMLButtonElement, ButtonProps>(
  ({ className, variant = 'primary', ...props }, ref) => {
    return (
      <button
        ref={ref}
        className={cn(
          'px-4 py-2 rounded-lg font-medium transition-colors',
          variant === 'primary' && 'bg-primary-500 text-white hover:bg-primary-600',
          variant === 'secondary' && 'bg-gray-200 text-gray-900 hover:bg-gray-300',
          variant === 'ghost' && 'hover:bg-gray-100',
          className
        )}
        {...props}
      />
    );
  }
);

export default Button;
```

#### E. Implement Charts

Create chart components using Recharts:

```bash
mkdir -p src/components/charts
touch src/components/charts/NetWorthChart.tsx
touch src/components/charts/SpendingChart.tsx
touch src/components/charts/CashFlowSankey.tsx
```

Example chart (`src/components/charts/NetWorthChart.tsx`):

```tsx
import { AreaChart, Area, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'recharts';

interface NetWorthChartProps {
  data: { date: string; value: number }[];
}

export function NetWorthChart({ data }: NetWorthChartProps) {
  return (
    <ResponsiveContainer width="100%" height={300}>
      <AreaChart data={data}>
        <CartesianGrid strokeDasharray="3 3" stroke="#e5e7eb" />
        <XAxis dataKey="date" stroke="#6b7280" />
        <YAxis stroke="#6b7280" />
        <Tooltip />
        <Area
          type="monotone"
          dataKey="value"
          stroke="#3b82f6"
          fill="#93c5fd"
          fillOpacity={0.3}
        />
      </AreaChart>
    </ResponsiveContainer>
  );
}
```

#### F. Set Up TanStack Query

Wrap your app with QueryClientProvider in `src/main.tsx`:

```tsx
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';
import { QueryClient, QueryClientProvider } from '@tanstack/react-query';
import './index.css';
import App from './App.tsx';

const queryClient = new QueryClient({
  defaultOptions: {
    queries: {
      staleTime: 60 * 1000, // 1 minute
      refetchOnWindowFocus: false,
    },
  },
});

createRoot(document.getElementById('root')!).render(
  <StrictMode>
    <QueryClientProvider client={queryClient}>
      <App />
    </QueryClientProvider>
  </StrictMode>,
);
```

## Development Workflow

### Building Pages

Refer to the wireframes in `/docs/wireframes/` as you build:
- `dashboard.png` - Main dashboard with budget, net worth, transactions
- `accounts.webp` - Accounts overview with grouping
- `budget.png` - Budget page with income/expense breakdown
- `reports-cashflow.png` - Sankey diagram for cash flow
- `reports-spending.webp` - Donut chart and transaction list
- `Specific account.png` - Individual account detail view

### Mock Data

For now, create mock data files to simulate the backend:

```bash
mkdir -p src/data
touch src/data/mockAccounts.ts
touch src/data/mockTransactions.ts
touch src/data/mockBudgets.ts
```

Example mock data:

```tsx
// src/data/mockAccounts.ts
export const mockAccounts = [
  {
    id: '1',
    name: "Melanie's Checking",
    type: 'checking' as const,
    balance: 15234.75,
    institution: 'Citibank Online',
  },
  {
    id: '2',
    name: 'Joint Savings',
    type: 'savings' as const,
    balance: 50107.55,
    institution: 'Bank of America',
  },
  // ... more accounts
];
```

### Styling Tips

- Use Tailwind utility classes for most styling
- Use the `cn()` utility from `src/lib/utils.ts` to merge classes conditionally
- Reference the color palette in `tailwind.config.js`:
  - `primary-*` for orange/coral accent
  - `success-*` for positive values (green)
  - `danger-*` for negative/over-budget (red)
- Common patterns:
  - Cards: `bg-white rounded-lg shadow-sm p-6`
  - Sidebar: `bg-white border-r border-gray-200`
  - Hover states: `hover:bg-gray-50 transition-colors`

### TypeScript Configuration

The project uses strict TypeScript. Create type definitions in `src/types/`:

```bash
mkdir -p src/types
touch src/types/account.ts
touch src/types/transaction.ts
touch src/types/budget.ts
```

Example types:

```tsx
// src/types/account.ts
export interface Account {
  id: string;
  name: string;
  type: 'checking' | 'savings' | 'credit' | 'investment';
  balance: number;
  institution: string;
  lastUpdated: Date;
}
```

## Testing the Build

```bash
npm run build
npm run preview
```

## Useful Commands

- `npm run dev` - Start development server
- `npm run build` - Build for production
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint

## Resources

- [React Router Docs](https://reactrouter.com/)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [Recharts Documentation](https://recharts.org/)
- [Zustand Guide](https://docs.pmnd.rs/zustand/)
- [TanStack Query Docs](https://tanstack.com/query/latest)
- [Lucide Icons](https://lucide.dev/)

## Next Steps

1. Create the sidebar navigation component
2. Build the Dashboard page layout
3. Implement the net worth chart component
4. Create the accounts list component
5. Build the budget page with progress bars
6. Implement transaction lists
7. Create the cash flow Sankey diagram
8. Add animations and transitions

Happy coding! 🚀
