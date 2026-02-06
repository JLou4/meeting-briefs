# Meeting Briefs

**Status:** In Development
**Purpose:** Generate one-page briefing docs before meetings with startups and VCs

## Overview

When Jack has a meeting with a company or VC fund, he provides:
- Company/Fund name
- Person he's meeting with
- LinkedIn URL (optional)
- Company website URL (optional)
- Timeframe (next week, tomorrow, etc.)

I research and generate a polished one-pager with all relevant context, stored on a dedicated website with history of past briefs.

## Data Sources

| Source | Access | Use |
|--------|--------|-----|
| Crunchbase Enterprise API | API key (in secrets) | Funding, investors, company data |
| Company website | web_fetch | Product info, team, about |
| LinkedIn | User provides URL | Person background |
| X/Twitter | bird skill / web | Social presence, recent activity |
| News/Web | web_search | Recent press, announcements |
| Hacker News | API (TBD) | Discussions, launches, sentiment |

## Output

**Site:** Standalone Cloudflare Pages site (meeting-briefs.pages.dev or similar)

**Homepage:** List of past briefs as cards
- Company/Fund name
- Person met with
- Date generated
- Click to view full brief

**Brief Page:** Clean, minimal, mobile-responsive one-pager
- Source citations as superscript numbers
- Click citation to jump to sources section
- Scannable sections with clear hierarchy

## Templates

### Company Brief Sections
1. Header (name, one-liner, links, location, founded)
2. The Space (problem/market context)
3. What They're Building (product/approach)
4. Funding (rounds, amounts, investors)
5. Team (founders, key people, backgrounds)
6. Recent News
7. Competitors & Landscape
8. Sources

### VC Fund Brief Sections
1. Header (name, focus, links)
2. Fund Overview (latest fund, AUM, check size, geography)
3. Investment Thesis
4. Notable Portfolio
5. Meeting With: [Partner] (background, boards, writing/talks)
6. Reputation & Style
7. Sources

## Technical Architecture

```
meeting-briefs/
├── index.html          # Homepage with brief list
├── brief.html          # Template for individual briefs
├── briefs/             # Generated brief JSON files
│   └── 2026-02-06-company-name.json
├── scripts/
│   └── generate.js     # Brief generation logic
├── templates/
│   ├── company.html
│   └── vc.html
├── styles.css          # Clean minimal styling
└── SPEC.md
```

## Workflow

1. Jack: "I'm meeting Jane at Acme Corp tomorrow, here's their LinkedIn and website"
2. I gather data from all sources
3. Generate brief JSON
4. Render to HTML
5. Commit to repo → auto-deploys to Cloudflare Pages
6. Send Jack the link via iMessage + webchat

## Design

- Clean, minimal, professional
- Mobile-first (readable between meetings)
- Light background, good typography
- Source citations as small superscript, clickable

## Quality Bar

- All links verified working
- Facts cross-referenced where possible
- No hallucinated information
- Sources cited for all claims
- 15-minute generation time target
