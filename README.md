# Repository for Reproducing a Turbopack Bug

This repository is prepared to reproduce and analyze Turbopack's behavior when using symbolic links to modules outside
the project directory.

## Repository Structure

The repository contains two folders:

1. **`next.js`** - A Next.js project that demonstrates the issue. This project references the `internal-module`.
2. **`internal-module`** - A sample module that is linked to the Next.js project. This module is used to demonstrate the
   behavior of symbolic links.

## Bug Description

- **What happens:**  
  When installing the `internal-module` using a local path (e.g., `npm install ../internal-module`), a symbolic link to
  this module inside `node-modules` is created. If the module resides outside the project directory, 
  Turbopack fails to detect it and throws an error.

- **Specific behavior:**  
  If the `internal-module` is located inside the project directory and also uses a symbolic link, the module is resolved
  correctly without errors.

## Steps to Reproduce

1. Clone this repository:
   ```bash
   git clone https://github.com/dimak-dev/turbopack-local-module-symlink-bug.git
   cd turbopack-local-module-symlink-bug
   ```
2. Navigate to the `next.js` directory:
   ```bash
   cd next.js
   ```
3. Start the Next.js development server using Turbopack:
   ```bash
   npm run dev:turbo
   ```
4. Observe the error indicating that Turbopack cannot resolve the `internal-module` (Build Error: Module not found: Can't resolve 'internal-module').

> **Note:** If you run `npm run dev:webpack`, where Turbopack support is disabled, no issues occur.

## Expected Behavior

- Turbopack should correctly resolve modules linked via symbolic links, even if those modules reside outside the project
  directory.

## Current Behavior

- Turbopack throws an error when attempting to resolve the `internal-module` if it is located outside the project
  directory.

## Repository Purpose

The purpose of this repository is to reproduce and investigate this behavior in Turbopack, allowing for further
debugging and facilitating communication with the Turbopack development team.


