# Zine: Static Site Generator

Zine is a fast, scalable, and flexible Static Site Generator (SSG) written in Zig. It is designed for performance and provides a modern development experience with live reloading and advanced templating.

## Project Overview

- **Language:** Zig (Minimum version 0.15.0)
- **Markdown Engine:** [supermd](https://github.com/kristoff-it/supermd)
- **HTML Engine:** [superhtml](https://github.com/kristoff-it/superhtml)
- **Data Format:** [ziggy](https://github.com/kristoff-it/ziggy)
- **Core Architecture:**
  - `src/main.zig`: Entry point, dispatches CLI subcommands.
  - `src/root.zig`: Core logic for configuration loading, content scanning, and site building.
  - `src/worker.zig`: Handles concurrent tasks for scaling.
  - `src/cli/`: Implementation of subcommands (`init`, `release`, `debug`, `serve`).
  - `src/render/`: HTML rendering logic for Markdown content.
  - `src/context/`: Data models for Site, Page, Assets, etc., available in templates.

## Building and Running

### Development Commands

- **Build Zine:** `zig build`
- **Check Build:** `zig build check` (faster than full build, only checks the executable)
- **Run Tests:** `zig build test` (runs snapshot tests in `tests/`)
- **Run on Test Site:** `zig build run` (runs `zine` against the `standalone-test` directory)

### CLI Usage

Once built, you can use the `zine` executable (found in `zig-out/bin/`):

- **Initialize a new site:** `zine init` (optionally with `--multilingual`)
- **Start dev server:** `zine` (default command, serves on `localhost:8000`)
- **Build for release:** `zine release` (outputs to `public/` by default)
- **Version info:** `zine version`

## Development Conventions

- **Snapshot Testing:** Zine relies heavily on snapshot tests located in `tests/`. These tests compare actual output against `snapshot.txt` files to prevent regressions.
- **Strict Typing:** Uses Zig's type system extensively to ensure correctness, particularly with `ziggy` schemas for configuration and frontmatter.
- **Performance:** Designed to be multi-threaded; `worker.zig` manages parallel processing of pages.
- **Template System:** Uses `superhtml` for layouts. Templates have access to `$site`, `$page`, and custom properties defined in frontmatter.

## Key Files

- `zine.ziggy`: The main configuration file for a Zine project.
- `frontmatter.ziggy-schema`: Defines the schema for page metadata.
- `src/root.zig`: Contains the `Site` and `Config` structs which define the project structure.
- `build.zig`: Defines the build process and test runners.
