# Plan — Hello Hono

This plan outlines the specific steps to implement the base Hono server setup with a minimal server-rendered home page.

## Task Group 1: Dependency Setup & Server Initialization
1. Install Hono dependencies:
   - Production dependencies: `hono`, `@hono/node-server`
   - Development dependencies: `tsx`, `typescript`, `@types/node`
2. Initialize Hono entry point at `src/index.ts`:
   - Import `Hono` from `hono`
   - Import `serve` from `@hono/node-server`
   - Instantiate the app: `const app = new Hono()`
   - Set up the server listener:
     ```typescript
     serve({
       fetch: app.fetch,
       port: 3000
     }, (info) => {
       console.log(`Server is running on http://localhost:${info.port}`)
     })
     ```

## Task Group 2: Configure Hono JSX & Shared Layout
1. Configure `tsconfig.json` to support JSX:
   - Ensure `"jsx": "react-jsx"` and `"jsxImportSource": "hono/jsx"` are set in `compilerOptions`.
2. Create a layout component (e.g., `src/layout.tsx`):
   - Define a functional component `Layout` accepting `title` and `children`.
   - Render basic HTML structure (`<!DOCTYPE html>`, `<html>`, `<head>`, `<body>`).
   - Add a basic stylesheet link or placeholder style tag.

## Task Group 3: Implement Home Page Route
1. Create the home page component (e.g., `src/home.tsx` or directly in `src/index.ts`):
   - Define a `Home` component returning the home page JSX structure.
   - Include heading `<h1>AgentClinic</h1>`, subheading "A safe haven and dedicated sanctuary for weary AI agents", and status "AgentClinic is open for business ✨".
2. Define the root route `/` in `src/index.ts`:
   - Set up a GET request handler on `/` returning the `Home` page wrapped in `Layout`.
   - Return the rendered template via Hono's `c.html()` method.

## Task Group 4: Configure Scripts & Run Server
1. Update `package.json` scripts:
   - Add `"dev": "tsx watch src/index.ts"` to run the hot-reloading development server.
   - Add `"start": "tsx src/index.ts"` to run the server.
2. Launch the development server to verify everything compiles and boots correctly.

## Task Group 5: Automated Testing Configuration
1. Install Vitest development dependencies:
   - Run `npm install -D vitest`
2. Add a test script in `package.json`:
   - `"test": "vitest run"`
3. Create a test file `src/index.test.ts` to assert:
   - A GET request to `/` returns status `200`
   - Response header `Content-Type` is `text/html`
   - Response body contains the text `"AgentClinic"` and `"open for business"`
