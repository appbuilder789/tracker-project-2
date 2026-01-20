# GrandmasterTracker

## Overview

GrandmasterTracker is a chess player tracking application that displays live leaderboard data and detailed player statistics from Chess.com. The app fetches real-time data from the Chess.com public API and presents it through a modern, dark-themed interface optimized for viewing chess grandmaster rankings and individual player performance metrics.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter for lightweight client-side routing
- **State Management**: TanStack React Query for server state and caching
- **Styling**: Tailwind CSS with custom CSS variables for theming
- **UI Components**: shadcn/ui component library (Radix UI primitives)
- **Charts**: Recharts for data visualization
- **Animations**: Framer Motion for page transitions

The frontend follows a component-based architecture with:
- Pages in `client/src/pages/` (Leaderboard, PlayerProfile, NotFound)
- Reusable components in `client/src/components/`
- Custom hooks in `client/src/hooks/` for data fetching
- Shared type definitions and schemas in `shared/`

### Backend Architecture
- **Runtime**: Node.js with Express 5
- **Language**: TypeScript with ES modules
- **Build Tool**: Vite for frontend, esbuild for server bundling
- **Development**: Hot module replacement via Vite dev server

The server acts as a proxy to the Chess.com API with:
- In-memory caching for leaderboard data (5-minute TTL)
- REST API endpoints defined in `shared/routes.ts`
- Zod schemas for request/response validation

### Data Storage
- **ORM**: Drizzle ORM with PostgreSQL dialect
- **Schema Location**: `shared/schema.ts`
- **Database**: PostgreSQL (connection via `DATABASE_URL` environment variable)
- **Current Usage**: Schema exists for potential player caching/favorites, but primary data comes from external Chess.com API

### API Design
- Typed API routes defined in `shared/routes.ts` with Zod validation
- `GET /api/leaderboard` - Fetches top 50 blitz players
- `GET /api/player/:username/stats` - Fetches individual player statistics

The API layer validates responses against Zod schemas for type safety between frontend and backend.

## External Dependencies

### Chess.com Public API
- Base URL: `https://api.chess.com/pub`
- Used for fetching leaderboards and player statistics
- Follows Chess.com API etiquette with proper User-Agent headers
- No authentication required

### Database
- PostgreSQL database required (provision via Replit or set `DATABASE_URL`)
- Drizzle Kit for schema migrations (`npm run db:push`)

### Key NPM Packages
- `@tanstack/react-query` - Server state management
- `drizzle-orm` / `drizzle-zod` - Database ORM and validation
- `recharts` - Data visualization charts
- `framer-motion` - Animation library
- `wouter` - Client-side routing
- `zod` - Runtime type validation
- Full shadcn/ui component suite via Radix UI primitives