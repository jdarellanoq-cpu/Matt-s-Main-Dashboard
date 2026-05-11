# Matt's Operating System — Project Context

> Read this file first. It contains everything needed to continue building this project without re-explaining anything.

---

## What This Project Is

A personal operating system dashboard built for **Matt Sanders**, CEO of:
- **Roots VS** (parent company)
- **Waypoint** (sports travel platform — booking, VIP, fan engagement for athletic programs)
- **Longitude** (B2B/B2B2C agent enablement)
- **EcoSolutions** (operations, gold distribution, succession)

It's being built by **Daniel Arellano** (Special Project Coordinator).

The dashboard's purpose: **show Matt where his attention is needed across Motion, Slack, and email — surface bottlenecks, flag urgent items, and give him a single command center to start his day.**

It is the materialized version of a request Matt made on March 12, 2026 in Slack:

> *"I think we should create a workspace just for you and me on how we continue to improve how we work together. Think of you and I as the strategic leadership heartbeat of these companies."*

---

## The Big Picture (3 layers)

```
┌─────────────────────────────────────────────────┐
│  LAYER 3: DASHBOARD (the visible product)       │
│  → Single HTML page, hosted on Netlify          │
│  → Shows Matt: critical items, bottlenecks,     │
│    project health, NACMA goals, urgent flags,   │
│    email follow-ups, suggested replies          │
└─────────────────────────────────────────────────┘
                       ↑
┌─────────────────────────────────────────────────┐
│  LAYER 2: AI BRAIN (the analysis)               │
│  → Claude API calls via backend                 │
│  → Reads Motion + Slack + Gmail data            │
│  → Categorizes by urgency                       │
│  → Generates suggested replies                  │
│  → Cross-references items across sources        │
└─────────────────────────────────────────────────┘
                       ↑
┌─────────────────────────────────────────────────┐
│  LAYER 1: DATA SOURCES (already in production)  │
│  → Motion (projects, tasks, schedule)           │
│  → Slack (channels, DMs, urgent flags)          │
│  → Gmail (inbox, sent, threads)                 │
└─────────────────────────────────────────────────┘
```

---

## What's Built vs. What's Pending

### ✅ Built (live in `matt_operating_system.html`)
- Full visual dashboard (single HTML file)
- Aspen tree theme with custom design system
- Intro screen with rotating daily quotes
- Goals tracker (3 cards: 30 schools, NACMA, investment raise)
- "Urgent — flagged by leadership" section
- 5 reorderable tabs (drag to reorder):
  1. Needs Attention
  2. Email Follow-ups
  3. NACMA Strategy
  4. Projects
  5. On Track
- Project health view with company filter (Waypoint / Longitude / EcoSolutions)
- NACMA strategy tab with countdown, decisions, school pipeline
- Email tab with 4 urgency-based sections + filters + search
- Inline action buttons (Open in Gmail, Suggested reply, Snooze)
- Auto-archive prompt for stale leads
- Focus mode toggle ("show top 3 only")
- Core values section (The Roots)
- Floating leaves animation
- Make.com + Claude pipeline for auto-creating Motion tasks from meetings (Daniel built this separately, ready to test)

