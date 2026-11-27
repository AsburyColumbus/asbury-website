# asburycolumbus.org

The website for **Asbury United Methodist Church** in Columbus, Indiana. It's being rebuilt from WordPress as a fast static site, with **Astro**, hosted on **Cloudflare**.

**Status:** planning. No site code yet. The plan is in [`docs/plan.md`](docs/plan.md), and current work is in [`docs/handoff-log.md`](docs/handoff-log.md). Target launch: before Easter 2027.

## How the site stays up to date

Ministry teams don't edit code. Each team keeps its own page text in a Google Doc, and events live in a shared Sheet or Calendar. The site pulls those in every time it builds, so a team updates its Doc and the change shows up on the next build. Structural changes (new page types, forms, layout) go through a pull request in this repo.

## Working on it

Read [`AGENTS.md`](AGENTS.md) first. It has the rules for people and AI assistants. This repo is **public**, so never commit passwords, API keys, or anyone's personal information.

Developer setup will be added here when the Astro project is created (Phase 1 in the plan).
