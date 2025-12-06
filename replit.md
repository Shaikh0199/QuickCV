# AI Resume & Cover Letter Generator

## Overview

This is an AI-powered resume and cover letter generation platform built as a modern SaaS application. Users input their personal information, work experience, education, and skills through a multi-step form wizard, paste a job description, and receive AI-generated, tailored resume and cover letter documents. The generated documents can be edited in-browser and downloaded in multiple formats.

The application follows a productivity-focused design system inspired by Linear, Notion, and Grammarly, emphasizing clarity, efficiency, and professional credibility.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture

**Framework**: React 18 with TypeScript, built using Vite for fast development and optimized production builds.

**Routing**: Client-side routing using `wouter`, a lightweight alternative to React Router. The application has three main routes:
- `/` - Landing page with feature showcase and CTA
- `/create` - Multi-step form wizard for data collection
- `/results` - Document preview and editing interface

**State Management**: 
- **Context API** for global application state via `ResumeContext`, managing form data, generation state, template selection, and document results across the multi-step flow
- **TanStack Query (React Query)** for server state management, API calls, and async mutation handling
- Local component state with React hooks for form-specific UI state

**UI Component Library**: shadcn/ui components built on Radix UI primitives, providing accessible, customizable components following the "New York" style variant. All components use Tailwind CSS for styling with a custom design token system.

**Form Management**: React Hook Form with Zod schema validation for type-safe form handling. Validation schemas are shared between client and server via the `shared/schema.ts` module.

**Design System**:
- Typography: Inter for UI, Source Serif Pro for document previews
- Spacing: Tailwind's spacing scale (2, 4, 6, 8, 12, 16)
- Custom CSS variables for theming with light/dark mode support
- Elevation system using shadow utilities and custom `hover-elevate` classes

**Key Architectural Patterns**:
- **Multi-step wizard** with progress indication and step validation
- **Split-view editing** (60/40 layout) for document preview and editing
- **Optimistic updates** with local state before server confirmation
- **Responsive design** with mobile-first approach, collapsing split views to stacked layouts

### Backend Architecture

**Framework**: Express.js with TypeScript running on Node.js.

**API Design**: RESTful API with two primary endpoints:
- `POST /api/generate` - Accepts resume data and template preference, returns AI-generated documents
- `POST /api/download` - Converts document content to downloadable formats (PDF/DOCX)

**Build Process**: Custom build script using esbuild for server bundling and Vite for client bundling. The server build bundles specific dependencies (OpenAI, database libraries, etc.) to reduce cold start times by minimizing file system operations.

**Development Mode**: Vite dev server runs as Express middleware with HMR support. Custom Replit plugins provide runtime error overlay, cartographer, and dev banner in development.

**Rationale**: Express was chosen for its simplicity and extensive middleware ecosystem. The monorepo structure with shared TypeScript schemas ensures type safety between client and server. esbuild bundling improves production startup performance on resource-constrained environments.

### Data Architecture

**Schema Definition**: Zod schemas in `shared/schema.ts` define the shape of all data structures:
- Personal information (contact details, summary)
- Work experiences (with achievements array)
- Education entries
- Skills array
- Job description (optional, for tailoring)
- Template style selection

**Data Flow**:
1. User inputs are validated on the client using Zod schemas
2. Form data is accumulated in React Context as user progresses through steps
3. Complete dataset is sent to `/api/generate` endpoint
4. AI-generated content is stored in context and displayed in results page
5. User edits are maintained locally until download is requested

**Database**: Drizzle ORM is configured for PostgreSQL (via `drizzle.config.ts`) but appears to be provisioned for future features like user accounts, saved resumes, or generation history. Currently, the application operates statelessly with session-based data.

**Rationale**: Client-side state management reduces server complexity for the MVP. Zod provides runtime validation and TypeScript type inference from a single schema definition. Drizzle is pre-configured to enable easy addition of persistence features later.

### External Dependencies

**AI Service**: 
- **OpenAI GPT-5** (as of August 2025) for generating resume and cover letter content
- API key configured via `OPENAI_API_KEY` environment variable
- Two main generation functions:
  - `generateResume()` - Creates tailored resume based on experience and job description
  - `generateCoverLetter()` - Generates matching cover letter
- Template-specific instructions (modern/classic/minimal) guide the AI's output style

**Development Tools**:
- **Replit-specific plugins**: Vite plugins for runtime error modal, cartographer (code navigation), and dev banner (only in development)
- **TanStack Query**: Async state management and caching for API requests
- **React Hook Form + Zod**: Type-safe form handling with validation

**UI Dependencies**:
- **Radix UI**: Headless component primitives for accessibility
- **Tailwind CSS**: Utility-first styling framework
- **class-variance-authority**: Component variant management
- **Lucide React**: Icon library

**Document Handling** (Future):
- The `/api/download` endpoint suggests planned support for PDF and DOCX generation, though implementation details are not visible in provided files
- Likely requires additional libraries like `pdfkit`, `docx`, or similar

**Typography**:
- **Google Fonts**: Inter, Source Serif Pro via CDN links in `index.html`
- Additional fonts loaded: Architects Daughter, DM Sans, Fira Code, Geist Mono (visible in HTML but usage unclear)

**Session Management**:
- `connect-pg-simple` and `express-session` are listed as dependencies, indicating planned or partial implementation of session storage
- Currently no visible session usage in routes

**Rationale**: OpenAI provides state-of-the-art language generation capabilities essential for creating professional, contextually appropriate resumes and cover letters. Radix UI ensures accessibility compliance while allowing full design customization. The extensive dependency list supports a professional-grade SaaS application with plans for expanded features.