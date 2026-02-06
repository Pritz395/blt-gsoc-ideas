# Project W — BLT Security Campaigns: Focused Time-Bound Security Drives (350h)

## Overview

**One line:** A campaigns system that lets small projects and founders run focused, time-bound "security drives" (e.g. 30 days of auth hardening) with curated issues, guidance, and visible progress.

**Project Type:** Single 350-hour GSoC project

**Primary Goal:** Shift BLT from passive platform ("here are your bugs") to active security partner ("let's fix auth issues together in February") — giving maintainers and founders structured, achievable security programs with social momentum and visible outcomes.

---

## Problem Statement

- **Founder Frank** (small startup founder) and **Open Source Oliver** (maintainer with limited bandwidth) cannot "do security" in the abstract; they need **focused, achievable pushes**.
- BLT is feature-oriented today; there is **no way to run a campaign** like "fix top 10 XSS issues in February" and actually see structured progress.
- Security work feels endless; time-boxed drives with clear goals create urgency and a sense of completion.

---

## Solution: Security Campaigns

Project W adds a **campaigns layer**:

1. **Campaign templates** — e.g. "Auth Hardening Sprint," "CVE Fix Week," "Secure Defaults Upgrade" — each with recommended labels, scope, and simple goals.
2. **Creation wizard** — Maintainers define scope (repos/issues/labels), duration (e.g. 2–4 weeks), and a simple goal (e.g. "close at least 5 high-priority auth issues").
3. **Campaign landing page** — Contributors see what the campaign is about, a curated issue list, and a **progress bar** (e.g. "3/10 issues resolved").
4. **Progress tracking** — Issues opened/closed during the campaign; goal completion calculated.
5. **Recap generator** — End-of-campaign summary (what got fixed, what remains); exportable as Markdown for GitHub Discussions or blog posts.

Optional: light integration with Project B (extra recognition for campaign contributions). Works with **basic issues/labels**; enhanced by A/B if present.

---

## Relationship to Other Projects

| Project   | Relationship to W                                                                                                                                 |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| **E**     | E = PR readiness (per-PR, after creation). W = program-level orchestration across many issues over time. No overlap.                             |
| **H**     | H = personal growth and "what to work on next" for contributors. W = maintainer/org-driven, time-boxed initiatives. Complementary.             |
| **B**     | W does not implement rewards; optional stretch: campaign-specific recognition via B. B remains the rewards engine.                               |
| **A / M** | W orchestrates work; it can surface issues that come from A/G/M. Does not do detection or remediation logic.                                      |

---

## Technical Approach

### Core components

- **Campaign model** — Status (draft, active, completed), scope (repos, labels, issue query), duration, goal (e.g. numeric target), timestamps.
- **Template system** — 3–5 predefined templates (Auth Hardening, CVE Fix Week, Secure Defaults / Dependency Upgrade) with recommended labels and goal patterns.
- **Creation wizard** — Maintainer-facing UI: select repos/labels, set duration and goal, preview campaign.
- **Contributor view** — Campaign landing page: description, curated issue list, progress bar, link to contribute.
- **Progress tracking** — Snapshot or poll issue state during campaign; compute progress toward goal.
- **Recap generator** — Markdown export: issues closed, goal met or not, suggested follow-up.

### Scope (350h) — indicative

| Component           | Description                                              | Hours (approx) |
| ------------------- | -------------------------------------------------------- | -------------- |
| Campaign model & DB | Campaign model, status, issue/label associations         | 25–35          |
| Template system     | 3–5 templates (Auth, CVE Fix, Secure Defaults, etc.)     | 40–50          |
| Creation wizard     | Maintainer UI: scope, goal, duration, preview             | 50–60          |
| Contributor view    | Landing page, issue list, progress bar                    | 40–50          |
| Progress tracking   | Issue state during campaign, goal calculation            | 35–45          |
| Recap generator     | End-of-campaign summary, Markdown export                 | 30–40          |
| Optional B hook     | Light recognition for campaign contributions (stretch)   | 15–20          |
| API                 | REST: list/create/update campaigns, get progress         | 25–35          |
| Tests & docs        | Unit/integration tests, API docs                          | 50–60          |

**Total:** ~330–395h; aim for lower end to stay within 350h.

### Minimum viable scope (if behind schedule)

- Campaign model with status (draft, active, completed).
- 3 core templates: Auth Hardening, CVE Fix Week, Dependency Upgrade.
- Basic creation wizard (repos, labels, duration, goal).
- Contributor landing page with issue list and progress bar.
- Progress tracking (count opened/closed during campaign).
- Simple Markdown recap generator.
- REST API (GET campaigns, POST create, PATCH update progress).
- Tests (e.g. 80%+ coverage target).

### Out of scope (explicit)

- Real-time progress via WebSockets (stretch).
- Full B integration (stretch).
- Chart visualizations in recap (text/Markdown first).

---

## Success Metrics

- Maintainers can create and publish a campaign in under 10 minutes.
- Contributors see a clear campaign goal and progress (e.g. X/Y issues).
- At least one end-to-end campaign (draft → active → completed → recap) runs successfully with fixture or real data.
- Recap is usable for a GitHub Discussion or blog post with no manual editing.

---

## Risks & Mitigations

| Risk                 | Mitigation                                              |
| -------------------- | ------------------------------------------------------- |
| Low campaign uptake  | Ship with 2–3 strong templates; document in README.      |
| Scope creep          | Strict MVP: 3 templates, no B dependency, no WebSockets. |
| Thin data            | Design for labels + issue list; works with fixtures.    |

---

## Why This Project Matters

1. **Discussion #5495 alignment** — "Helping small OSS projects and early-stage founders"; campaigns give them a structured approach.
2. **Programs, not just tools** — BLT becomes an active security partner: "Let's fix auth issues together in February."
3. **Narrative for leaders** — "We ran 3 successful security campaigns this year" is a marketable outcome.
4. **Lightweight dependencies** — Works with issues/labels; A/B enhance but are not required.

---

| Component        | Notes                                                                 |
| ---------------- | --------------------------------------------------------------------- |
| **Issues/labels**| Campaigns scope by repo + labels; no new detection.                   |
| **Project B**    | Optional: campaign contributions can feed into B for recognition.    |
| **Project E**    | Campaigns organize work across many PRs; E focuses on single-PR readiness. |
