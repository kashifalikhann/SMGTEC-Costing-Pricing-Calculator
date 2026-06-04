# SMGTEC Enterprise Pricing Engine — Improvement Roadmap

**Date:** 2026-06-04
**Status:** Research & Planning Complete
**Current:** Single-file HTML/JS pricing calculator (3 tiers, real-time margin calc, SLA exposure, Spanish deposit compliance)
**Target:** Multi-tenant enterprise MSP pricing & quoting platform

---

## 1. Current Feature Inventory (baseline)

| Feature | Status | Details |
|---------|--------|---------|
| 3-Tier Pricing Model | ✅ Live | T1: Data Protection, T2: Active Perimeter, T3: Fully Protected |
| Real-Time Margin Calculation | ✅ Live | Setup, Monthly Y1/Y2, Aggregate Y1 with color thresholds (50%) |
| Hardware Cost Database | ✅ Live | FortiGate, Dell servers, Datto Siris, APC UPS, cabling — wholesale/retail pairs |
| Licensing Cost Database | ✅ Live | M365, VoIP, ESET, S1, N-Central, IT Glue, BACKBLAZE, MSP360, FortiGuard |
| M365 Sourcing Toggle | ✅ Live | Business Standard vs Premium, wholesale vs retail pass-through |
| VoIP Toggle | ✅ Live | Per-user costing with wholesale/retail |
| Hardware Add-ons | ✅ Live | Switch, UPS, printers (B&W + color) |
| SLA Penalty Exposure | ✅ Live | T2 at 10%, T3 at 15% of monthly recurring |
| Spanish 50% Deposit Rule | ✅ Live | Upfront hardware payment compliance |
| 10-Workstation Minimum Billing | ✅ Live | Auto-scaling with warning banner |
| Pricing Manual Overrides | ✅ Live | Per-tier setup + monthly overrides |
| Tailwind UI (CDN) | ✅ Live | Clean dark theme with brand colors (smg_dark, smg_cream, smg_gold) |
| Labor Standard (€40/hr) | ✅ Live | Hardcoded internal + retail rates |

---

## 2. Competitor Landscape (Top 10 MSP Pricing Tools)

### Tier 1 — Enterprise CPQ / PSA-Native

| Tool | Pricing | Strengths | Weaknesses |
|------|---------|-----------|------------|
| **QuoteWerks** | $15–30/user/mo | 100+ distributor catalogs, real-time pricing, hardware-heavy quoting | Desktop app (legacy), poor UX, no AI |
| **ConnectWise CPQ (Sell)** | $50–85/user/mo | Deep PSA ecosystem, CRM integration, quote templates | Being sunset, 2-3 month implementation, over-engineered |
| **Kaseya Quote Manager** | Bundled with Kaseya | Real-time distributor pricing, procurement automation, e-commerce flow | Complete vendor lock-in, ecosystem-only |
| **HaloPSA** | $35–109/agent/mo | Modern UI, transparent pricing, deep configurability, PSA-native quoting | Separate RMM needed, steep learning curve for config |

### Tier 2 — Cloud-Native Quoting & Proposals

| Tool | Pricing | Strengths | Weaknesses |
|------|---------|-----------|------------|
| **Quoter (ScalePad)** | $149–569/mo | Cloud-native, modern UX, fast proposals, distributor integrations | Quote caps per tier, limited AI, hardware-heavy focus |
| **Zomentum** | $99–199/user/mo | AI-powered, sales enablement + quoting, MRR tracking, pipeline | Less known, smaller ecosystem, integration depth |

### Tier 3 — Analytics & Intelligence (Complementary)

| Tool | Pricing | Focus | Relevance |
|------|---------|-------|-----------|
| **Analytify.ai** | ~$1.5K–5K/mo | MSP BI, semantic layer, embedded client portals | Not a quoter — analytics overlay for profitability tracking |
| **MSPCFO** | ~$2K–4K/mo | Client profitability analytics, SLA scorecards, automated insights | Reporting layer, no quoting |
| **Scopable** | Free (alpha) | AI scoping from PSA data, risk assessments | Newest; AI-first approach worth watching |

### Tier 4 — Free / Lightweight Calculators

| Tool | Pricing | Notes |
|------|---------|-------|
| **NinjaOne Pricing Calc** | Free Excel | COLA factor, security stack, Spanish landing page exists |
| **CalculaFast** | Free web | Margin modeling, support hour stress testing |

---

## 3. Gap Analysis: SMGTEC vs Enterprise Competitors

