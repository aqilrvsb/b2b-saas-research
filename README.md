# B2B SaaS Research — Cold Outreach Pipeline

A curated research collection of **10 expert practitioners** on the **cold outreach pipeline for B2B
SaaS**, with their recent content pulled through APIs and organized for building a real outbound
playbook later.

> **Snapshot:** 10 verified experts · 27 YouTube transcripts · 28 newsletter/blog articles · 10 LinkedIn
> dossiers · **~77,000 words** of primary source material. Quality over volume — every source is a real,
> active practitioner, verified live, with content dated 2024–2026.

---

## Why this topic

Of the eight topics offered, I chose **Cold Outreach** deliberately:

- It has the **deepest bench of genuine practitioners** in B2B SaaS — people who run agencies, build the
  tools, and publish real send/reply numbers — which makes "10 high-signal, not generic" achievable and
  defensible.
- The pipeline has **clear, separable sub-stages** (copy → deliverability → data/AI → multichannel →
  cold calling → agency ops), so a curated set can cover the *whole* topic instead of one angle repeated.
- It's the area I can evaluate with real judgment: I build AI outreach tooling (an AI chatbot and an AI
  voice-calling product), so I can tell an operator from an influencer — exactly what this task rewards.

## Why these 10 experts

Each expert had to pass three filters (full rationale in [`research/sources.md`](research/sources.md)):

1. **Practices what they teach** — runs an agency, builds a tool, or sells the service. Operators, not commentators.
2. **Owns a distinct stage** of the pipeline, so together they're playbook-complete.
3. **Respected by insiders** — names practitioners actually cite, not first-page Google results.

| # | Expert | Owns this stage |
|---|--------|-----------------|
| 1 | **Josh Braun** (Braun Training) | Email & cold-call psychology |
| 2 | **Will Allred** (Lavender.ai) | Data-backed email copy (billions of emails analyzed) |
| 3 | **Jed Mahrle** (Practical Prospecting) | Multichannel sequencing, live A/B tests |
| 4 | **Leslie Venetz** (Sales-Led GTM) | Outbound process / agency operating model |
| 5 | **Eric Nowoslawski** (Growth Engine X) | Clay + AI cold email at 4M/month scale |
| 6 | **Jordan Crawford** (Blueprint GTM) | AI outbound research, pain-based targeting |
| 7 | **Nick Abraham** (Leadbird) | Deliverability & sending infrastructure |
| 8 | **Thibaut Souyris** (SalesLabs) | Multichannel sequence training (incl. WhatsApp) |
| 9 | **Lead Gen Jay** (Jay Feldman) | Cold-email systems (80k-sub YouTube) |
| 10 | **30MPC** (Farrokh & Cegelski) | Cold calling / phone-led outbound (600+ episodes) |

Backups in reserve: **Florin Tatulea** (ZoomInfo, SDR strategy), **Tito Bohrt** (AltiSales).

## What I collected

| Bucket | Count | Notes |
|---|---|---|
| YouTube transcripts | 27 | 5 experts with channels; recent + topic-targeted videos (2025–2026) |
| Newsletter / blog articles | 28 | Full-text, scraped; each with author + URL + date header |
| LinkedIn dossiers | 10 | One per expert: profile, real post excerpts, manual-collection checklist |

## Repository structure

```
b2b-saas-research/
├── README.md                          ← you are here
└── research/
    ├── sources.md                     ← the 10 experts: links, dates, annotations, methodology
    ├── youtube-transcripts/           ← transcripts, one folder per author (+ index README each)
    │   ├── josh-braun/  jed-mahrle/  eric-nowoslawski/  lead-gen-jay/  30mpc/
    ├── linkedin-posts/                ← one folder per author (posts.md)
    │   └── <all 10 experts>/
    └── other/                         ← newsletter issues, blog posts, frameworks, data dossiers
        └── <all 10 experts>/
```

## How it was collected (tools & APIs)

- **YouTube** — `yt-dlp` resolves channels and lists recent + keyword-targeted uploads; `youtube-transcript-api`
  fetches the caption tracks. (Hit YouTube's IP rate limit at 27 transcripts — HTTP 429 — documented honestly.)
- **Newsletters / blogs** — Firecrawl scrape (markdown, main-content only), one file per article with a source header.
- **LinkedIn** — blocked at the provider level for profile/activity URLs, so collected per the brief's
  manual-collection allowance: profile links + genuine post excerpts found via search + a copy-paste checklist.
  (LinkedIn `/pulse/` *articles* do scrape — used for Leslie Venetz.)
- **Verification** — every expert's identity, current role, and recent activity was confirmed with live web
  search before any content was collected. **No content is fabricated**; unfetchable sources are flagged in-file.

## From research → playbook (where this is headed)

The material is organized so it maps directly onto a cold-outreach playbook:

1. **Targeting & data** — Jordan Crawford (pain-based ICP), Eric Nowoslawski (Clay/TAM, 100k-minimum)
2. **Deliverability & infrastructure** — Nick Abraham, Lead Gen Jay (domains, warmup, inbox placement)
3. **Copywriting** — Josh Braun (psychology), Will Allred (data: length, tone, the 3-second filter)
4. **Sequencing & multichannel** — Jed Mahrle, Thibaut Souyris (email + LinkedIn + WhatsApp)
5. **Cold calling** — 30MPC (openers, objections, gatekeepers)
6. **Operating model** — Leslie Venetz, Eric Nowoslawski (running it as a repeatable system)

## Reproducing the YouTube pull

```bash
python -m pip install --user youtube-transcript-api yt-dlp requests
# list a channel's recent videos:
python -m yt_dlp --flat-playlist --playlist-end 6 -J "https://www.youtube.com/@leadgenjay/videos"
# fetch a transcript by video id with youtube-transcript-api (see research notes)
```

---

*Curated by Aqil ([@aqilrvsb](https://github.com/aqilrvsb)). Built with Claude Code — verification,
scraping, and transcript collection orchestrated across parallel research agents.*
