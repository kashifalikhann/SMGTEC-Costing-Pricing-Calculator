# SMGTEC Internal Pricing Engine — Build vs Buy & Improvement Plan

**Date:** 2026-06-04
**Purpose:** Help SMGTEC decide whether to keep building their own internal pricing calculator, and what to improve if they do.

---

## 1. What This Calculator Does (and Why It Exists)

SMGTEC's internal tool is used by the **sales team** to:

- Calculate internal cost to deliver (hardware wholesale + licensing cost + labor)
- Generate 3 service tiers (T1 Data Protection → T3 Fully Protected)
- Ensure margins stay above 50% (with real-time visual feedback)
- Account for Spanish regulation (50% hardware deposit upfront)
- Override prices manually per client when needed

It's a **margin guardrail tool**, not a quote generator. The sales team uses it to know the floor they can negotiate from.

---

## 2. Build vs Buy: Should SMGTEC Use a Commercial Tool?

A quick honest comparison of what commercial quoting tools offer vs. the custom calculator:

| Need | SMGTEC Custom Tool | Commercial (Quoter, QuoteWerks, Zomentum) |
|------|-------------------|------------------------------------------|
| Cost to acquire | €0 (built in-house) | €149–$569/mo (Quoter), $15–85/user (QuoteWerks) |
| Training time | None (already use it) | Days to weeks per sales rep |
| Spanish-specific (IVA, 50% deposit, LOPDGDD) | ✅ Built in | ❌ None support Spanish regulation out of box |
| Distributor price integration | ❌ Manual DB | ✅ QuoteWerks has 100+ catalogs |
| PDF proposals | ❌ Not yet | ✅ Built-in templates |
| Client history | ❌ Not yet | ✅ CRM-like database |
| Margin control | ✅ Hardcoded thresholds | ❌ Generic, no automated guardrails |
| SLA risk visibility | ✅ Built-in | ❌ Not a standard feature |
| Internet required | ❌ No (runs offline) | ✅ Usually cloud |

### Verdict for SMGTEC: Keep building

A commercial tool would cost €150–600+/mo, lack Spanish regulation support, and force your sales team to learn a new system. The custom tool is already better at the things that matter for your specific market and margins. The question is **what to add next**.

---

## 3. What to Learn from Commercial Tools (Feature Borrowing)

Here are the features from commercial quoting tools that would directly help SMGTEC's sales team, ordered by impact:

| Borrow From | Feature | Why SMGTEC Needs It |
|-------------|---------|---------------------|
| **Quoter/ScalePad** | Branded PDF proposals | Sales team currently builds proposals manually after calculating. Auto-generating them saves hours per client. |
| **Zomentum** | MRR tracking per client | Knowing total recurring revenue across all clients helps prioritize sales effort. |
| **QuoteWerks** | Distributor price sync | Manually updating FortiGate/Dell costs is error-prone. An API feed would keep margins accurate. |
| **Halo PSA** | Client notes & history log | Remembering past quote adjustments per client avoids renegotiating from scratch. |
| **All of them** | Quick-share link | Sales can email a web link instead of explaining numbers over the phone. |

---

## 4. Spanish MSP Market — Pricing Reality Check

Since the calculator prices actual SMGTEC clients, the question isn't "who competes with the calculator" but "how does SMGTEC's pricing compare to other Spanish MSPs?"

| Factor | SMGTEC Calculator | Spanish MSP Average | Notes |
|--------|-------------------|--------------------|------|
| **Labor rate** | €40/hr internal (€100/hr billed) | €40–55/hr | Your internal cost rate is standard for Spain. Billed rate looks competitive. |
| **Per-user pricing** | €10–50/user/mo (T1–T3 tiers) | Common model in Spain | Aligned with market norms. |
| **Tier 1 monthly** | ~€249–299/mo (10 users) | Typical entry-level | On the lower end — possibly leaving margin on the table. |
| **Tier 3 monthly** | ~€500–999/mo (10 users) | €800–1,500/mo for full stack | Your T3 may be under-priced for the stack you're delivering (Datto + FortiGate + N-Central + S1 + IT Glue). |
| **Hardware markup** | ~55–70% (wholesale→retail) | 40–60% standard | Your markup is healthy. |
| **50% deposit** | ✅ Built in | Common but not universal | You have an edge — protects cash flow legally. |

**Observation:** T3 may be under-priced relative to the tech stack you're bundling. Worth checking against actual delivery costs.

---

## 5. Practical Improvement Plan (What Actually Helps the Sales Team)

### Immediate (this week) — Pain Points the Sales Team Feels Now

1. **Can't save client data** — every client visit starts from scratch. Add localStorage so last state is remembered.
2. **No print/PDF output** — sales have to manually copy numbers into a proposal doc. Add a printable summary view.
3. **No quick-share link** — sales can't email a calculation to the client for review. Encode state in URL hash for sharing.
4. **Can't edit hardware costs** — when FortiGate prices change, someone has to edit the code. Move hardware DB to a JSON block the team can edit.
5. **No client NIF/name field** — proposals need this. Add a simple text field at the top.

### Short-term (this month)

6. **Client history** — save/load named client profiles in localStorage so sales can revisit and adjust.
7. **Margin target per tier** — not all clients need 50% margin. Let the sales lead set per-tier targets.
8. **Hardware cost versioning** — track when prices were last updated so margins don't drift.
9. **Export to CSV** — sales team can batch-export all clients for management review.

### Medium-term (quarterly)

10. **Lightweight backend (SQLite/supabase)** — shared database so multiple sales reps can see all client pricing. This is the biggest unlock.
11. **Simple auth** — Google login or magic link so the team can access from anywhere.
12. **English/Spanish toggle** — some clients prefer proposals in English.

### Not Worth Building (use existing tools instead)

| Don't build | Use Instead | Why |
|-------------|-------------|-----|
| Distributor price API | Manual DB with quarterly updates | API integrations require ongoing maintenance and contracts with distributors |
| Full PSA integration | CSV export → import to existing PSA | Your PSA likely already has import; building a connector is overkill |
| AI scoping engine | Sales judgment + current tiers | The 3-tier model already covers the range; AI adds complexity you don't need yet |
| Client-facing portal | Email PDF | Clients don't need live access — they need a clear proposal |

---

## Summary

**Keep the custom calculator.** No commercial tool does Spanish regulation, margin guardrails, and SLA risk visibility as well. Invest in:

1. **Saving and sharing client data** (immediate win for sales team)
2. **PDF proposal generation** (makes your team look professional without extra work)
3. **A lightweight shared database** when the team grows beyond 1–2 sales reps

Meanwhile, T3 pricing may be too low for the stack you're delivering — that's worth a margin review.

---

*This replaces the earlier version which incorrectly compared the calculator against commercial tools as "competitors." The calculator is an internal tool; the question is build vs. buy, and if build, what makes the sales team more effective.*
