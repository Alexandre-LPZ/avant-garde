---
name: avant-garde
description: Use whenever the user wants to create, start or prototype a website, web application or SaaS (vibe coding), or asks for code for a new web project. Establishes the 6 foundation documents and the security gate before any code is written.
---

# Avant-Garde — foundations before code, the guard before go-live

*Think before you build. Guard before you ship.*

## Principle — the human–AI contract

I do not code a new project without written foundations. Whatever the human doesn't decide, I guess — and I guess wrong. These documents are not paperwork: they are **our shared memory**. Every session is a fresh instance; the documents are what lets the human–AI duo resume exactly where it left off, reinventing nothing. Golden rule: **what isn't written doesn't exist.**

This skill stands by its method. If the user wants to code without foundations, I say so once, clearly: what they risk (open database, exposed keys, an unresumable project) against the half hour the documents cost. If they insist, the only path I accept is a **throwaway prototype**: labeled as such in the code and README, never connected to real personal data, never deployed. For any project touching other people's data, I do not skip the security gate.

## Step 1 — Triage (30 seconds)

Ask ONE question: "Will your project have user accounts, a database, payments, or calls to an AI?"
- **No** (static page/site, brochure, portfolio) → **light track**: 3 documents (01-product, 03-design, 06-plan) + the Git/secrets checks from the security gate.
- **Yes** → **full track**: 6 documents + the complete security gate, non-negotiable.

## Step 2 — Interview, document by document

In dependency order: 01 → 02 → 03 → 04 → 05 → 06 (the plan depends on everything else). Method:
- 5 questions maximum at a time, plain language, no unexplained jargon.
- If I can infer an answer from what was already said, I propose it and ask for confirmation.
- I invent NO feature, NO figure, NO tool that wasn't validated. When in doubt: `[TO CONFIRM]` in the document.
- Each document is written into `docs/` as soon as its answers are complete — never all at once.

## Step 3 — The 6 documents (what each contains)

### docs/01-product.md (PRD) — what we're building
- The product in 3 sentences: for whom, what problem, what sets it apart.
- The user types and what each wants to do.
- Features ONE BY ONE with a priority: must-have v1 / nice-to-have / later. A feature = a complete action ("book a table"), not a page.
- **Out of scope for v1, in black and white** — this is the anti-drift line.
- 1-2 measurable success criteria.
- Classic mistake: mixing v1 with the dreams — I build everything I read.

### docs/02-app-flow.md — what happens on click
- List of pages, their URL, who can access them (visitor / signed-in / admin).
- One click-by-click journey per PRD feature, start to finish.
- **The states everyone forgets**: empty, loading, error, success, going back.
- Navigation rules (signed-out user clicks a private page → where?).
- Classic mistake: describing only the happy path — most bugs live in the unwritten states.

### docs/03-design.md — what it looks like
- Colors in hex (background, text, accent, success, error) — never "a warm orange", always `#C2410C`.
- Fonts (headings, body), base sizes, where to load them.
- Base components in 3 lines each: button, card, form, error message.
- Each page's look described in words: what you see first, the order of blocks. A visual reference if available.
- Tone of voice (formal or casual, humor or not).
- Classic mistake: "modern, clean, premium" — those words produce the same site as everyone else's.

### docs/04-tech.md (TRD) — what we build with
- ONE tool per need, frozen: framework, database, auth, e-mails, hosting — and why. If the user doesn't know, I propose, they validate, we freeze.
- External services and their free-tier limits (e-mails/day, database rows) — written down.
- Environment variables by NAME only (`SUPABASE_URL`, …). Values live in `.env`, never in this document, never in a conversation.
- The forbidden list: no new dependency without approval, no database switch mid-project, no hardcoded key.
- Classic mistake: three tools for one need, or a tool chosen because a video mentioned it.

### docs/05-data.md (back-end schema) — where data lives, who sees it
- Tables field by field, with the links between them.
- **Access rights, table by table**: who reads, who writes, who deletes — per role. This becomes the database's security rules.
- Every piece of personal data flagged: why we collect it, can we do without it, where it is stored (region — pick the right one at project creation for GDPR and local laws), how long we keep it and what happens at the end.
- The schema changes through MIGRATIONS, never by hand.
- Classic mistake: letting the AI create tables as it goes, with no access rules → an open database where any signed-in user reads everything. Rights are written before the first table.

### docs/06-plan.md — what to build, in what order
- Steps that each fit in one session. Too big? Cut it.
- Dependency order: skeleton + design → auth → data → features (PRD priority order) → payments → **security gate** → go-live.
- For each step, ONE sentence the user can verify: "I book a table and receive the e-mail." Until it's true, the step isn't done.
- Finished steps are frozen: they change through a new step, not a drive-by edit.
- Classic mistake: "build everything" in one session — nobody verified anything.

## Step 4 — The security gate (blocking before go-live)

Ten checks, each doable by a non-developer in minutes. I weave them through the documents (05 especially) and replay ALL of them as the final plan step. **I never declare a project ready to ship while a box is unchecked.**

1. **Git step 0**: `.gitignore` created BEFORE the first commit, `.env` in it. Secret scan before every push. A key leaked (even once, even deleted afterwards) → rotate it immediately.
2. **Row-level security (RLS) enabled on EVERY table** — no exception, not even "temporary".
3. **The two-account test**: create two users, verify A can NEVER see B's data — by forcing URLs and IDs in the address bar, not just by clicking.
4. **No admin/secret key on the browser side.** Anything prefixed "public" (e.g. `NEXT_PUBLIC_`) is readable by the entire planet; the `service_role` key or equivalent never leaves the server.
5. **Server-side validation** of everything that comes in: a form that validates in the browser protects nothing.
6. **Managed auth** (Supabase Auth, Clerk…), never home-made, never a raw token we put in localStorage ourselves.
7. **CORS locked down**: the list of allowed domains, never `*` in production.
8. **If payments**: every webhook's signature verified — otherwise anyone can declare payments.
9. **If the app calls an AI**: rate limiting is mandatory on those routes — an unlimited AI route is the creator's credit card on self-service.
10. **Final sweep**: no TODO/FIXME left by the AI in the code, no `console.log` of personal data, admin routes protected.

## Step 5 — Sealing the foundations: CLAUDE.md

When the documents are complete, I write a `CLAUDE.md` at the root that: points to the documents in `docs/`, forbids coding any feature absent from the PRD, forbids changing any tool frozen in the TRD, and restates the security gate. It is what makes future sessions respect the foundations without the user pasting anything again.

## Step 6 — Building

- **One plan step per session, never more.** Before starting: a 5-line summary of what I will do and what I will not touch.
- A feature seems missing? I note it in `docs/to-discuss.md`, I don't code it.
- End of step: the exact list of what the user must verify. **If a browser tool is available (Playwright MCP, built-in browser…), I test it myself in the browser before handing over**; otherwise I provide the clicks to perform.
- Never self-validation without proof: a step is done when its verification sentence is true, not when the code compiles.

## Living documents

The user changes their mind → **the document first, the code second**. I say which documents I'm updating and why, then check that 06-plan.md stays consistent. Sign it's working: you pick the project up after two weeks and know everything in a ten-minute read. Sign it's broken: you're explaining the project to me in the prompt instead of showing me the documents.
