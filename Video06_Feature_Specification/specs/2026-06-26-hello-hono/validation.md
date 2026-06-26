# Validation — Hello Hono

This document outlines the validation criteria required to verify that Phase 1 (Hello Hono) is successfully implemented with a server-rendered home page.

## Automated Verification

### 1. Test Suite Pass
- Running `npm run test` must execute the Vitest suite successfully with zero failures.
- The unit test in `src/index.test.ts` must explicitly request `/` from the application's handler and verify:
  - Response status code is `200`
  - Response `Content-Type` header starts with `text/html`
  - Response body contains the main heading `"<h1>AgentClinic</h1>"`
  - Response body contains the welcoming status text: `"AgentClinic is open for business ✨"`

### 2. TypeScript & JSX Compile Check
- Running TypeScript compiler `npx tsc --noEmit` must report zero compilation errors.
- The compilation check confirms Hono JSX configuration in `tsconfig.json` is properly configured under compiler options.

---

## Manual Verification

### 1. Boot Verification
- Start the server using the dev runner script:
  ```bash
  npm run dev
  ```
- The console output must show that the server has started and is listening on port 3000:
  ```text
  Server is running on http://localhost:3000
  ```

### 2. Request & Visual Verification
- Run a `curl` request to the server from a separate terminal window:
  ```bash
  curl -i http://localhost:3000/
  ```
- The response headers and body must match:
  ```http
  HTTP/1.1 200 OK
  Content-Type: text/html; charset=utf-8
  ```
  And contain the HTML markup for the home page.
- Open `http://localhost:3000/` in the browser and confirm the home page is displayed with:
  - The page title showing "AgentClinic"
  - The main heading `<h1>AgentClinic</h1>`
  - The tagline and status message readable on the page.
