# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- **Development**: `pnpm dev` (uses Next.js with Turbopack)
- **Build**: `pnpm build`
- **Production**: `pnpm start`
- **Lint**: `pnpm lint` (Next.js ESLint)
- **Format**: `pnpm format` (Prettier write) and `pnpm format:check` (Prettier check)

This project uses **pnpm** as the package manager.

## Environment Setup

Required environment variables in `.env.local`:
```
LIVEKIT_API_KEY=your_livekit_api_key
LIVEKIT_API_SECRET=your_livekit_api_secret
LIVEKIT_URL=https://your-livekit-server-url
```

## Architecture Overview

This is a LiveKit Voice Agent starter built with Next.js 15 and React 19. The application provides real-time voice interaction with LiveKit Agents through a web interface.

### Core Components Structure

- **App Entry**: `components/app.tsx` - Main application wrapper with room management and session state
- **Session Management**: `components/session-view.tsx` - Active call interface with media tiles and controls
- **Welcome Screen**: `components/welcome.tsx` - Landing page with start call functionality
- **LiveKit Components**: `components/livekit/` - Custom LiveKit integrations including:
  - Agent control bar with permissions
  - Video/audio tiles
  - Chat functionality
  - Device selection

### Key Architecture Patterns

1. **Room State Management**: Uses LiveKit's Room class with React state for session control
2. **Connection Flow**: API route generates tokens → Room connects → Session starts
3. **Configuration-Driven**: `app-config.ts` controls features, branding, and UI text
4. **Component Composition**: Radix UI primitives with custom styling via Tailwind CSS

### API Routes

- `/api/connection-details` - Generates LiveKit room tokens and connection details

### Hooks

- `useConnectionDetails` - Manages LiveKit connection tokens
- `useChatAndTranscription` - Handles real-time chat and transcription
- `useDebug` - Development debugging utilities

### Configuration

The app is configured through `app-config.ts` which controls:
- Feature flags (chat input, video input, screen sharing)
- Branding (logos, colors, company name)
- UI text and behavior

### Styling

Uses Tailwind CSS v4 with shadcn/ui components and Radix UI primitives for consistent, accessible UI.