### Critical Gaps (must-have for enterprise upgrade)

| # | Capability | Gap Severity | Competitor Baseline |
|---|-----------|-------------|---------------------|
| 1 | **Client portfolio management** (multi-client, search, history) | 🔴 Critical | All PSA tools have this |
| 2 | **Data persistence** (localStorage → indexed DB → cloud) | 🔴 Critical | Even free tools save state |
| 3 | **PDF proposal generation** (branded, line-item, Spanish legal format) | 🔴 Critical | Quoter, QuoteWerks, Zomentum all do this |
| 4 | **IVA (VAT) handling** (21% Spanish IVA, reverse charge, exempt) | 🟠 High | Required by Spanish law |
| 5 | **LOPDGDD/RGPD compliance module** (DPO cost, data audit, AEPD risk) | 🟠 High | No competitor does this — potential moat |
| 6 | **Multi-language interface** (ES/EN/CAT) | 🟠 High | Spanish MSPs operate bilingually |
| 7 | **Labor truly-loaded cost** (salary + SS + IRPF + training + tools) | 🟠 High | Currently hardcoded €40/hr, not modeled |
| 8 | **Export / shareable links** (URL state encoding or export JSON) | 🟠 High | Quoter generates shareable proposal links |
| 9 | **Profitability analytics / dashboards** (trends, per-client P&L) | 🟠 High | Analytify, MSPCFO core offering |
| 10 | **NIS2 compliance tracking** (18 mandatory sectors, Article 23/24) | 🟠 High | New EU directive — first-mover opportunity |

### Secondary Gaps (competitive differentiators)

| # | Capability | Gap Severity | Notes |
|---|-----------|-------------|-------|
| 11 | **Scenario / what-if modeling** (Monte Carlo, best/worst case) | 🟡 Medium | CalculaFast does basic version |
| 12 | **API / integration layer** (PSA, RMM, CRM webhooks) | 🟡 Medium | ConnectWise, Halo PSA have mature APIs |
| 13 | **Multi-currency** (EUR default, USD/GBP for hardware sourcing) | 🟡 Medium | Needed for distributor price comparison |
| 14 | **Collaboration / approval workflow** (sales → ops → director) | 🟡 Medium | QuoteWerks has this |
| 15 | **Client-facing portal / self-service quotes** | 🟡 Medium | ScalePad, Zomentum offer this |
| 16 | **vCIO roadmap generation** (strategic planning outputs from data) | 🟢 Low | Scopable touches this — differentiator |
| 17 | **AI-powered scoping** (natural language → tier recommendation) | 🟢 Low | Scopable alpha feature |
| 18 | **Integrator/distributor price feeds** (Ingram, Tech Data, etc.) | 🟢 Low | QuoteWerks strongest here, not realistic short-term |

---

## 4. Spanish Market Context

### Regulatory Landscape (Opportunity to Build Moat)

| Regulation | Scope | Penalty | Application |
|-----------|-------|---------|-------------|
| **RGPD (EU 2016/679)** | All EU data processing | Up to €20M or 4% global turnover | Every client with employee/ customer data |
| **LOPDGDD 3/2018** | Spanish implementation of RGPD | Fines + AEPD enforcement | CCTVs, geolocation, biometrics, digital disconnection |
| **ENS (RD 311/2022)** | Public sector & government contractors | Loss of contract, exclusion from public tenders | Critical for SMGTEC government clients |
| **NIS2 (Directive 2022/2555)** | 18 critical sectors (energy, transport, health, digital infra, etc.) | Fines, liability, mandatory reporting | Security obligations — complements Tier 2/3 stack |
| **50% Deposit Law (Ley de Contratos)** | B2B hardware procurement | Civil liability | Already implemented in calculator |

### Market Data
- Spain MSP market: ~€7.2B (2024), growing 5.22% CAGR
- Average billing: ~€40–55/hr (matches current calculator)
- Per-user pricing is the norm (vs. per-device in US)
- IVA (VAT): 21% standard, 10% reduced (some IT services)

### Competitive Positioning
- **No competitor** currently offers an integrated RGPD/LOPDGDD compliance cost calculator
- **No competitor** automates NIS2 readiness cost estimation
- **ENS** compliance is mandatory for Spanish public sector — SMGTEC has government clients
- This regulatory gap is a **sustainable moat**, not a feature toggle

---

## 5. Recommended Architecture (Phase 0–3)

### Phase 0 — Immediate (Single-Week)
_Focus: Zero-dependency improvements to existing single-file app_

