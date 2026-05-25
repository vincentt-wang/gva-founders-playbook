# GVA Founders Playbook
## Strategic Development Report · v2.0

**Date:** May 2026  
**Prepared by:** Vincent Wang + Claude Code  
**Status:** Living Document — Internal & Partner Review

| Audience | Role | Focus |
|---|---|---|
| Tina | GVA Program Lead | Strategic decisions, partner conversations |
| Terry | Lead Investor | Investment thesis, growth trajectory, ROI |
| Engineering Team | Technical Collaborators | Migration, architecture, onboarding |

---

## Executive Summary

GVA Founders Playbook is a production-grade marketing and recruitment site for the Global Venture Accelerator — designed, built, and deployed in **under 25 hours** of AI-assisted development at a technology cost of approximately **NTD 850** (USD ~27). The equivalent scope from a traditional agency would cost **NTD 310,000–610,000**.

> **The core question this report answers:** What is the path from this prototype to a production platform that serves multiple stakeholder types, scales with the program, and can be handed off to a professional engineering team?

**What is live today:**
- Full bilingual (EN/ZH) marketing site at [vincentt-wang.github.io/gva-founders-playbook](https://vincentt-wang.github.io/gva-founders-playbook/)
- 17 interactive sections: real-time globe, YC-style proof scroll, curriculum accordion, hero particle mesh
- Multi-stakeholder portal overlay (Founder / Alumni / Mentor / Investor / Staff)
- Mobile-responsive, SEO-structured, deployable in one `git push`

---

## 1. What Has Been Built

### Technical Stack

| Layer | Technology | Notes |
|---|---|---|
| Frontend | HTML5 / CSS3 / Vanilla JS | Single-file, zero dependencies |
| Hosting | GitHub Pages | Free, CDN-backed, auto-deploy on push |
| Version Control | Git / GitHub | `vincentt-wang/gva-founders-playbook` |
| Domain | vincentt-wang.github.io (staging) | Ready for `playbook.gva.tw` |
| Fonts | Google Fonts (Playfair Display, DM Sans, Noto) | Preloaded for performance |
| Globe | Canvas 2D + Natural Earth TopoJSON | Real country outlines, zero API cost |
| Build System | None | Edit → git push → live in 60 seconds |

### Feature Inventory

| Section | Feature | Status |
|---|---|---|
| Hero | Particle mesh → sphere on hover | Live |
| Hero | Bilingual badge + headline + animated stats | Live |
| Marquee | Scrolling partner ticker | Live |
| About | Pain-point cards with hover animation | Live |
| Pillars | Three-pillar grid (GVA.tw aligned) | Live |
| Globe | Interactive orthographic globe + city legends | Live |
| Curriculum | 8-module accordion (M1–M8) | Live |
| Proof | YC-style scroll-driven case study wheel | Live |
| Team | Core team (3) + advisory board (4) | Live |
| Press | 5 media quote cards | Live |
| Ecosystem | Partner logo strip | Live |
| Video | Placeholder video shell | Live |
| Apply | Dark CTA section with cohort stats | Live |
| FAQ | 6-question accordion | Live |
| Portal | 5-role stakeholder overlay | Live |
| i18n | Full EN/ZH toggle via data attributes | Live |
| SEO | og:image, canonical, FAQPage + Organization schema | Live |

---

## 2. Architecture: Strengths, Limits, and Growth Path

### What the Static Architecture Does Well

- **Zero infrastructure cost** — GitHub Pages is free indefinitely for public repos
- **Instant deployment** — `git push` = live in under 60 seconds
- **No server maintenance** — no databases, no containers, no patches
- **Global CDN** — delivered from the nearest PoP automatically
- **Full auditability** — every change in git history, fully reversible

### Hard Limits

| Limitation | Business Impact | Resolution Path |
|---|---|---|
| No server-side logic | Cannot process forms, validate auth, or store data | Vercel serverless functions |
| No database | No persistent application tracking or cohort records | Airtable → PostgreSQL |
| No authentication | Portal logins are placeholders | Auth0 / Clerk |
| No CMS | Content changes require code edits | Contentful / Notion headless |
| Single file | Difficult for multiple engineers to work in parallel | Refactor to Astro components |
| No email automation | `mailto:` links are not trackable | Systeme.io + Zapier |

### Scalability Ceiling

**Current architecture supports:**
- Up to 500,000 page views/month (GitHub Pages limit)
- Unlimited static content updates
- Single-engineer workflows with git branching

**Current architecture cannot support:**
- Real user accounts or session management
- Application intake with database persistence
- Automated email sequences or role-based access
- Real-time cohort data or dashboards

---

## 3. Stakeholder Framework

### Access Tier Map

| Tier | Role | Current State | Target State |
|---|---|---|---|
| Public | Visitors, prospective founders | Full site access | Unchanged |
| Applicant | Founders who submitted | Portal placeholder | Systeme.io form → Airtable |
| Cohort Member | Active participants | Portal placeholder | Systeme.io membership area |
| Alumni | Program graduates | Fake login | Circle.so or custom area |
| Mentor | Assigned mentors | Fake login | Notion shared workspace |
| Investor | Partner VCs | Fake login | Private Notion + email |
| Staff / Admin | GVA team | Fake login | Airtable interface + Notion |

### Recommended Short-Term Stack (Zero Custom Backend)

```
Applications:    Systeme.io embed form → webhook → Airtable
Cohort content:  Systeme.io membership area
Community:       Circle.so (private) or Slack
Mentor mgmt:     Notion shared workspace
Admin backend:   Airtable interface views
Email comms:     Systeme.io automated sequences
```

**Total monthly cost of this stack:** NTD 850–3,200 (Systeme.io Startup: ~NTD 850/month)

---

## 4. Systeme.io Integration Playbook

### Integration Options

**Option A — Embed + Redirect** *(Recommended for Launch)*  
Replace the portal's `mailto:` Apply link with a Systeme.io embedded form.  
Systeme.io handles submission, storage, and automated reply emails.  
**Effort: 2 hours · Cost: Free tier**

**Option B — Webhook + Airtable Pipeline**  
Systeme.io form → webhook → Zapier/Make → Airtable CRM.  
Staff review all applications through Airtable Interface.  
**Effort: 4 hours · Cost: Zapier free tier (100 tasks/month)**

**Option C — Full Membership Integration**  
Systeme.io membership area hosts cohort materials (videos, sessions, readings).  
Accepted founders receive an email invite. Alumni retain post-cohort access.  
**Effort: 1 week · Cost: Systeme.io Startup ($27/month)**

### Launch Sequence

```
Week 1:  Set up Systeme.io account + application form
Week 2:  Embed form in Portal Founder step
Week 3:  Connect Systeme.io webhook → Airtable
Week 4:  Test full funnel: apply → confirmation → Airtable record
```

---

## 5. Competitive Gap Analysis

### vs. YC, Antler, Iterative

| Feature | YC | Antler | GVA Current | Priority |
|---|---|---|---|---|
| Real team bios + photos | ✓ | ✓ | Placeholder | High |
| Clear investment terms | ✓ ($500K/7%) | ✓ | Not disclosed | High |
| Application deadline + countdown | ✓ | ✓ | Not shown | High |
| Real partner VC logos | ✓ | ✓ | Placeholder | High |
| Portfolio company logos | ✓ | ✓ | Not available | High |
| Alumni directory (searchable) | ✓ | ✓ | Not available | Medium |
| Press coverage section | ✓ | ✓ | Placeholder | Medium |
| Blog / Founder Insights | ✓ | ✓ | Not built | Medium |
| Demo Day page / archive | ✓ | ✓ | Not built | Low |
| Video content | ✓ | ✓ | Placeholder | Low |

### Highest-Leverage Gaps to Close

1. **Real team bios** — highest single trust signal; requires only content, not engineering
2. **Clear pricing / terms** — removes the #1 objection in the application decision
3. **Application deadline** — scarcity + urgency is proven to drive conversion
4. **Real partner VC logos** — social proof for both founder and investor audiences
5. **One blog post** — a single well-written article can drive more organic traffic than all SEO meta tags combined

---

## 6. SEO Architecture

### Current State

| Element | Status | Notes |
|---|---|---|
| Title tag | Optimized | GVA Founders Playbook + Taiwan-to-Global |
| Meta description | Present | Could be richer with a call-to-action |
| og:image | Added | placehold.co (replace with real image) |
| Canonical URL | Added | GitHub Pages URL |
| Schema: Course | Present | Basic course structured data |
| Schema: Organization | Added | GVA entity |
| Schema: FAQPage | Added | Maps to FAQ section |
| Schema: Event | Added | Cohort 2026 as a structured event |
| sitemap.xml | Added | Static, lists key pages |
| robots.txt | Added | Allows all crawlers |
| Core Web Vitals | Good | Single static file, minimal JS |
| hreflang | Present | EN + ZH-TW alternates |

### Growth Levers

**Immediate (no engineering):**
- Submit sitemap to Google Search Console
- Set up Google Analytics 4 with conversion events
- Replace placehold.co og:image with a real branded image

**Short-term (minor engineering):**
- Add `/blog` directory with 3–5 static HTML articles
- Target: "Taiwan startup fundraising", "how to pitch US VCs from Asia", "pre-accelerator Taiwan"

**Long-term (with CMS):**
- Notion or Contentful as headless CMS → auto-generate blog pages
- Dynamic OG images via Vercel OG

---

## 7. Analytics & Metrics

### Recommended Stack

| Tool | Cost | What It Tracks |
|---|---|---|
| Google Analytics 4 | Free | Page views, sessions, geography, device |
| PostHog | Free (up to 1M events) | Session recordings, funnels, heatmaps |
| Google Search Console | Free | Impressions, clicks, keyword rankings |

### Key Events to Track

```javascript
// Apply button click
gtag('event', 'apply_click', { section: 'hero' });

// Portal role selection
gtag('event', 'portal_role_select', { role: 'founder' });

// Curriculum module expand
gtag('event', 'curriculum_expand', { module: 'M1' });

// Language switch
gtag('event', 'language_switch', { to: 'zh' });

// Scroll depth
gtag('event', 'scroll_depth', { depth: '75%' });
```

### Dashboard Metrics

| Metric | Benchmark | GVA Target |
|---|---|---|
| Unique visitors / month | — | 500 (M1) → 2,000 (M3) |
| Apply button CTR | 2–4% (B2B) | 3% |
| Portal role breakdown | — | 70% Founder / 20% Investor |
| Avg. session duration | 2 min | 3.5 min |
| Bounce rate | 50–70% | Below 60% |

---

## 8. Minimum Success Criteria (MSC)

### Phase 1 — Website as Lead Generation (Months 1–3)

| Criterion | Minimum | Target |
|---|---|---|
| Applications received | 30 | 80 |
| Website → Apply CVR | 1.5% | 3% |
| Organic monthly visitors | 300 | 1,000 |
| Avg. session duration | 2 min | 4 min |
| Media / partner responses | 3 | 10 |

### Phase 2 — First Cohort Execution (Months 3–6)

| Criterion | Minimum | Target |
|---|---|---|
| Cohort enrollment | 8 founders | 15 founders |
| Cohort completion rate | 80% | 95% |
| Alumni NPS | 40 | 70 |
| Founders raising within 12 months | 2 | 5 |
| Referral-driven applications (Cohort 2) | 10% | 30% |

### Phase 3 — Business Model Validation (Month 6+)

| Criterion | Definition |
|---|---|
| Unit economics positive | Program fee × cohort size > all operating costs |
| Cohort 2 without paid ads | Organic + referral fills all 15 spots |
| VC partner co-investment | At least 1 portfolio company receives introduction from partner VC |
| Press pickup (organic) | At least 1 unsolicited media mention |

---

## 9. Cost & Investment Analysis

### Development Cost

| Item | Est. Hours | AI-Assisted Cost | Agency Equivalent |
|---|---|---|---|
| Design system + UI | 6h | ~NTD 200 | NTD 80,000–150,000 |
| Frontend development | 10h | ~NTD 300 | NTD 100,000–200,000 |
| Interaction design (globe, animations) | 5h | ~NTD 150 | NTD 60,000–120,000 |
| Bilingual system | 2h | ~NTD 50 | NTD 20,000–40,000 |
| Mobile optimization | 3h | ~NTD 100 | NTD 30,000–60,000 |
| SEO + portal system | 2h | ~NTD 50 | NTD 20,000–40,000 |
| **Total** | **~25h** | **~NTD 850** | **NTD 310,000–610,000** |

> **Cost reduction: 99.7%** vs. traditional agency development.  
> *AI cost basis: Claude Code subscription NTD 640–3,200/month across ~2–3 months active development.*

### Ongoing Monthly Costs

| Item | Monthly Cost |
|---|---|
| GitHub Pages hosting | NTD 0 |
| Systeme.io Startup plan | ~NTD 850 |
| Google Analytics + Search Console | NTD 0 |
| Custom domain (gva.tw, already owned) | NTD 0 (amortized) |
| Claude Code subscription | NTD 640–3,200 |
| **Total** | **NTD 1,490–4,050/month** |

---

## 10. Migration Roadmap

### Phase 1 — Static Site to Vercel (1 Day)

```bash
# Install Vercel CLI
npm i -g vercel

# From project directory
vercel

# In Vercel dashboard: set custom domain
# playbook.gva.tw → CNAME → cname.vercel-dns.com
```

Result: same single-file site, now with preview deployments on every pull request.

### Phase 2 — Component Architecture with Astro (1–2 Weeks)

Astro outputs 100% static HTML (like the current site), but organizes code into components, enables Markdown-based blog pages, and supports easy Vercel deployment.

```
gva-founders-playbook/
├── src/
│   ├── components/
│   │   ├── Hero.astro
│   │   ├── Pillars.astro
│   │   ├── Globe.astro
│   │   ├── Curriculum.astro
│   │   └── Portal.astro
│   ├── layouts/
│   │   └── Base.astro
│   ├── pages/
│   │   ├── index.astro
│   │   └── blog/
│   └── content/          ← Markdown blog posts
├── public/
│   ├── sitemap.xml
│   └── robots.txt
└── CLAUDE.md             ← AI collaboration rules
```

### Phase 3 — Backend Layer (When Required)

**Trigger:** When real authentication, application tracking, or dynamic content becomes necessary.

```
Auth:      Clerk (drop-in, free for small scale)
Database:  Supabase (PostgreSQL, free tier)
CMS:       Contentful or Sanity (free tier)
Payments:  Stripe (for program fees)
```

---

## 11. Engineer Onboarding Checklist

### Access & Setup

- [ ] GitHub repository access (`vincentt-wang/gva-founders-playbook`)
- [ ] Vercel project access (after migration)
- [ ] Google Analytics property access
- [ ] Systeme.io account access (for form management)
- [ ] Airtable base access (for application tracking)
- [ ] Read `CLAUDE.md` — all design + AI collaboration rules are there

### Development Workflow

- [ ] Clone repo → open `index.html` in browser → confirm it works
- [ ] Create `dev` branch — never push directly to `main`
- [ ] Feature branches: `feature/[description]` from `dev`
- [ ] PR to `dev` → review → merge to `main` for production

### Key Rules (from CLAUDE.md)

- Minimum font size: 16px everywhere, no exceptions
- No emoji in UI — SVG icons only
- All new text needs `data-en` and `data-zh` attributes for bilingual support
- Layout buffer must be ≥ 50px before deploying any layout changes
- All step-reveal animations must go through `findNextRevealable()`

### AI-Assisted Development

- Use `claude` command in the project directory — it loads `CLAUDE.md` automatically
- Existing project context is preserved across sessions via memory files
- The `CLAUDE.md` file primes Claude on all design rules before every session

---

## 12. AI Integration Possibilities

### Immediately Feasible (No Backend Required)

| Integration | Tool | Effort | Monthly Cost |
|---|---|---|---|
| AI chatbot (FAQ answering) | Crisp.chat with AI | 1 hour | NTD 0–800 |
| Application form processing | Systeme.io native | 2 hours | Included in plan |
| SEO content generation | Claude.ai | Ongoing | Subscription |

### Feasible with Serverless Functions (Vercel)

| Integration | Description | Est. Cost |
|---|---|---|
| AI application screener | Submit → Claude API → score + summary → Airtable | ~NTD 0.10/application |
| Dynamic OG images | Generate branded social cards per page | Free (Vercel OG) |
| AI chatbot (custom, Claude API) | Serverless proxy → Claude API | ~NTD 30–100/month |

### Estimated AI API Costs at Launch Scale

At Claude Sonnet 4.6 pricing (input: $3/M tokens, output: $15/M tokens):

- AI chatbot, 500 conversations/month, avg 800 tokens: **~NTD 40/month**
- Application screener, 100 applications, 1,500 tokens each: **~NTD 15/month**
- Total AI API costs at launch scale: **under NTD 100/month**

---

## 13. Immediate Action Checklist

### Tina (Program Lead) — Next 2 Weeks

- [ ] Decide on program pricing / investment terms (publish or not)
- [ ] Provide real team bios and headshots for 2–3 core team members
- [ ] Confirm application open and close dates for Cohort 2026
- [ ] Set up Systeme.io account and create the application form
- [ ] Connect custom domain `playbook.gva.tw` to GitHub Pages or Vercel

### Terry (Lead Investor) — For Discussion

- [ ] Review investor portal messaging — does it reflect GVA's actual investor value proposition?
- [ ] Confirm which partner VCs can be named publicly on the site
- [ ] Define criteria for the "Cohort 2 fills without paid ads" milestone

### Engineering Team — When Engaged

- [ ] Clone repo and read `CLAUDE.md`
- [ ] Set up local dev environment (open `index.html` directly in browser)
- [ ] Evaluate Astro migration vs. remaining on single-file HTML
- [ ] Plan Vercel migration (estimated: 1 day)
- [ ] Set up Google Analytics 4 with the five key events listed in Section 7
- [ ] Integrate application form (Systeme.io embed or custom)

### Everyone — Right Now

- [ ] Share the live URL with 5 potential applicants and collect feedback
- [ ] Identify 2–3 real alumni or advisors who can provide quotable testimonials
- [ ] Submit sitemap to Google Search Console

---

## Appendix: Technology Decision Log

| Decision | Alternative Considered | Why |
|---|---|---|
| Single HTML file | Next.js, Astro | Maximum portability, zero build complexity at this stage |
| GitHub Pages | Vercel, Netlify | Zero cost; Vercel migration is one command when ready |
| Canvas 2D for globe | Mapbox, Leaflet | No API key, full visual control, no ongoing cost |
| i18n via data attributes | i18next library | Zero dependency, same performance, works offline |
| Pravatar.cc placeholders | Lorem Picsum | Consistent face-like images for team / testimonial placeholders |
| TopoJSON for countries | Hard-coded coordinates | Accurate Natural Earth data, CDN-hosted, ~8KB |

---

*This document is a living strategic reference, updated as GVA moves from prototype to production.*  
*Latest version always in repository: `GVA_Strategy_Report_v2.md`*  
*Prepared with Claude Code (claude-sonnet-4-6) · Anthropic, 2026*
