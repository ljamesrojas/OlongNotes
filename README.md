# OlongNotes

**A free, community-driven notes repository for students in Olongapo City.**

OlongNotes lets students upload, organize, and browse class notes and reviewers by school, grade level, and subject — so a graduating student's notes don't disappear the moment they leave, and instead become a resource for the students who come after them.

> Built by BSIT 2 students as a hackathon MVP. This repository covers **Phase 1: the Notes Repository** — upload, organize, browse. Peer Q&A, tutor-matching, and competition team-finding are documented as roadmap, not shipped here (see [Roadmap](#roadmap)).

---

## Table of Contents

- [The Problem](#the-problem)
- [The Vision](#the-vision)
- [MVP Scope](#mvp-scope)
- [Out of Scope (for now)](#out-of-scope-for-now)
- [Tech Stack](#tech-stack)
- [User Tiers](#user-tiers)
- [Principles](#principles)
- [Content Moderation](#content-moderation)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Roadmap](#roadmap)
- [Our Strategy](#our-strategy-advocacy-and-validation-before-scale)
- [Contributing](#contributing)
- [License](#license)

---

## The Problem

Olongapo City schools face structural challenges that a single classroom can't fix alone:

- **Teacher-subject mismatch** — teachers are sometimes assigned subjects outside their specialization due to staffing shortages.
- **Mass promotion and learning gaps** — students advance without fully mastering the prior grade level, and gaps compound over time.
- **Declining foundational proficiencies** — core skills like reading comprehension and numeracy show measurable decline in national and international assessments.
- **Digital divide and limited EdTech integration** — many schools still rely on physical, one-time handouts with no central place to preserve or share materials beyond a single classroom or school year.
- **Grey literature loss** — reviewers, annotated notes, and capstone projects are real intellectual output that falls outside formal publishing, so nothing automatically preserves them.

A notes-sharing platform doesn't fix teacher staffing policy or replace foundational literacy instruction. What it *can* do is give students an always-available layer of peer-created academic support, written by people who recently sat in the same seat, same subject, same school. That's a real, currently missing resource — even if it isn't a complete solution on its own.

DepEd already runs a national attempt at this (LRMDS / the LR Portal, plus a separate OER initiative), and India's DIKSHA platform is a useful international parallel — a national repository that sources a large share of its content from schools and individual teachers, and grows state by state. We treat these as validation, not discouragement: DepEd's own system requires a DepEd email just to access some resources, which keeps it largely invisible to ordinary students. OlongNotes is the ground-level version, starting local.

## The Vision

Picture a senior high school student in Olongapo finishing their STEM track. Over two years they've built a dozen reviewers, summarized notes, and study guides tested against real exams. Today, when they graduate, all of that usually leaves with them — a closed group chat, a personal Drive folder, or the trash.

OlongNotes keeps that knowledge searchable by school, grade level, and subject, so the next batch of students at the same school, in the same subject, benefits from work that's already been done. Over time, every school in Olongapo builds its own living, growing academic archive, maintained by its own students.

## MVP Scope

The prototype focuses on one core loop: **upload, organize, browse.**

- **Two ways to participate** — anyone can browse freely with no account needed; creating an account unlocks uploading.
- **Upload by category** — contributors tag uploads by school, grade level, and subject before posting.
- **Accepted formats** — PDF, Word, Excel, and image files, hosted directly on the platform (not linked externally), so content stays available and moderable over time.
- **The Reviewer Zone** — the core browsing experience: filter by school, grade level, and subject to find relevant notes, archived and searchable at city scale.
- **Contributor annotations** — contributors can leave short notes alongside their own uploads explaining context, common mistakes, or what a teacher emphasized.

### Out of Scope (for now)

- No buying or selling of notes or answers, of any kind.
- No peer Q&A / live answering yet (Phase 2).
- No tutor-matching yet (Phase 3).
- No competition/team-finding yet (Phase 4).

We'd rather ship one feature that works clearly than four that are each half-finished. The rest of the vision is documented in the [Roadmap](#roadmap) — not abandoned, just sequenced.

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, Vanilla JavaScript |
| Backend | Node.js + Express.js |
| Database | Supabase (PostgreSQL) |
| File Storage | Supabase Storage (images, documents, uploads) |

## User Tiers

Access is based on **affiliation, not age** — we don't collect government ID.

| Tier | Who | What They Can Do / How Verified |
|---|---|---|
| **Tier 1 — Browser** | Any student, no account | Search and read notes/reviewers by school, grade, and subject. No verification needed. |
| **Tier 2 — Verified Contributor** | Students with a school-issued email | Upload, tag, and annotate immediately. School email confirms real affiliation without collecting government ID or age data. |
| **Tier 3 — Unverified Contributor** | Students without a school email | Can still upload; content is held for manual moderator approval before it goes live. |
| **Teacher** *(future)* | Verified educators | Upload legacy curriculum material at their own discretion; flag outdated info. |

## Principles

Constraints we're designing the system around, not marketing lines:

- **Always free.** No paywalls, no selling of notes or answers.
- **Usernames, not real names.** Public profiles show a username only. No government ID, no requirement to disclose real identity publicly.
- **School is a filter, not a requirement.** Selecting a school helps a user find relevant content faster — it's optional and never shown on a public profile.
- **Hosted, not linked.** We don't accept Google Drive links or other externally-hosted content as primary uploads. A link can be silently changed or deleted after approval; a hosted file can't.
- **Age-aware by design.** We're setting an initial account age floor and treat this as a sequencing decision, not a permanent limitation — moderation capacity needs to scale before access does.

## Content Moderation

Every upload goes through automated pre-screening before going live, followed by human review for anything ambiguous:

- **Computer vision** — flags likely faces, handwriting, or ID-like content in scanned images (a first pass for PII).
- **OCR + text matching** — extracts text from uploads and checks it against known copyrighted material to catch obvious infringement.
- **Perspective API** — applied to annotations and comments to catch toxic or harassing language.
- **Student-led moderation team** — reviews anything flagged automatically or reported by users.
- **Reactive reporting system** — lets any user or educator trigger a takedown request at any time.

**Duplicates:** exact duplicates are caught automatically via file hash comparison. Near-duplicates (same content, reformatted) rely on community upvoting to surface the best version and moderator review to merge obvious cases — automated near-duplicate detection is a roadmap item, not an MVP claim.

**Accessibility:** the platform is designed for lightweight, low-bandwidth use on entry-level Android phones, with offline file saving and compressed previews to reduce data cost.

## Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) (LTS recommended)
- A [Supabase](https://supabase.com/) project (for PostgreSQL + Storage)

### Installation

```bash
# Clone the repository
git clone https://github.com/<your-org>/olongnotes.git
cd olongnotes

# Install dependencies
npm install
```

### Environment Variables

Create a `.env` file in the project root:

```env
SUPABASE_URL=your-supabase-project-url
SUPABASE_ANON_KEY=your-supabase-anon-key
SUPABASE_SERVICE_ROLE_KEY=your-supabase-service-role-key
PORT=3000
```

### Running Locally

```bash
npm run dev
```

The app will be available at `http://localhost:3000`.

## Project Structure

```
olongnotes/
├── public/            # Static frontend assets (HTML, CSS, JS)
│   ├── css/
│   ├── js/
│   └── img/
├── server/             # Express server, routes, and API logic
├── supabase/           # SQL schema / migrations, storage policies
├── .env.example
├── package.json
└── README.md
```

*(Adjust to match your actual folder layout as the project evolves.)*

## Roadmap

| Phase | Description |
|---|---|
| **Phase 1 — Notes Repository** | Upload, browse, and organize notes/reviewers by school, grade, and subject. *(This repository.)* |
| **Phase 2 — Peer Q&A** | Students ask and answer subject-specific questions, once there's an existing user base and content to anchor trust. |
| **Phase 3 — Tutor Connections** | Students willing to tutor become discoverable, with safeguards around pricing, identity, and parental awareness designed in before launch. |
| **Phase 4 — Team & Competition Matching** | A space to find peers for STEM/HUMSS (or other) competitions, built once the platform has an established, trusted community. |

## Our Strategy: Advocacy and Validation Before Scale

We're not positioning ourselves as the team that builds and hosts this at city or national scale. We're positioning ourselves as the team that proves the problem is real and that a working, responsible first version is possible — then hands that proof to the people (teachers, school heads, eventually DepEd offices) who actually have the resources to scale it.

1. Build and demonstrate a working, responsibly-scoped MVP for the hackathon.
2. Use the MVP to gather validation — even one real teacher willing to say, on record, that this reflects a problem they deal with.
3. Bring that validation to a real local conversation: a school principal, a division supervisor, a barangay education committee. Local first, not DepEd Central first.
4. If local buy-in exists, use it as the basis for a larger conversation with Region III or DepEd — a hoped-for outcome, but not a requirement for this project to be considered a success.

## Contributing

This project is currently maintained as a student hackathon submission. If you'd like to contribute, report a bug, or suggest a feature, please open an issue or pull request.

---

<p align="center">Knowledge shared today becomes success for tomorrow.</p>
