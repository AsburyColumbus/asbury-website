# Site plan

The technical and design plan for the new asburycolumbus.org. Planning that involves accounts, people and internal decisions is kept in the church's internal project notes, not here.

**Target launch:** before Easter, 2027-03-28.

## Goal

Move asburycolumbus.org off WordPress to **Astro + GitHub + Cloudflare**. Ministry teams keep their own content in Google Docs and Sheets, so the site doesn't depend on one person.

Why:
- The current site is 3–4 years old and due for a refresh.
- The WordPress events calendar is clunky, and the church has no real public events calendar.
- Embedded forms on WordPress are awkward to use.
- Cloudflare adds security headers (HSTS, Permissions-Policy) and a firewall that the current host doesn't.

## Stack

| Piece | Choice |
|---|---|
| Site framework | **Astro**, static output |
| Hosting | **Cloudflare** (Workers/Pages), deployed from this repo; every branch gets a preview URL |
| Content | Google Docs (one per ministry) and a Sheet or Calendar for events, pulled at build time |
| Sermon series | Planning Center Services API at build time |
| Rebuilds | Scheduled (nightly or hourly) plus a "publish now" button that calls a Cloudflare deploy hook |
| Forms | Google Forms / Apps Script web apps or a small Cloudflare Worker, built into the page (no iframes) |
| Optional editor | A Git-backed CMS (Decap or TinaCMS) if volunteers need to edit pages directly |

## Story and structure

- **A storyboard site.** The main character is the first-time visitor, and the site's main job is to lead people to **Plan Your Visit**.
- **Visitor path:** Come Worship (first visit) → Connections Breakfast with the pastor → four-week onboarding → Build Faith (small groups, Bible studies) → Love People.
- **Theme:** lean into "build" literally: *We build things: homes, faith, people.* Show real projects and people instead of generic language.
- **Hub and spoke.** Three pillar pages (Come Worship, Build Faith, Love People) tell the story and stay scannable. Only signature ministries get their own page; smaller ones are sections on a pillar page.
- **Spoke pages:** Plan Your Visit, Wednesday Family Night, Small Groups, Asbury Conservatory, Love Chapel (with the Mission Columbus story), TLM recovery partnership, Children's Morning Out.
- **Sections on pillar pages:** Pit Stop, Kids Church, Card Factory, Wednesday pickleball (under Small Groups), Faith Promise (on the Give page).
- **One next step:** announcements and sign-ups all point to `next.asburycolumbus.org`, which links to event pages tied to the public calendar.

## Home page ("Three Pillars", with a blueprint feel)

1. Header
2. Hero: "Come Worship. Build Faith. Love People." over a blueprint grid, a Plan Your Visit button, and service times
3. Three pillars:
   - **01 Come Worship** (teal): guest parking, Guest Center, Kids Church, Wednesday Family Night
   - **02 Build Faith** (orange): Connections Breakfast, small groups, Bible studies
   - **03 Love People** (red): Children's Morning Out, TLM recovery partnership, building and serving with Love Chapel
4. Wednesday Family Night band: "Dinner first. Then we grow together." 5:30 dinner (free-will donation), 6:00 studies, kids' activities and small groups
5. This week at Asbury: the current sermon series (from Planning Center) and next steps (from the calendar)
6. Plan Your Visit: "Your story starts Sunday." with a form on the page
7. Footer

## Design system

- **Font:** Mulish (Google Fonts; the brand's Muli under its current name).
- **Colors:** blue `#324873` (primary); pillar accents teal `#00A7C8`, orange `#F8961F`, red `#E53446`.
- **Buttons:** blue with white text, or teal with **dark** text (white on teal fails contrast).
- Grid lines and numbered sections give the "blueprint" feel.
- Brand basics follow Asbury's 2020 style guide, with a web addendum (accessible colors, web type styles, photo style, voice) to be written into this repo.

## Content pipelines

| Source | Feeds | How |
|---|---|---|
| Google Docs, one per ministry | Ministry page text | Pulled at build time and converted to Markdown |
| Google Sheet or Calendar | Public events calendar and event pages | Pulled at build time |
| Planning Center Services | Current sermon series and artwork | API call at build time |
| A Sheet (exported from the church database at first) | Small groups list | Pulled at build time |

- Ministry Docs use fixed headings: **Purpose, Story, When and Where, Get Involved.** The build keeps only headings, bold/italic, links, lists and simple tables. Photos go in a folder next to the Doc.
- Goal: every team maintains its own section from its own Drive folder. The web team maintains the system, not the content.

## Forms

- **Plan Your Visit:** name, mobile, which Sunday, adults and kids, kids' ages, and a texting consent checkbox. On submit it alerts the greeters and schedules welcome texts.
- **Event sign-ups** through a Forms/Sheets registration flow.
- **Room reservation request** (the current site has one): a Google Form, a free form service, or a small Cloudflare Worker that saves and emails each request.

## Phases

| Phase | What |
|---|---|
| 0 · Take stock | Domain and DNS records, crawl of the current site (every URL and PDF, for redirects) |
| 1 · Foundation | Astro project, Cloudflare deploys and branch previews, design system, page skeletons |
| 2 · Data pipelines | Docs, events, Planning Center and small groups pulled at build time; scheduled and "publish now" rebuilds |
| 3 · Funnels and forms | Plan Your Visit, `next.asburycolumbus.org`, sign-ups, room reservations |
| 4 · Content | Pillar and ministry pages along the visitor path; photos, video and stories; teams review their Docs |
| 5 · Cutover | Redirect map from every old URL, DNS to Cloudflare (keeping the email records exactly), analytics and Search Console carried over |
| 6 · Handoff | Runbook (editing a page, publishing now, fixing a failed build) and a README for the next volunteer |
