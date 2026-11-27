# AGENTS.md: rules for any AI agent (and human) working here

This is the source for **asburycolumbus.org**, the public website of Asbury United Methodist Church in Columbus, Indiana. It's built and maintained by volunteers with AI assistants. Assume the next person to read your work has never seen this conversation, and may not be a programmer.

`CLAUDE.md` just points here. Tool-specific files should do the same, not fork these rules.

## 1. Start of every session: read these, in order

1. `docs/handoff-log.md`: the latest entries tell you what's in flight and what's next.
2. `docs/plan.md`: the site's structure, design system, content pipelines and phases.

## 2. Hard rules (stop and ask before breaking any of these)

1. **This repo is public. Never commit secrets.** API keys (Twilio, Planning Center, Google), deploy hooks, passwords and tokens go in Cloudflare's or Apps Script's secret settings, never in git, not even in a commit you delete later. Add any new variable to `.env.example` with a fake value.
2. **Never commit personal information.** No form submissions, visitor names, phone numbers, emails, member lists, giving data, or anything exported from Realm or Planning Center People. Test data uses obviously fake names (`Testy McTestface`), `example.org` emails and `555-01xx` phone numbers.
3. **Photos of people need permission, and photos of children need a parent's permission.** Don't add a photo of a recognizable child unless whoever supplied it confirms consent. Never put a child's full name next to their photo.
4. **Content comes from the ministry teams' Docs and Sheets.** Don't hard-code page text that a team owns. If a page's text is wrong, fix the source Doc, or ask its owner.
5. **Accessibility is required.** Text must meet WCAG AA contrast (for example, white text on the teal #00A7C8 fails; use dark text on teal). Every image needs alt text, and every form field needs a label.
6. **Don't break old links.** When a page moves or is removed, add a redirect.
7. **Ask before anything hard to reverse or public-facing:** DNS changes, deleting pages, adding a paid service, adding a tracking/analytics script, or changing what the Plan Your Visit form collects or texts.

## 3. How to work

- **Small changes, one branch, one PR.** Branch names: `<who>/<topic>`, for example `kevin/plan-your-visit-form`. Cloudflare builds a preview URL for every branch, so check the preview before merging. Never commit straight to `main` once the site code lands.
- **Write for visitors.** Plain, warm language, written for someone who has never been to Asbury. Follow the voice and design notes in `docs/plan.md`.
- **Keep it static and fast.** Prefer build-time data over client-side JavaScript. Add a client-side library only when a page really needs it.
- **End every session with a `docs/handoff-log.md` entry:** what changed, what's half-done, and what's next.