- [ ] **localStorage persistence** — save/load calculator state across sessions
- [ ] **Export to JSON / URL sharing** — encode state in URL hash for quick sharing
- [ ] **IVA toggles** — 21% / 10% / exempt with live "with tax" column
- [ ] **Multi-language strings** — ES/EN via simple JSON object swap
- [ ] **Fully-loaded labor model** — salary + SS (30%) + training + tools → true cost/hr
- [ ] **Improved UI** — hover tooltips on every input, print-friendly CSS
- [ ] **Accessibility** — aria labels, keyboard nav, contrast audit

### Phase 1 — Professional (2–3 Weeks)
_Focus: Multi-client, proposals, compliance_

- [ ] **Client database** — localStorage-backed client CRUD (name, NIF, address, sector)
- [ ] **PDF proposal generation** — jsPDF or pdfmake with SMGTEC brand template
- [ ] **Proposal version history** — saved snapshots per client
- [ ] **RGPD/LOPDGDD cost estimator** — DPO hours, data audit, consent mgmt, AEPD risk score
- [ ] **NIS2 readiness module** — sector selector → obligation checklist → cost estimate
- [ ] **ENS compliance** — public sector module with categorization levels (BASIC/MEDIUM/HIGH)
- [ ] **Export CSV** — bulk export all clients with key metrics
- [ ] **Dark/light mode** — user-preference toggle

### Phase 2 — Growth (1–2 Months)
_Focus: Analytics, intelligence, integration_

- [ ] **Profitability dashboard** — per-client gross margin, MRR trend, cohort analysis
- [ ] **Revenue forecasting** — based on current proposals, win-rate assumptions
- [ ] **What-if scenario modeling** — change variables across all clients simultaneously
- [ ] **API endpoints** — lightweight Express/Fastify backend or serverless functions
- [ ] **PSA integration** — webhook targets for ConnectWise, Halo PSA, Autotask
- [ ] **Integrator price catalogs** — sync from Ingram/Tech Data (distributor API)
- [ ] **User authentication** — simple JWT or magic-link for multi-user access
- [ ] **Client portal** — read-only proposal view for client approval

### Phase 3 — Scale (3–6 Months)
_Focus: AI, platform, market positioning_

- [ ] **AI scoping engine** — describe client needs in natural language → tier/budget recommendation
- [ ] **Automated proposal generation** — AI drafts proposal narrative from pricing data
- [ ] **White-label / MSP resell** — other Spanish MSPs can use SMGTEC-branded instance
- [ ] **Public API** — REST API for third-party integrations
- [ ] **Marketplace listing** — as a "Spanish MSP Compliance + Pricing" tool
- [ ] **vCIO strategic planning** — multi-year roadmap generation from pricing data

---

## 6. Go-to-Market Strategy

### Positioning
> "The only MSP pricing & quoting platform built for Spanish regulation."

### ICP
- Spanish MSPs with 5–50 employees (€500K–€5M revenue)
- Serving regulated sectors (healthcare, legal, finance, public sector)
- Currently using spreadsheets or no formal pricing tool
- Need RGPD/LOPDGDD/NIS2 compliance baked into the quote

### Distribution
1. **Direct outbound** — Spanish MSP associations, LinkedIn
2. **Community** — r/msp-es, RiiOT, MSP Iberia events
3. **Partner** — bundle with PSA implementations, law firms advising on data protection
4. **Content** — "MSP Pricing in Spain: Regulatory Compliance Cost Guide"
5. **Free tier** — single-client version with RGPD estimator → upsell multi-client analytics

### Monetization
| Tier | Price | Target |
|------|-------|--------|
| **Free** | €0 | Solo operators, evaluation |
| **Starter** | €29/mo | Up to 5 clients, RGPD module |
| **Professional** | €79/mo | Unlimited clients, NIS2 + ENS, export, PDF proposals |
| **Enterprise** | Custom | API, white-label, multi-user, PSA integration |

---

## 7. Next Actions (Immediate)

1. **⏩ Phase 0 implementation** — localStorage, IVA, multi-language, fully-loaded labor
2. **⏩ Publish Phase 0** — iterative deployment to GitHub Pages (same repo, branch-based)
3. **⏩ User testing** — let current SMGTEC sales team use it, gather feedback
4. **⏩ Phase 1 planning** — detailed spec for client DB + PDF + compliance modules

---

*This document is a living roadmap. Priority order may shift based on user feedback and market signals.*
