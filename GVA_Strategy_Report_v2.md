# GVA Founders Playbook — Strategic Development Report

**Version:** 2.0  
**Date:** May 2026  
**Prepared by:** Vincent Wang + Claude Code (Anthropic AI)  
**Status:** Living Document — For Internal & Partner Review

**Primary Audiences:**
- **Tina** — GVA Program Lead (strategic decisions, partner conversations)
- **Terry** — Lead Investor (investment thesis, growth trajectory, ROI)
- **Engineering Team** — Migration, architecture, collaboration protocols

---

## Executive Summary

GVA Founders Playbook is a production-grade marketing and recruitment site for the Global Venture Accelerator — designed, built, and deployed in **under 25 hours** of AI-assisted development at an estimated technology cost of **NTD 640–3,200** (USD 20–100, subscription-based). The site represents what would traditionally cost **NTD 300,000–800,000** in agency fees.

**What exists today:**
- Full bilingual (EN/ZH) marketing site, live at [vincentt-wang.github.io/gva-founders-playbook](https://vincentt-wang.github.io/gva-founders-playbook/)
- 10+ interactive sections including a real-time globe, YC-style proof scroll, and interactive curriculum
- Multi-stakeholder portal overlay (Founder / Alumni / Mentor / Investor / Staff)
- Mobile-responsive, SEO-structured, deployable in one `git push`

**The core question this report answers:** What is the path from this prototype to a production platform that can serve multiple stakeholder types, scale with the program, and be handed off to a professional engineering team?

---

## 1. What Has Been Built

### Technical Stack

| Layer | Technology | Notes |
|---|---|---|
| Frontend | HTML5 / CSS3 / Vanilla JS | Single-file, zero dependencies |
| Hosting | GitHub Pages | Free, CDN-backed, auto-deploy on push |
| Version Control | Git / GitHub | `vincentt-wang/gva-founders-playbook` |
| Domain | vincentt-wang.github.io (staging) | Ready for `playbook.gva.tw` custom domain |
| Fonts | Google Fonts (Playfair Display, DM Sans, Noto) | Preloaded for performance |
| Globe | Canvas 2D + Natural Earth 110m (TopoJSON) | Real country outlines, no map tile costs |
| Build System | None | Direct edit → git push → live |

### Feature Inventory

| Section | Feature | Status |
|---|---|---|
| Hero | Particle mesh → sphere interaction on hover | Live |
| Hero | Bilingual badge + headline + stats | Live |
| Marquee | Scrolling partner ticker | Live |
| About | Pain-point cards with hover animation | Live |
| Pillars | Three-pillar system (GVA.tw aligned) | Live |
| Globe | Interactive orthographic globe with country outlines | Live |
| Globe | City legends, hover tooltips | Live |
| Curriculum | 8-module accordion (M1–M8) | Live |
| Proof | YC-style scroll-driven case study wheel | Live |
| Proof | Mobile optimized with image + quote | Live |
| Team | Core team + advisory board | Live |
| Press | 5 media mentions | Live |
| Ecosystem | Partner logo strip | Live |
| Video | Placeholder video shell | Live |
| Apply | Dark CTA section with stats | Live |
| FAQ | 6-question accordion | Live |
| Portal | 5-role stakeholder overlay (Founder/Alumni/Mentor/Investor/Staff) | Live |
| Portal | Per-role info + fake login forms | Live |
| i18n | Full EN/ZH toggle via data attributes | Live |
| SEO | og:image, canonical, FAQPage + Organization schema | Live |

---

## 2. Architecture: Current Scope, Limits, and Strengths

### What the Static Architecture Does Well

- **Zero infrastructure cost** — GitHub Pages is free indefinitely for public repos
- **Instant deployment** — `git push` = live in under 60 seconds
- **No server maintenance** — no databases, no containers, no patches
- **Global CDN** — GitHub's CDN delivers the page from the nearest PoP
- **Auditability** — every change is in git history, fully reversible

### Hard Limits of the Current Architecture

| Limitation | Impact | Resolution Path |
|---|---|---|
| No server-side logic | Cannot process forms, validate auth, or store data | Add Vercel serverless functions |
| No database | No persistent user data, application tracking, cohort records | Airtable (short-term) → PostgreSQL (long-term) |
| No authentication | No real login system; all portal logins are placeholder | Auth0 / Clerk (drop-in auth layer) |
| No CMS | Content changes require code edits | Contentful / Notion as headless CMS |
| Single large file | Hard for multiple engineers to work on simultaneously | Refactor to Astro or Next.js components |
| API key exposure | Cannot securely call private APIs from the frontend | Serverless functions as proxy layer |
| No email processing | `mailto:` links are not trackable or automatable | Systeme.io embed or Formspree + Zapier |

### Scalability Ceiling

**Current architecture can support:**
- ~500,000 page views/month (GitHub Pages limit)
- Unlimited static content updates
- Single-engineer workflows with git branching

**Current architecture cannot support:**
- Real user accounts or session management
- Application intake with database persistence
- Automated email sequences
- Role-based content access
- Real-time cohort data

---

## 3. Stakeholder Framework

### Access Tier Map

| Tier | Role | Current State | Target State |
|---|---|---|---|
| **Public** | Visitors, prospective founders | Full site access | Unchanged |
| **Applicant** | Founders who submitted application | Portal placeholder | Systeme.io form → Airtable |
| **Cohort Member** | Active program participants | Portal placeholder | Systeme.io membership area |
| **Alumni** | Program graduates | Portal login (fake) | Circle.so or custom member area |
| **Mentor** | Assigned mentors | Portal login (fake) | Notion shared workspace |
| **Investor** | Partner VCs | Portal login (fake) | Private Notion page + email |
| **Staff / Admin** | GVA team | Portal login (fake) | Airtable interface + Notion |

### Recommended Short-Term Stack (Zero Custom Backend)

```
Applications:    Systeme.io embed form → webhook → Airtable
Cohort content:  Systeme.io membership area
Community:       Circle.so (private) or Slack/Discord
Mentor mgmt:     Notion shared workspace
Admin backend:   Airtable (interface views per role)
Email comms:     Systeme.io email sequences
```

**Total monthly cost of this stack:** NTD 0–3,200 (Systeme.io Startup: $27/month)

---

## 4. Systeme.io Integration Playbook

### Integration Options (Ranked by Complexity)

**Option A — Embed + Redirect (Recommended for Launch)**
1. Create application form in Systeme.io
2. Copy the HTML embed code
3. Replace the `mailto:` Apply button in the portal with the embedded form
4. Systeme.io handles submission, storage, and automated reply emails
- **Effort:** 2 hours — **Cost:** Free tier sufficient

**Option B — Webhook + Airtable Pipeline**
1. Systeme.io form submission → webhook fires
2. Zapier/Make receives webhook → writes to Airtable base
3. Airtable becomes the CRM for all applicants
4. Staff view applications via Airtable Interface
- **Effort:** 4 hours — **Cost:** Zapier free tier (100 tasks/month) or Make free tier

**Option C — Full Membership Integration**
1. Systeme.io membership area hosts cohort content (videos, materials, sessions)
2. Accepted founders receive an email invite to the membership area
3. Alumni retain access post-cohort with reduced permissions
- **Effort:** 1 week — **Cost:** Systeme.io Startup ($27/month)

### Recommended Launch Sequence

```
Week 1:  Set up Systeme.io account + application form
Week 2:  Embed form in Portal Founder step
Week 3:  Connect Systeme.io webhook → Airtable
Week 4:  Test full funnel: apply → receive confirmation → appear in Airtable
```

---

## 5. Competitive Gap Analysis (vs. YC, Antler, Iterative)

### What Leading Accelerators Have That GVA Doesn't (Yet)

| Feature | YC | Antler | GVA Current | Priority |
|---|---|---|---|---|
| Real team with bios + photos | ✅ | ✅ | ✅ (placeholder) | High |
| Clear investment terms | ✅ ($500K for 7%) | ✅ | Not disclosed | High |
| Alumni directory (searchable) | ✅ | ✅ | Not available | Medium |
| Application deadline + countdown | ✅ | ✅ | Not shown | High |
| Press coverage section | ✅ | ✅ | ✅ (placeholder) | Medium |
| Demo Day page / archive | ✅ | ✅ | Not built | Low |
| Blog / Founder Insights | ✅ | ✅ | Not built | Medium |
| Portfolio company logos | ✅ | ✅ | Not available | High |
| Partner VC logos (real) | ✅ | ✅ | Placeholder | High |
| Video content | ✅ | ✅ | Placeholder | Low |
| Job board | ✅ | ✅ | Not built | Low |

### Highest-Leverage Gaps to Close (Effort vs. Impact)

1. **Real team bios** — single highest trust signal; no engineering needed, just content
2. **Clear pricing/terms** — removes the #1 objection in the application decision
3. **Application deadline** — scarcity + urgency is proven to drive conversion
4. **Real partner VC logos** — social proof for the investor/founder audience
5. **A blog post** — one well-written post can drive more SEO traffic than all meta tags combined

---

## 6. SEO Architecture

### Current SEO State

| Element | Status | Notes |
|---|---|---|
| Title tag | Optimized | GVA Founders Playbook + Taiwan-to-Global |
| Meta description | Present | Could be richer with call-to-action |
| og:image | Added | placehold.co temporary |
| Canonical URL | Added | GitHub Pages URL |
| Schema — Course | Present | Basic course markup |
| Schema — Organization | Added | GVA organization structured data |
| Schema — FAQPage | Added | Maps to FAQ section |
| Schema — Event | Added | Cohort 2026 as an event |
| sitemap.xml | Added | Static file, lists key pages |
| robots.txt | Added | Allows all crawlers |
| Core Web Vitals | Good | Single static file, minimal JS |
| hreflang | Present | EN + ZH-TW alternates |

### SEO Growth Levers (Post-Launch)

**Short-term (no engineering):**
- Submit sitemap to Google Search Console
- Set up Google Analytics 4 with conversion events
- Add a `<link rel="preload">` for the hero font

**Medium-term (minor engineering):**
- Add a `/blog` directory with 3–5 static HTML articles
  - Target keywords: "Taiwan startup global fundraising," "how to pitch US VCs from Asia," "pre-accelerator Taiwan"
- Add FAQ structured data for more FAQ items

**Long-term (with CMS):**
- Notion or Contentful as headless CMS
- Auto-generate blog pages from Notion entries
- Dynamic OG images (using Vercel OG)

### Ongoing SEO Principle (For All Future Edits)

Every new section added to the site should:
1. Have a descriptive `id` attribute for anchor linking
2. Use semantic heading hierarchy (one H1 per page, H2 per section)
3. Include `aria-label` on interactive elements
4. Use `alt` text on all images
5. Avoid text inside images (not indexable)

---

## 7. Analytics & Metrics Collection

### Recommended Analytics Stack

| Tool | Cost | What It Tracks |
|---|---|---|
| Google Analytics 4 | Free | Page views, sessions, geography, device |
| PostHog | Free (up to 1M events) | Session recordings, funnels, heatmaps |
| Google Search Console | Free | Impressions, clicks, keyword rankings |

### Key Events to Track (Copy-Paste Into GA4 Setup)

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

### Dashboard Metrics to Review Weekly

| Metric | Benchmark | GVA Target |
|---|---|---|
| Unique visitors / month | — | 500 (Month 1) → 2,000 (Month 3) |
| Apply button CTR | 2–4% (B2B) | 3% |
| Portal role breakdown | — | 70% Founder / 20% Investor / 10% Other |
| Avg. session duration | 2 min | 3.5 min |
| Mobile % | 60% avg | Monitor for UX issues |
| Bounce rate | 50–70% | Below 60% |

---

## 8. Minimum Success Criteria (MSC)

### Phase 1 — Website as Lead Generation Tool (Months 1–3)

| Criterion | Minimum | Target |
|---|---|---|
| Applications received | 30 | 80 |
| Website → Apply click CVR | 1.5% | 3% |
| Organic monthly visitors | 300 | 1,000 |
| Avg. session duration | 2 min | 4 min |
| Media/partner outreach responses | 3 | 10 |

### Phase 2 — First Cohort Execution (Months 3–6)

| Criterion | Minimum | Target |
|---|---|---|
| Cohort enrollment | 8 founders | 15 founders |
| Cohort completion rate | 80% | 95% |
| Alumni NPS | 40 | 70 |
| Founder raises within 12 months | 2 | 5 |
| Referral-driven applications (Cohort 2) | 10% | 30% |

### Phase 3 — Business Model Validation (Month 6+)

| Criterion | Definition |
|---|---|
| Unit economics positive | Program fee × cohort size > all operating costs |
| Cohort 2 without paid ads | Organic + referral fills all 15 spots |
| VC partner co-investment | At least 1 GVA portfolio company receives introduction from partner VC |
| Press pickup (organic) | At least 1 unsolicited media mention |

---

## 9. Cost & Investment Analysis

### Development Cost (Current Website)

| Item | Hours | AI-Assisted Cost | Traditional Agency Cost |
|---|---|---|---|
| Design system + UI | 6h | ~NTD 200 | NTD 80,000–150,000 |
| Frontend development | 10h | ~NTD 300 | NTD 100,000–200,000 |
| Interaction design (globe, animations) | 5h | ~NTD 150 | NTD 60,000–120,000 |
| Bilingual system | 2h | ~NTD 50 | NTD 20,000–40,000 |
| Mobile optimization | 3h | ~NTD 100 | NTD 30,000–60,000 |
| SEO + portal system | 2h | ~NTD 50 | NTD 20,000–40,000 |
| **Total** | **~25h** | **~NTD 850** | **NTD 310,000–610,000** |

**Cost reduction: 99.7%** — versus traditional agency development.

*AI cost calculation basis: Claude Code subscription NTD 640–3,200/month; estimated 2–3 months of active development.*

### Ongoing Cost Projection (Post-Launch)

| Item | Monthly Cost |
|---|---|
| GitHub Pages hosting | NTD 0 |
| Systeme.io Startup plan | NTD 850 (~USD 27) |
| Google Analytics + Search Console | NTD 0 |
| Custom domain (gva.tw, already owned) | NTD 0 (amortized) |
| Claude Code subscription (ongoing development) | NTD 640–3,200 |
| **Total** | **NTD 1,490–4,050/month** |

---

## 10. Migration Roadmap to Vercel + Multi-Engineer Collaboration

### Why Vercel (vs. Alternatives)

| Platform | Pros | Cons |
|---|---|---|
| **Vercel** (recommended) | Free tier generous, serverless functions, env vars, CI/CD built-in, Next.js native | Vendor lock-in for some features |
| Netlify | Similar to Vercel | Slightly slower builds |
| Railway | Full backend, databases | Costs money immediately |
| AWS/GCP | Maximum control | Very high operational overhead |

### Phase 1 Migration: Static Site → Vercel (1 Day)

```bash
# Step 1: Install Vercel CLI
npm i -g vercel

# Step 2: From the project directory
vercel

# Step 3: Set custom domain in Vercel dashboard
# Add playbook.gva.tw → CNAME → cname.vercel-dns.com

# Step 4: Update GitHub Actions to deploy to Vercel on push
# (Vercel auto-generates the GitHub Action)
```

**Result:** Same single-file site, now on Vercel with preview deployments on every PR.

### Phase 2: Refactor to Component Architecture (1–2 Weeks with Engineer)

```
Recommended framework: Astro
- Outputs 100% static HTML (like current)
- Components in .astro files (HTML + scoped CSS + JS)
- Easy to add blog (Markdown → pages automatically)
- File-based routing (pages/apply.astro, pages/blog/[slug].astro)
- Drop-in Vercel adapter
```

Proposed directory structure:
```
gva-founders-playbook/
├── src/
│   ├── components/
│   │   ├── Hero.astro
│   │   ├── Pillars.astro
│   │   ├── Globe.astro
│   │   ├── Curriculum.astro
│   │   ├── Portal.astro
│   │   └── ...
│   ├── layouts/
│   │   └── Base.astro
│   ├── pages/
│   │   ├── index.astro
│   │   └── blog/
│   └── content/        ← Markdown blog posts
├── public/
│   ├── sitemap.xml
│   └── robots.txt
├── CLAUDE.md           ← AI collaboration rules (already exists)
└── astro.config.mjs
```

### Phase 3: Backend Layer (When Needed)

**Trigger:** When real authentication, application tracking, or dynamic content is required.

```
Auth:      Clerk (drop-in, NTD 0 for small scale)
Database:  PlanetScale (MySQL, free tier) or Supabase (PostgreSQL)
CMS:       Contentful or Sanity (free tier)
Payments:  Stripe (for program fees)
```

### Engineer Onboarding Checklist

For a new engineer joining the project:

**Access & Setup**
- [ ] GitHub repository access (`vincentt-wang/gva-founders-playbook`)
- [ ] Vercel project access (after migration)
- [ ] Custom domain DNS access (if touching routing)
- [ ] Google Analytics property access
- [ ] Systeme.io account access (for form management)
- [ ] Airtable base access (for application tracking)
- [ ] Read `CLAUDE.md` — all design + AI collaboration rules are documented there

**Development Workflow**
- [ ] Clone repo → open `index.html` in browser → confirm it works
- [ ] Create `dev` branch — never push directly to `main`
- [ ] Feature branches: `feature/[description]` from `dev`
- [ ] PR to `dev` → review → merge to `main` for production

**Key Rules (from CLAUDE.md)**
- Minimum font size: 16px everywhere
- No emoji in UI (SVG icons only)
- Bilingual: all new text needs `data-en` and `data-zh` attributes
- Buffer ≥ 50px before deploying layout changes
- Animation architecture: all step reveals through `findNextRevealable()`

**For AI-Assisted Development (Claude Code)**
- Existing session context is in `.claude/projects/` memory
- The `CLAUDE.md` file primes Claude on all design rules
- Use `claude` command in the project directory for context-aware assistance

---

## 11. AI Tool Integration Possibilities

### Immediately Feasible (No Backend)

| Integration | Tool | Effort | Monthly Cost |
|---|---|---|---|
| AI chatbot (FAQ answering) | Crisp.chat with AI | 1 hour | NTD 0–800 |
| Application form processing | Systeme.io native | 2 hours | Included in plan |
| SEO content generation | Claude via Claude.ai | Ongoing | Subscription |

### Feasible with Serverless Functions (Vercel)

| Integration | Description | Cost |
|---|---|---|
| AI application screener | Submit → Claude API → score + summary → Airtable | ~NTD 0.10/application |
| Dynamic OG images | Generate social card per page with founder stats | Vercel OG library (free) |
| AI chatbot (custom) | Claude API via serverless proxy | ~NTD 30–100/month |

### Estimated AI API Costs

At Claude Sonnet 4.6 pricing (input: USD 3/M tokens, output: USD 15/M tokens):

- AI chatbot, 500 conversations/month, avg 800 tokens each: ~**NTD 40/month**
- Application screener, 100 applications, 1,500 tokens each: ~**NTD 15/month**
- Total AI API costs at launch scale: **under NTD 100/month**

---

## 12. Immediate Action Checklist

### For Tina (Program Lead) — Next 2 Weeks

- [ ] Decide on program pricing/investment terms (publish on site or not)
- [ ] Provide real team bios and photos for 2–3 core team members
- [ ] Confirm application open/close dates for Cohort 2026
- [ ] Set up Systeme.io account and create application form
- [ ] Connect custom domain `playbook.gva.tw` to GitHub Pages

### For Terry (Lead Investor) — For Discussion

- [ ] Review investor portal messaging (does it reflect GVA's actual investor value prop?)
- [ ] Confirm which partner VCs can be named publicly on the site
- [ ] Define criteria for "Cohort 2 fill rate without ads" milestone

### For Engineering Team — When Engaged

- [ ] Clone repo and read `CLAUDE.md`
- [ ] Set up local dev environment
- [ ] Evaluate Astro migration vs. staying on single-file HTML
- [ ] Plan Vercel migration (estimated: 1 day)
- [ ] Set up Google Analytics 4 with event tracking
- [ ] Add application form (Systeme.io embed or custom)

### For Everyone — Right Now

- [ ] Share the live URL with 5 potential applicants for feedback
- [ ] Identify 2–3 real alumni/advisors who can provide quotable testimonials
- [ ] Submit sitemap to Google Search Console

---

## Appendix: Technology Decisions Log

| Decision | Alternative Considered | Why We Chose This |
|---|---|---|
| Single HTML file | Next.js, Astro | Maximum portability, zero build complexity at this stage |
| GitHub Pages | Vercel, Netlify | Zero cost, already used; Vercel migration is trivial when ready |
| Canvas 2D for globe | Mapbox, Leaflet | No API key needed, full visual control, no ongoing cost |
| i18n via data attributes | i18next library | Zero dependency, same performance, works offline |
| Pravatar.cc for placeholders | Lorem Picsum | Consistent face-like images for team/testimonial placeholders |
| TopoJSON for country outlines | Hard-coded coordinates | Accurate Natural Earth data, CDN-hosted, ~8KB |

---

*This document was generated as a living strategic reference. It will be updated as GVA moves from prototype to production. The most current version is always in the repository at `GVA_Strategy_Report_v2.md`.*

*Prepared with Claude Code (claude-sonnet-4-6) — Anthropic, 2026*
