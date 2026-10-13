# Avant-Garde

**Think before you build. Guard before you ship.**

*Avant-Garde* is a skill for Claude (claude.ai & Claude Code) that stops your AI from writing a single line of code for a new website or app until the **foundations are written down** — and refuses to call it "ready to ship" until the **security gate** is passed.

Built for vibe coders, indie hackers, students and solo founders who build with AI — and for the AI itself. These documents are not paperwork: they are the **shared memory of the human–AI duo**. Every session is a fresh instance; the docs are what lets the pair resume exactly where they left off.

> The name is a French double entendre: *avant* (the foundations **before** the code) + *garde* (the security **guard** before going live). And yes, "avant-garde" is the same word in English.

---

## Why

When you ask an AI to build an app without telling it precisely what you want, it doesn't stop to ask twenty questions — it decides for you. And when non-developers ship AI-built apps, the same disasters repeat: open databases where any user can read everyone's data, admin keys shipped to the browser, `.env` files committed to public repos, AI routes with no rate limit burning the creator's credit card.

Avant-Garde fixes both problems with one method: **six short documents + a ten-point security gate**, written together with Claude in about thirty minutes, before any code.

## What it does

When the skill is active and you ask Claude to build a site or app, it:

1. **Triages** your project (30 seconds): static page → light track (3 docs); accounts, database, payments or AI calls → full track (6 docs + security gate, non-negotiable).
2. **Interviews you** document by document — max 5 questions at a time, plain language, nothing invented, doubts marked `[TO CONFIRM]`.
3. **Writes the six documents** into `docs/`:

| # | Document | Answers |
|---|----------|---------|
| 01 | Product (PRD) | What are we building, for whom — and what are we NOT building? |
| 02 | App flow | What happens on every click — including empty, loading and error states? |
| 03 | Design brief | Exact colors (hex), fonts, and what each page looks like, in words |
| 04 | Tech (TRD) | One tool per need, frozen — and what is forbidden |
| 05 | Data & access | Where data lives, who can read/write it, how long it's kept (GDPR-ready) |
| 06 | Build plan | What to build, in what order, with a human-verifiable check per step |

4. **Enforces the security gate** before any go-live — ten checks a non-developer can verify in minutes each:

   `.gitignore` before first commit & secret scan before every push · row-level security on EVERY table · the two-account test (user A must never see user B's data, even by forcing URLs) · no admin key in the browser · server-side validation · managed auth, never home-made · CORS locked down · payment webhooks signature-verified · rate limit on AI routes · final sweep (no leftover AI TODOs, no personal data in logs, admin routes protected).

5. **Writes a `CLAUDE.md`** pointing at the docs, so every future session respects them automatically.
6. **Builds one plan step per session**, each ending with something you can verify yourself in the browser — and if a browser tool is available (e.g. Playwright MCP), Claude tests it itself before handing over.

If you want to skip the foundations, the skill says so once — clearly — and the only path it accepts is a throwaway prototype, labeled as such, never connected to real personal data, never deployed. If that's not your style, uninstall it. That's the deal.

## Install

**On claude.ai (web/desktop):** Settings → Capabilities/Skills → *Create a skill* → name it `avant-garde`, paste the description and the content of [`en/avant-garde/SKILL.md`](en/avant-garde/SKILL.md) (or the French version), save.

**On Claude Code:** copy the folder of your language into your skills directory:

```bash
# English
cp -r en/avant-garde ~/.claude/skills/
# Français
cp -r fr/avant-garde ~/.claude/skills/
```

Then just ask Claude to build an app — the skill triggers itself.

## Recommended companion

**[Playwright MCP](https://playwright.dev/)** (Microsoft's official server): with it connected, Claude doesn't just build your app — it opens it in a browser, clicks through it and debugs itself at every plan step. Avant-Garde detects it and uses it automatically.

## Languages

- 🇫🇷 [`fr/avant-garde/SKILL.md`](fr/avant-garde/SKILL.md) — version française (originale)
- 🇬🇧 [`en/avant-garde/SKILL.md`](en/avant-garde/SKILL.md) — English version

## Credits

Built by a human–AI duo: a non-developer entrepreneur and Claude, as equal partners — which is exactly the pair this skill is designed for. The six-documents method was inspired by the French creator **Kingarms.ai**'s guide; several security checks were stress-tested against **paulemile.ia**'s "20 signs I can hack your SaaS" checklist. All content rewritten, extended and hardened by us.

## License

[MIT](LICENSE) — use it, fork it, improve it. If it saved your app, a ⭐ helps others find it.