### ⏳ Pending (the connections)
- OAuth setup for Motion API
- OAuth setup for Slack API
- OAuth setup for Gmail API
- Backend service to run Claude analysis on a schedule
- Database for storing tokens + cached results
- Authentication (Matt's login to the dashboard)

---

## Tech Stack & Architecture Decisions

### Frontend
- **Single HTML file** (currently `matt_operating_system.html`)
- Vanilla JS, no framework — keeps it lightweight and easy to maintain
- Google Fonts: **Fraunces** (serif, headlines) + **Manrope** (sans, body)
- CSS custom properties for theming
- Designed for desktop-first, responsive down to mobile

### Hosting
- **Netlify** (same as Daniel's previous Waypoint dashboard at `mattsdashboard1.netlify.app`)
- HTTPS by default
- Auto-deploy from GitHub

### Recommended backend stack
- **Composio or Pipedream** for OAuth handling (Slack, Gmail, Motion). Saves ~2 days vs. building from scratch.
- **Supabase** for auth + encrypted token storage (free tier generous, handles login + DB)
- **Make.com** for scheduled Claude analysis runs (Daniel already familiar with it)
- **Anthropic API** for Claude (already in use for the meeting → task pipeline)

### Why this stack
- Frontend is decoupled from backend → can redeploy 50 times without affecting OAuth tokens
- Tokens live in Supabase, not in the HTML → secure
- Claude analysis runs on a schedule → dashboard loads fast (just reads cached results)

---

## The Aspen / Pando Metaphor

The visual identity is built around **Pando** — a 14,000-year-old aspen grove in Utah that looks like 47,000 separate trees but is actually **one organism connected underground** by a single root system.

This is the metaphor for the system:
- Above ground: separate trees (Motion, Slack, Email, three companies, many projects)
- Below ground: one connected root system (the operating system Daniel is building)

Design tokens reflect this:

```css
--bark: #F8F4EC;          /* Page background — aspen bark cream */
--bark-deep: #EFE9DA;     /* Card backgrounds */
--charcoal: #1F1B16;      /* Text + dark accents */
--charcoal-soft: #4A4339; /* Secondary text */
--charcoal-mute: #8A8377; /* Muted text */
--moss: #3D5A38;          /* "Healthy" / "On track" */
--gold: #B8842A;          /* Autumn aspen leaf — accents, "warning" */
--rust: #A04A2A;          /* "Critical" / "Blocker" */
--root: #5A4128;          /* Decorative root color */
--line: rgba(31, 27, 22, 0.12);
```

The footer signs off with: *"Pando — fed by Motion · Slack · Email"*

The intro screen rotates 14 quotes (deterministic by date) drawn from aspen wisdom and Matt's own core values.

---

## Matt's Core Values (live in "The Roots" section)

These are real values from Matt's own slide deck. Do not modify them:

1. **Neglect not the gift that is in you** — Everyone has native talent. Each person discovers it; leaders help develop it.
2. **Humility accelerates learning** — Learn from mistakes, from change, from others. Humility creates learning assets.
3. **Primacy of getting it right** — Focus on WHAT is right, not WHO is right. Outcomes over positioning.
4. **Gratitude unlocks everything** — Real gratitude makes people feel seen. Loyalty and motivation grow naturally.
5. **Failure creates learning assets** — Move at market speed. Fail. Learn aggressively. Outpace the competition.
6. **I believe in you** — Belief unlocks the human spirit. The more we believe in others, the more they believe in themselves.

---

## Real Data You Can Reference

### Goals (current state, May 2026)
- **Year goal:** 30 schools on Waypoint by EOY → currently 2 (BYU, West Virginia)
- **NACMA goal (June 8, 2026):** 3–5 schools closed → currently 3 (BYU, WV, FSU)
- **Investment raise:** SPV in progress, ~35%

### Real Motion projects (Waypoint workspace, 8 projects)
1. Governance + Strategy *(also in Longitude + EcoSolutions)*
2. Crowd Commerce *(also in Longitude + EcoSolutions)*
3. Waypoint Investment Raise *(Waypoint only)*
4. B12 Product Development & Launch *(Waypoint only)*
5. NIL Portal / Athlete Ambassador Program *(Waypoint only)*
6. Marketing Leadership Upskilling *(also in Longitude + EcoSolutions)*
7. Business Development *(also in Longitude + EcoSolutions)*
8. IAPA / Media Partnerships *(Waypoint only)*

The 4 shared projects also exist in Longitude and EcoSolutions workspaces (currently shown as placeholders awaiting connection).

### Real bottlenecks (as of May 2026)
- **Jackson Macedone (SPV):** 25 days no reply, critical
- **Big 12 / CFO Playbook:** 24 days in icebox, 0 minutes logged
- **WV Amendment Terms (Paul Coelho):** 18 days waiting
- **March invoice:** unresolved with Matt
- **Priceline vs Xeni decision:** active debate, Scott vs Spencer
- **FSU onboarding:** this week, counts toward NACMA goal
- **Julia (influencer):** brand non-compliance

### NACMA contacts (NACDA convention, June 8)
- **Nick Strah** (VP, NACMA): nstrah@nacda.com · 440-788-7473 → agenda
- **Erik Christianson** (EVP, Sponsorships): echristianson@nacda.com · 317-600-6676 → mixer sponsorship
- **Meredith Scerba** (SVP, Exhibit Hall): mscerba@nacda.com · 216-659-1781 → booths
- **Alex Cramer** (Arkansas, NACMA Board): inside contact for speaking ops

### Key people in Matt's orbit
- **Scott Stevens** — co-founder, Waypoint
- **Spencer Lee** — co-founder, Waypoint
- **Erik Mikkelsen** — Longitude
- **Cameron Brockbank** — Longitude
- **Nathan Lee** — Crowd Commerce email outreach
- **Eric (BYU)** — primary client contact, more responsive than Jared
- **Paul Coelho** — legal partner

---

## Tab Structure & Logic

Tabs are draggable (HTML5 drag-and-drop) and remember user order via state. Default order:

1. **Needs Attention** — Critical alerts (rust dot) + Bottlenecks (gold dot). Each card expandable to show suggested reply. Stats row: Critical / Bottlenecks / Moving well / Auto-scheduled.
2. **Email Follow-ups** — 4 sections by urgency: Critical → This week → Sent (waiting) → Scheduling. Filters: All / Leadership / External / Clients + search.
3. **NACMA Strategy** — Countdown banner, open decisions, school pipeline. Disappears after June 8.
4. **Projects** — Health view (NOT Kanban — Motion is source of truth). Filter pills by company. Each card shows: progress, task breakdown by status, next milestone or blocker, "Open in Motion" button.
5. **On Track** — Items moving well that don't need attention. Renamed/conceptual: things Matt has delegated and can mentally archive.

---

## Email Tab Logic (the most complex)

### 6 design principles built in
1. **Capped at 5–7 per section** with "Show more" expansion
2. **Auto-dismiss** when Matt replies in Gmail (cross-referenced with sent folder)
3. **5-day expiry** in "This week" → auto-promotes to Critical or fades
4. **Severity escalation** — emails age into higher severity automatically
5. **Focus mode** — button shows top 3 only for saturated mornings
6. **Executive summary** — when volume is high, Claude writes a brief at top: *"You have X emails. Y are critical. Z can wait."*

### How Claude classifies each email
The backend should send each email to Claude with a prompt that considers:

- **Sender priority:** Is it Scott, Spencer, an investor, an active client? → critical/high. Newsletter, LinkedIn notification? → noise (auto-filtered).
- **Content signals:** Direct question? Decision request? Mentions deadline or blocker? → bumps priority.
- **Response history:** Does Matt usually reply to this person within 24 hours? → likely important.
- **Cross-reference:** Does this email relate to a Motion task or Slack thread? → bumps priority.

### Output schema Claude should produce per email
```json
{
  "id": "gmail_thread_id",
  "section": "critical | thisweek | sent | scheduling | filtered",
  "from": "Sender name",
  "tag": "Investor | Co-founder · Waypoint | Active client | etc",
  "subject": "...",
  "snippet": "first 100 chars",
  "ai_note": "one-line reasoning shown to Matt",
  "age_days": 25,
  "escalated_from": "thisweek" | null,
  "suggested_reply": "drafted text" | null,
  "linked_motion_task_id": "..." | null,
  "linked_slack_thread_id": "..." | null
}
```

The dashboard then renders this JSON into the email tab structure.

---

## Connector Setup (when ready)

### OAuth flow (recommended via Composio or Pipedream)
1. Matt visits the dashboard for the first time
2. Authentication popup → Google SSO with his email
3. Three "Connect" buttons appear: Motion, Slack, Gmail
4. He clicks each, authorizes, returns to dashboard
5. Tokens stored encrypted in Supabase, scoped to his account
6. Dashboard now reads live data

### Token expiration to handle
- Motion: ~1 year
- Slack: indefinite
- Gmail: ~6 months
- Build refresh logic to renew silently before expiry

### Critical: tokens NEVER live in the frontend
The HTML file calls a backend endpoint that returns already-fetched data. The token never touches the browser.

---

## Make.com + Claude Meeting Pipeline

Daniel built this separately. It runs every time a Motion meeting ends:

1. Motion AI Notetaker captures the transcript
2. Make.com webhook fires
3. Transcript sent to Claude API with prompt: *"Extract specific commitments Matt made. Distinguish from general discussion. Return as Motion tasks with proper project assignment."*
4. Claude returns structured task list
5. Make.com creates tasks in Motion via API
6. Dashboard refreshes to show new tasks

**Why this matters:** Daniel found Motion's native AI Notetaker creates fictional or unnecessary tasks. Claude is much better at understanding actual commitments. This pipeline is the difference between a useful task list and noise.

**To test:** Run one real meeting end-to-end. Verify tasks land in correct project. If yes, half the system is locked in.

---

## Phase 2 Ideas (don't build yet, mention in pitch)

### Voice assistant ("Pando voice brief")
Matt walks into office at 8 AM. Voice brief plays automatically:
> *"Good morning, Matt. Today is Thursday. You have 4 meetings. First is at 9:30 with Scott — he flagged something urgent about Priceline last night. Two things need attention before noon: Jackson is still waiting on the SPV reply, and Paul hasn't received the WV amendment terms..."*

Tech stack: ElevenLabs (~$22/mo for premium voice) + HomePod or Google Nest in office.
Build time: 3–4 days after dashboard is live.
Tactical advice: Don't pitch this on Day 1. Mention it as "Phase 2 if you're interested" so Matt asks for it himself.

### Reply directly from dashboard
Currently buttons say "Open in Gmail." With write OAuth permissions, they could say "Send" — Matt edits Claude's draft and sends without leaving the dashboard. Saves 5 minutes per email.

---

## Pre-Launch Checklist (39 items)

A separate PDF file (`operating_system_prelaunch_checklist.pdf`) has the full list of things to verify before connecting to Matt's accounts. Top categories:

- **Security & Privacy** (5 items) — most critical, do first
- **OAuth & Connections** (6 items)
- **Performance & Reliability** (5 items)
- **Make.com + Claude Pipeline** (5 items)
- **Onboarding & Maintenance** (4 items)
- **Legal & Relationship** (4 items)
- **UX & Long-Term Adoption** (4 items)
- **Monday Presentation** (6 items)

3 must-do items before the Monday May 11 demo:
1. Decide how Matt logs in to dashboard
2. Have video/screenshot backup if live demo breaks
3. Define the specific decision being requested ("approve to keep building" vs "approve to connect accounts today")

---

## Important Conventions for Anyone Editing This Code

### Don't break
- The aspen color palette (variables in `:root`)
- The intro screen logic (rotating quotes, deterministic by date)
- Tab drag-and-drop (HTML5 dragstart/dragover/drop)
- The single-HTML-file architecture (don't split into modules unless absolutely needed for maintainability)

### Default to
- Paraphrasing real Slack/email content rather than copying it (privacy)
- Adding new sections inside existing tabs rather than creating new tabs
- Filling new project cards with the placeholder pattern (`placeholder-card` class) before real data is available
- Keeping copy in English — Matt's primary language

### Watch for
- The dashboard should never feel like a Motion clone. Motion = source of truth for tasks. Dashboard = intelligence layer above Motion.
- Don't auto-create Motion tasks from the dashboard (one-way write would create dual sources of truth and chaos)
- Email actions that send messages should always have a confirmation step

---

## File Structure

```
project/
├── matt_operating_system.html          # The dashboard (single file)
├── operating_system_prelaunch_checklist.pdf  # 39-item verification list
├── PROJECT_CONTEXT.md                  # This file
└── README.md                           # Quick-start (optional)
```

---

## Quick Reference: Real Quotes to Anchor Decisions

When in doubt about a design decision, ask: *"Does this serve the goal of making Matt feel like the strategic leadership heartbeat?"*

Matt's actual words from Slack:
- March 12: *"Think of you and I as the strategic leadership heartbeat of these companies."*
- March 12: *"In that workspace would be the items in your job description where you're helping me — organize company, governance, workspace, projects, and tasks, setting up meetings and agendas, and follow ups."*
- April 28: *"You're good! I owe you some time."*
- February 13: *"Keep bugging me if you feel lost or need answers to things…"*

---

*This file is the canonical source. Keep it updated as the project evolves.*
