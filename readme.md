# JavaReact SSR Framework (Sparkle ✨ 💖 )

> A Next.js-inspired full-stack framework leveraging Java Spring Boot backend with React frontend, featuring file-based routing, seamless Java data injection into React components, and server-side rendering powered by GraalVM.

---

## Overview

This framework combines the robustness and performance of a JVM backend with the modern declarative UI of React. Inspired by Next.js, it enables full-stack development with:

- **File-based routing** for frontend pages and backend APIs
- **Server-Side Rendering (SSR)** of React components on JVM via GraalVM or Node.js interop
- **Java-to-React data injection**, enabling backend data to flow naturally into React components during SSR
- **Hot-reloading & unified dev experience** with integrated build tooling
- **API routes alongside page routes**, facilitating RESTful endpoints inside the same file system

---

## Key Concepts

### 1. File-Based Routing

- **`/pages` folder**: React components that correspond to frontend routes
  - `/pages/index.jsx` → `/`
  - `/pages/about.jsx` → `/about`
  - Dynamic routes: `/pages/user/[id].jsx` → `/user/:id`
- **`/api` folder**: Java controllers or endpoint definitions serving backend APIs
  - `/api/user.java` → `/api/user`
  - Support for RESTful CRUD operations with method-based routing (`GET`, `POST`, etc.)

### 2. Server-Side Rendering (SSR)

- React components in `/pages` are rendered server-side during request lifecycle.
- Uses **GraalVM’s Node.js runtime** to execute React’s `ReactDOMServer` inside JVM.
- SSR output HTML is injected with serialized Java data props.
- Fallback to client-side hydration ensures dynamic interactivity.

### 3. Java Data Injection into React Components

- Backend Java services supply data during SSR.
- Data is serialized and passed as props to React components.
- Developers define data-fetching methods on Java side that correspond to React page lifecycle hooks (similar to `getServerSideProps` in Next.js).
- This enables React components to render with real-time backend data on initial load.

### 4. Unified Build and Dev Workflow

- CLI tooling orchestrates:
  - React frontend compilation (via embedded Node.js or external build tools like Vite/webpack)
  - JVM backend compilation and Spring Boot app lifecycle
  - Watch mode for hot reload of frontend and backend
- Production build bundles optimized React assets served via Spring Boot’s static resources.

---

## Proposed File Structure

```plaintext
root/
├── api/                  # Java backend API endpoints/controllers
│   ├── UserController.java
│   └── AuthController.java
│
├── pages/                # React frontend pages (file-based routes)
│   ├── index.jsx
│   ├── about.jsx
│   └── user/
│       └── [id].jsx      # Dynamic route
│
├── components/           # Shared React UI components
│   └── Header.jsx
│
├── services/             # Java backend services/business logic
│   └── UserService.java
│
├── public/               # Static assets (images, fonts, etc.)
│
├── build/                # Build output directory
│
├── framework.config.js   # Config file for routing, SSR options, etc.
│
├── pom.xml / build.gradle # Java build files
│
└── package.json          # React and build tooling dependencies
