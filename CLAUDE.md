# CLAUDE.md
必ず日本語で回答してください。
This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Next.js 15 dashboard application built as part of the Next.js App Router tutorial. It's a modern invoice management system with customer tracking and authentication features.

## Development Commands

- **Development server**: `npm run dev` (uses Turbopack for faster builds)
- **Build**: `npm run build`
- **Production start**: `npm start`
- **Lint**: `npm run lint`

The project uses pnpm as the package manager (see pnpm-lock.yaml).

## Architecture & Structure

### App Router Structure
- Uses Next.js 15 App Router with nested layouts
- Root layout (`app/layout.tsx`) handles global styles and fonts
- Dashboard layout (`app/dashboard/layout.tsx`) includes sidebar navigation
- Route groups: `(overview)` for default dashboard view
- Dynamic routes: `[id]` for individual invoice/customer pages

### Key Directories
- `app/lib/`: Core business logic and utilities
  - `actions.ts`: Server actions for CRUD operations (createInvoice, updateInvoice, deleteInvoice)
  - `data.ts`: Database queries and data fetching functions
  - `definitions.ts`: TypeScript type definitions for all data models
  - `utils.ts`: Helper functions including formatCurrency
- `app/ui/`: Reusable UI components organized by feature
  - `dashboard/`: Dashboard-specific components (cards, charts, navigation)
  - `invoices/`: Invoice-related components (forms, tables, status indicators)
  - `customers/`: Customer management components

### Database & Data Flow
- PostgreSQL database with direct SQL queries using the `postgres` library
- Server actions handle form submissions and data mutations
- Zod schema validation for form data (`FormSchema` in actions.ts)
- Type-safe data models defined in `definitions.ts`
- Currency amounts stored as cents in database, formatted for display

### Styling & UI
- Tailwind CSS with custom configuration
- Custom color palette (blue variants: 400, 500, 600)
- Custom grid template (13-column grid)
- Shimmer animation keyframes for loading states
- @tailwindcss/forms plugin for form styling
- Inter font family from Google Fonts

### Features
- Invoice CRUD operations with form validation
- Customer management
- Dashboard with revenue charts and latest invoices
- Search and pagination for data tables
- Loading states and error handling
- Partial Prerendering (PPR) enabled experimentally

### Environment Setup
- Requires `.env` file with `POSTGRES_URL` for database connection
- SSL required for PostgreSQL connection
- TypeScript strict mode enabled
- Path alias `@/*` maps to project root

### Authentication
- Uses NextAuth 5.0 beta for authentication
- Bcrypt for password hashing

## Development Notes

- The app uses Server Components by default with Server Actions for data mutations
- Form validation uses Zod schemas with proper error handling
- Database queries include artificial delays in development for demo purposes (remove in production)
- Error boundaries implemented for graceful error handling
- Incremental Partial Prerendering (PPR) enabled in next.config.ts