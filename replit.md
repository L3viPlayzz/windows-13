# Windows 13 Simulator

## Overview

Windows 13 Simulator is a fully-featured browser-based operating system simulator that recreates a Windows-like desktop experience. Built with React, TypeScript, and Express.js, it provides a realistic desktop environment with window management, a taskbar, start menu, and a comprehensive suite of built-in applications including a file explorer, browser, terminal, calculator, calendar, and more. The project also features an app store for installing additional applications, multiple authentication methods (PIN, password, Windows Hello face recognition), and PWA support for installation on devices.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite with hot module replacement
- **Styling**: Tailwind CSS v4 with custom theme variables and CSS-in-JS via class-variance-authority
- **UI Components**: Radix UI primitives with shadcn/ui component library (New York style)
- **State Management**: React Query for server state, React Context for global UI state (SystemSettingsContext, FileSystemContext)
- **Routing**: Wouter for lightweight client-side routing
- **Animations**: Framer Motion for window animations and transitions

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript compiled via esbuild for production
- **API Structure**: RESTful endpoints under `/api/` prefix
- **Static Serving**: Vite dev server in development, static file serving in production

### Data Storage Solutions
- **Database**: PostgreSQL via Neon serverless driver with Drizzle ORM
- **Schema Location**: `shared/schema.ts` contains all table definitions
- **Client-Side Storage**: IndexedDB for virtual file system (file uploads, user files), localStorage for settings persistence
- **Session Storage**: In-memory storage for user authentication state

### Authentication Mechanisms
- **PIN Lock**: 6-digit numeric PIN authentication
- **Password Lock**: Traditional password authentication
- **Windows Hello**: Face recognition using face-api.js with client-side model loading and server-side verification
- **Guest Mode**: Optional bypass for unauthenticated access

### Key Design Patterns
- **Context Providers**: Wrap the app in providers for file system access and system settings
- **Virtual File System**: IndexedDB-backed file storage with folder hierarchy support
- **Window Management**: Z-index based focus management with draggable, resizable windows
- **PWA Support**: Service worker for offline caching, manifest for installability

## External Dependencies

### Database
- **PostgreSQL**: Primary database, connected via `DATABASE_URL` environment variable
- **Neon Serverless**: PostgreSQL driver optimized for serverless environments with WebSocket support

### ORM & Schema
- **Drizzle ORM**: Type-safe database queries and schema management
- **Drizzle Kit**: Database migration and push tooling

### Third-Party Services
- **No external APIs required**: The app is self-contained; face recognition models are served locally from `/public/models/`

### Key NPM Dependencies
- **@tanstack/react-query**: Server state management
- **framer-motion**: Animation library
- **face-api.js**: Client-side face detection and recognition
- **lucide-react**: Icon library
- **wouter**: Lightweight router
- **zod**: Schema validation

### Deployment Targets
- **Replit**: Pre-configured with Vite dev server on port 5000
- **Vercel**: Configuration in `vercel.json` for serverless deployment
- **Standalone**: Can run independently with Node.js and PostgreSQL