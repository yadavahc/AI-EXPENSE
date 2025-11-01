# AI Splitwise Clone - Copilot Instructions

This document helps AI coding agents understand key patterns and workflows in this Next.js-based expense splitting application.

## Architecture Overview

### Tech Stack

- **Frontend**: Next.js 13+ (App Router), TailwindCSS, Shadcn UI
- **Backend**: Convex (Backend-as-a-Service)
- **Authentication**: Clerk
- **Background Jobs**: Inngest
- **Email**: Resend
- **AI Features**: Google Gemini

### Key Components

1. **Authentication Layer** (`app/(auth)/*`)

   - Sign-in/up flows managed by Clerk
   - Protected routes in `app/(main)/*`

2. **Data Layer** (`convex/*`)

   - Schema defined in `convex/schema.js`
   - Core models: Users, Expenses, Settlements, Groups
   - Queries and mutations organized by domain (`expenses.js`, `groups.js`, etc.)

3. **UI Components** (`components/*`)
   - Base UI components in `components/ui/*` using Shadcn
   - Feature components colocated with pages in `app/(main)/*/components/`

## Common Patterns

### Data Access

```javascript
// Queries (Read)
const data = useQuery(api.module.queryName, args);

// Mutations (Write)
const mutation = useMutation(api.module.mutationName);
mutation({ arg1, arg2 });
```

### Component Organization

- Page-specific components live in `app/(main)/[feature]/components/`
- Shared components in `components/`
- UI primitives in `components/ui/`

### Authentication Flow

- `ConvexClientProvider` wraps app for auth integration
- Use `useStoreUser` hook for current user access
- Protected routes check auth in layout components

## Development Workflow

### Environment Setup

Required env variables in `.env`:

```
CONVEX_DEPLOYMENT=
NEXT_PUBLIC_CONVEX_URL=
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=
CLERK_SECRET_KEY=
RESEND_API_KEY=
GEMINI_API_KEY=
```

### Database Schema

- Core schema in `convex/schema.js`
- Use Convex indexes for common query patterns
- Search indexes for name/email lookups

### Common Commands

```bash
npm run dev      # Start development server
npx convex dev   # Start Convex development
```

## Key Files

- `convex/schema.js` - Database schema definition
- `app/(main)/layout.jsx` - Main app layout with authentication
- `components/convex-client-provider.jsx` - Auth integration
- `lib/expense-categories.js` - Expense categorization logic

## Extension Points

- Add new expense categories in `lib/expense-categories.js`
- Background jobs configured in `inngest/` directory
- Email templates managed through Resend
