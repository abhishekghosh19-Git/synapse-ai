# SynapseAI - Self-Evolving Autonomous Agent Platform

## Overview

SynapseAI is an advanced AI agent platform that enables users to interact with multiple AI models, apply sophisticated prompt engineering techniques, and generate complete applications through natural language. The platform integrates multiple AI providers (Google Gemini, OpenAI, Groq) with free-tier API access, features a comprehensive prompt technique library with 25+ methods, and provides live code generation with real-time previews.

The application is built as a full-stack TypeScript platform with a React frontend and Express backend, emphasizing self-evolving AI capabilities, context compression, and intelligent reasoning visualization.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React 18 with TypeScript, bundled via Vite

**UI System**: Material Design 3 adaptation using shadcn/ui components built on Radix UI primitives. The design system implements:
- Fibonacci-based spacing scale (2, 3, 5, 8, 13, 21px units) for consistent rhythm
- Custom typography hierarchy: Inter for UI text, JetBrains Mono for code displays
- Golden ratio-inspired layout proportions
- Three-column desktop layout: Sidebar (280px) | Main Chat (flex-1) | Inspector Panel (360px)

**State Management**: 
- TanStack Query (React Query) for server state synchronization
- Local React state for UI interactions
- Context API for theme management (light/dark mode)

**Routing**: Wouter for lightweight client-side routing

**Key Frontend Components**:
- `ChatArea`: Main conversation interface with message history, typing indicators, and context compression visualization
- `AppSidebar`: Session management, model selection, language switching, and prompt technique library access
- `InspectorPanel`: Real-time reasoning tree visualization, performance metrics, and meta-learning settings
- `CodeEditor`: Multi-file code editing with syntax awareness
- `LivePreview`: Responsive iframe preview with device mode switching
- `AgentBuilder`: Visual agent configuration with capability toggles
- `PromptTechniqueLibrary`: 25+ categorized techniques (Chain of Thought, ReAct, Tree of Thoughts, RAG, etc.)

### Backend Architecture

**Framework**: Express.js with TypeScript

**API Design**: RESTful endpoints for:
- Session management (`/api/sessions`)
- Message persistence (`/api/messages`)
- AI model interactions (chat, code generation)
- System status checks

**AI Service Layer** (`server/ai.ts`):
- Multi-provider abstraction supporting Gemini, OpenAI, and Groq APIs
- Model configuration registry mapping model IDs to providers
- Unified chat interface handling context, system prompts, and technique application
- Code generation with multi-file output structure

**Storage Layer** (`server/storage.ts`):
- Interface-based design (`IStorage`) enabling swappable backends
- In-memory implementation (`MemStorage`) using Maps for development
- Schema designed for PostgreSQL with Drizzle ORM
- Entities: Users, Sessions, Messages, GeneratedFiles, Agents

**Build System**:
- Development: Vite dev server with HMR over HTTP
- Production: esbuild bundles server, Vite builds client to `dist/public`
- Server dependencies selectively bundled to reduce syscall overhead

### Data Storage Solutions

**ORM**: Drizzle ORM with PostgreSQL dialect

**Database Provider**: Neon serverless PostgreSQL (via `@neondatabase/serverless`)

**Schema Design** (`shared/schema.ts`):
- `users`: Authentication (username/password)
- `sessions`: Conversation history with metadata (title, preview, model, timestamps)
- `messages`: Chat messages with role, content, token counts, compression ratios, applied techniques
- `generatedFiles`: Code artifacts with version history (sessionId, name, language, content, version numbers)
- `agents`: Autonomous agent configurations with capabilities stored as JSONB

**Migration Strategy**: Drizzle Kit with migrations output to `./migrations` directory

### Authentication and Authorization

**Current State**: Basic schema supports username/password authentication, but no active session management is implemented in the codebase. The application currently operates without user authentication requirements.

**Designed Infrastructure** (not yet active):
- User table with hashed passwords
- Session-based architecture implied by storage interface
- No JWT or OAuth integrations present

## External Dependencies

### AI Model Providers

**Google Gemini** (`@google/genai`):
- Gemini 2.5 Flash model
- Free tier: 1M token context, 1,500 requests/day
- API key: `GEMINI_API_KEY` environment variable

**Groq**:
- Llama 3.3 70B model via OpenAI-compatible API
- Free tier with ultra-fast inference
- Endpoint: `https://api.groq.com/openai/v1`
- API key: `GROQ_API_KEY` environment variable

**OpenAI** (`openai`):
- GPT-4o model access (paid tier)
- API key: `OPENAI_API_KEY` environment variable

**OpenRouter**:
- DeepSeek V3 and other models
- Cost-efficient routing

### Database and Storage

**Neon Serverless PostgreSQL** (`@neondatabase/serverless`):
- Serverless PostgreSQL with WebSocket connections
- Connection string: `DATABASE_URL` environment variable
- Automatic connection pooling

**Drizzle ORM** (`drizzle-orm`, `drizzle-zod`):
- Type-safe SQL query builder
- Zod schema integration for runtime validation
- Migration management via `drizzle-kit`

### UI Component Libraries

**Radix UI**: Comprehensive set of unstyled, accessible primitives:
- Dialogs, Dropdowns, Popovers, Tooltips
- Accordions, Tabs, Scrollable areas
- Form controls (Select, Checkbox, Switch, Slider)

**shadcn/ui**: Pre-styled Radix components with Tailwind CSS integration

**Styling**:
- Tailwind CSS for utility-first styling
- Custom design tokens in CSS variables
- `class-variance-authority` for component variants
- PostCSS with Autoprefixer

### Development Tools

**Build Tooling**:
- Vite 5.x for frontend bundling and dev server
- esbuild for production server bundling
- tsx for development TypeScript execution

**Replit Integration**:
- `@replit/vite-plugin-runtime-error-modal`: Error overlay
- `@replit/vite-plugin-cartographer`: Code navigation
- `@replit/vite-plugin-dev-banner`: Development mode indicator

### Utility Libraries

- `wouter`: Lightweight routing (~1.2KB)
- `date-fns`: Date manipulation and formatting
- `nanoid`: Unique ID generation
- `clsx` + `tailwind-merge`: Conditional class name composition
- `zod`: Runtime type validation and schema definition

### Session Management (Planned)

**Dependencies Present** (not yet implemented):
- `express-session`: Session middleware
- `connect-pg-simple`: PostgreSQL session store
- `memorystore`: In-memory session fallback