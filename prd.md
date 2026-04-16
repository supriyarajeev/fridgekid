# Product Requirements Document
# FridgeKid — Smart Fridge Nutrition App for Kids

**Version:** 1.1
**Date:** April 16, 2026
**Status:** Draft — updated after Engineering Manager and Senior Product Lead review

---

## Revision Notes (v1.0 → v1.1)
- Preserved the strongest research-backed framing: manual tracking fails, meal planning is the real pain, and shared family meals matter more than nutrition detail
- Tightened v1 scope to one launch path: compatible smart-fridge integration only; fallback inventory modes moved out of v1 scope
- Converted vague product ideas into clearer build requirements and launch gates
- Added explicit non-goals for v1 to reduce feature creep
- Clarified what the product does and does not claim about nutrition accuracy
- Replaced generic milestones with concrete discovery/build/beta gates

---

## 1. Overview

### 1.1 Product Summary
FridgeKid is a mobile app for parents that uses a smart fridge as the source of truth for what food is at home, then turns that inventory into simple kid-focused meal suggestions and a lightweight nutrition snapshot. The product is designed to reduce meal-planning friction, not add another tracking task.

### 1.2 Problem Statement
Parents do not fail at kids' nutrition tracking because they do not care. They fail because the current workflow is too manual, too repetitive, and too fragile for real family life. The clearest pattern in the research is that parents already feel overburdened by picky eating, allergies, conflicting schedules, and decision fatigue. If the app adds logging work, planning work, or another place to manage food information, it will be abandoned.

Evidence from research:

> "Writing everything down was a pain and never stuck."
> — Reddit, r/iosdev, February 26, 2026

> "I've spent 45 minutes planning a week that's already wrong."
> — Reddit, r/blendedfamilies, February 26, 2026

> "I so wish we could all sit at the table and eat essentially the same thing."
> — Reddit, r/workingmoms, October 11, 2025

### 1.3 Market Size Constraint
The research in `research/` does not contain a reliable market-size estimate for smart-fridge households, so TAM/SAM figures are intentionally omitted from this PRD.

Known constraint:
- A smart-fridge-dependent v1 will be narrower than a general mobile app.
- The narrower initial market is acceptable only if the product meaningfully reduces workload for parents who already have compatible kitchen hardware.
- Because the initial market is constrained, v1 success should be judged primarily on repeat usage, trust, and parent-reported relief, not broad top-of-funnel volume.

---

## 2. Goals & Success Metrics

### 2.1 Goals
- Reduce the cognitive load of feeding kids at home
- Eliminate manual nutrition logging as the core workflow
- Help parents make one flexible family meal instead of multiple separate meals
- Surface useful nutrition guidance without guilt, calorie obsession, or clinical complexity
- Support real parent workarounds such as safe foods, batch cooking, and repetitive meal rotation

### 2.2 Success Metrics
| Metric | Target | Rationale |
|---|---|---|
| Parent-reported reduction in meal-planning stress | Primary beta metric; measured weekly | The research strongly validates stress as the core pain point |
| % of active households viewing at least 1 meal suggestion per week | Primary engagement metric | Confirms whether the home-screen value proposition is compelling |
| % of active households confirming or accepting at least 1 suggested meal per week | Primary value-delivery metric | Stronger than raw opens; tests whether suggestions are actually useful |
| Parent satisfaction / NPS | Secondary beta metric | Research supports measuring trust and relief, not a specific public benchmark |
| Manual corrections per active household per week | Guardrail metric; should trend down over time | Tracks whether passive inventory is becoming trustworthy enough |
| % of households still active after 4 weeks | Retention metric | Appropriate for a narrow but high-intent v1 audience |

### 2.3 Monetization Model
Proposed model: freemium subscription.

- **Free tier:** 1 child profile, daily home-screen meal suggestion, simple nutrition snapshot
- **Paid tier:** multiple child profiles, shared household access, shopping gap suggestions, meal history, household customization

Rationale from research:
- Parents are already piecing together workarounds such as `Pediasure`, milkshakes, ChatGPT meal planning, freezer batches, and even self-built apps.
- That suggests willingness to invest in solutions that clearly save effort or reduce worry, but the research does not support a specific price point yet.

Non-goal for v1:
- Monetization optimization is not a launch blocker. The product must first prove repeat weekly usage and trust in the inventory-to-meal loop.

---

## 3. Target Users

### 3.1 Primary User: The Overloaded Parent
- Parent of kids roughly toddler through elementary age
- Responsible for feeding a household with different needs and preferences
- Already juggling work, scheduling, and household logistics
- Wants fewer decisions, not more content

Research signal:

> "I so wish we could all sit at the table and eat essentially the same thing."
> — Reddit, r/workingmoms, October 11, 2025

### 3.2 Secondary User: The Parent of a Picky Eater
- Child has a narrow set of acceptable foods or strong food rigidity
- Parent worries about growth, protein, and nutritional gaps
- Household meals are often distorted around one child's "safe foods"

Research signals:

> "My son (11) essentially controls what my family eats with his completely inflexible pickiness."
> — Reddit, r/ParentingADHD, February 14, 2026

> "Finding foods that aren't highly processed that she will actually eat is a struggle."
> — Reddit, r/Parenting, November 25, 2025

### 3.3 Out of Scope — User Types (v1)
- Families seeking medical diagnosis or treatment for ARFID or other clinical feeding disorders
- Adults who want general-purpose calorie or macro tracking for themselves
- Households where most meals are eaten away from home and fridge inventory is not a useful signal
- Households without a compatible smart fridge

### 3.4 Out of Scope — Features (v1)
See §6.2 for the full excluded features list.

---

## 4. User Problems (Evidence-Based)

| # | Pain Point | Evidence |
|---|---|---|
| P1 | Manual nutrition tracking does not stick | "Writing everything down was a pain and never stuck." |
| P2 | Meal planning breaks when family composition and constraints change | "I've spent 45 minutes planning a week that's already wrong." |
| P3 | One child's rigidity can dominate household food decisions | "My son (11) essentially controls what my family eats..." |
| P4 | Parents want one family meal, not multiple custom dinners | "I so wish we could all sit at the table and eat essentially the same thing." |
| P5 | Parents actively patch nutritional gaps with hacks and supplements | Research shows parents adding `Pediasure`, milkshakes, multivitamins, and "sneaky" protein strategies |
| P6 | Parents escalate from "it will pass" to anxiety about growth and professional help | "People kept telling me he'd grow out of it, but it doesn't seem to be happening." |

---

## 5. Solution

### 5.1 Core Concept
FridgeKid uses the food already in the home as the starting point. It connects to a smart fridge or fridge-adjacent inventory source, detects what is available, and gives parents:

- one practical meal idea for tonight
- a kid-focused adaptation of that meal
- a lightweight weekly nutrition snapshot for each child
- a short shopping-gap list to make next week's meals easier

The core promise is not precision nutrition. The core promise is reduced household friction.

v1 scope decision:
- v1 supports compatible smart-fridge integrations only.
- Fridge-adjacent fallback modes may be explored later, but they are not part of the launch scope for this PRD.

### 5.2 Key Principles
1. **No manual logging as the default path.** The product should avoid the failure mode described in research: "Writing everything down was a pain and never stuck."
2. **Meal planning must account for reality, not ideal behavior.** The product must work even when the household relies on repetition, safe foods, or backup options.
3. **One meal, configurable plates.** The system should optimize for shared base meals with kid-specific adaptations.
4. **Positive guidance over guilt.** Parents are already anxious; the app should highlight what is covered and what one next step would help.
5. **Support workarounds parents already use.** Examples from research include batch freezing, protein drinks, ChatGPT for ideas, and repeating the same limited meals.

### 5.3 Product Non-Goals
- FridgeKid does not attempt to prove exactly what a child ate.
- FridgeKid does not replace pediatric or dietitian advice.
- FridgeKid does not solve severe feeding disorders in v1.
- FridgeKid does not optimize for grocery commerce, recipe discovery breadth, or adult nutrition tracking.

---

## 6. Features

### 6.1 MVP Features (v1.0)

#### F1 — Passive Fridge Inventory
- App connects to a compatible smart fridge
- Inventory updates automatically when the source reports a change
- Parent can review and correct items when needed
- Manual correction is available, but not required for normal use
- v1 must clearly show when inventory is current, stale, or uncertain
- v1 launch requires support for at least one production-grade smart-fridge integration

Why this exists:
- Research consistently shows parents will not sustain a logging-heavy workflow

#### F2 — Child Profiles
- Parent creates one or more child profiles
- Each profile stores age band and household food restrictions
- Profile output is practical and parent-readable, not medical
- Nutrition logic should remain high-level: food groups and common nutrient coverage, not obsessive calorie math
- v1 child profile fields are limited to: name, age band, household restrictions, and optional nickname/avatar
- Weight, calorie goals, and percentile tracking are excluded from profile setup

Why this exists:
- Parents in the research worry about growth, protein, and nutritional gaps, but they are not asking for clinical dashboards

#### F3 — Daily Meal Suggestion Card
- Home screen shows a simple meal suggestion based on what is already available
- Each suggestion includes:
  - meal name
  - estimated prep difficulty
  - why it is being suggested
  - kid adaptation or "safe food" variation
- Suggestions should favor meals that reduce the chance of cooking multiple dinners
- Home screen should show 1 primary suggestion and up to 2 alternates
- Each suggestion must be explainable from visible inventory plus child-profile logic; no black-box recommendations

Research grounding:
- Parents repeatedly ask for meals that work across allergies, picky eating, and family constraints

#### F4 — Nutrition Gap Snapshot
- Weekly view of broad nutrition coverage for each child
- Framed as "covered," "could use support," or "not enough home data"
- Never framed as diagnosis
- Snapshot is based on meals the app can reasonably infer or that the parent confirms
- v1 snapshot is limited to broad food-group and common nutrient guidance; it must not imply clinical completeness

Research grounding:
- Parents are using multivitamins, `Pediasure`, and "sneaky" nutrition hacks because they lack confidence in what is covered

#### F5 — Shared Household View
- Multiple caregivers can access the same household inventory, suggestions, and child profiles
- Supports one-home and multi-home family setups
- Multi-home support in v1 is limited to shared read/write access for the same household; merged cross-household nutrition history is out of scope until technically validated

Research grounding:
- Meal planning breaks when multiple adults, households, and schedules are involved

#### F6 — Shopping Gap Fill
- Weekly list of a small number of items that would improve meal flexibility or nutrition coverage
- Prioritizes realistic additions, not idealized pantry overhauls
- Example logic: suggest one protein, one produce item, and one flexible base ingredient
- v1 list is informational only; no direct grocery checkout integration is required for launch

Research grounding:
- Parents want fewer decisions and are already improvising with limited repeat meals and supplements

### 6.2 Explicitly Excluded from v1
- Calorie counting for children
- Weight tracking for children
- Competitive streaks, points, or guilt-based gamification around eating
- Clinical feeding-disorder treatment workflows
- Open-ended AI recipe generation without curation
- Full grocery marketplace platform
- Adult-first macro tracking
- Camera-based fallback inventory capture for non-smart-fridge households
- Cross-household merged meal history
- School-lunch, daycare, or restaurant meal tracking

---

## 7. User Experience

### 7.1 Onboarding (target: simple and fast)
1. Connect household inventory source
2. Add child profile(s)
3. Confirm what the system sees in the fridge
4. View first suggested meal and weekly snapshot

Onboarding principle:
- The process should feel lighter than starting a baby-tracking app or manual food journal

Launch requirement:
- If the user cannot connect a supported fridge during onboarding, they cannot proceed into the full v1 experience. A waitlist or "unsupported device" flow is acceptable; a partial fallback mode is not part of launch scope.

### 7.2 Daily Flow
- Parent opens app
- Sees one suggested meal and one lightweight snapshot
- Can optionally view alternatives
- At end of day, app can ask for a lightweight confirmation if confidence is low

Daily-flow principle:
- The app should reduce decisions, not create a new nightly task

### 7.3 Design Constraints
- Home screen should stay focused on one primary action
- No cluttered dashboards
- Language should be plain and reassuring
- Any corrective workflow should be optional and lightweight
- Home screen should contain no more than 3 primary interactive actions
- Any inventory correction action should be reachable within 2 taps from home

Research grounding:

> "Writing everything down was a pain and never stuck."

### 7.4 Notification Strategy
- At most one core meal suggestion notification per day by default
- Notifications should be framed as help, not guilt
- If the parent ignores notifications repeatedly, frequency should decrease automatically
- No wording that implies failure, neglect, or deficiency

Research grounding:
- Parents in the research are already stressed, frustrated, and often feel judged

---

## 8. Technical Requirements

### 8.1 Fridge Integration & Partnership Prerequisites
- v1 requires at least one working integration with a compatible smart fridge
- Commercial/API feasibility must be validated during discovery
- If direct smart-fridge integration is not viable, v1 should not proceed to full build under this PRD; the team should write a revised PRD for an alternate inventory approach

Open technical fact:
- The research in `research/` does not contain verified OEM/API details, so no API claims are included here without further validation

### 8.2 Computer Vision
- Inventory detection should be good enough to support meal suggestions and weekly nutrition summaries
- Low-confidence detections must be shown for review instead of being silently treated as truth
- The system must clearly distinguish between:
  - known item
  - possible item
  - no reliable read
- v1 acceptance criterion: the team must define and approve an internal confidence threshold before beta; the threshold must be visible in QA and analytics tooling

Requirement principle:
- Wrong data is worse than incomplete data when parents are already anxious about nutrition

### 8.3 Minimum Device Requirements
- Mobile app device requirements are TBD during technical discovery
- If passive recognition requires newer devices, the product must still offer a reduced but usable experience on older devices

### 8.4 Nutrition Data
- Nutrition logic must be based on a credible public nutrition data source and age-appropriate pediatric guidance
- All child-facing nutrition interpretation must be reviewed by a qualified pediatric nutrition expert before launch
- The app should provide broad coverage guidance, not claim precise dietary completeness
- Clinical review is a launch gate, not a follow-up task

Research grounding:
- Parents are looking for confidence and direction, not medicalized scoring

### 8.5 Platform
- v1 platform strategy: mobile app
- Web is out of scope for v1 unless required for caregiver account management

### 8.6 Meal Inference Model
- The system should infer likely meals from inventory changes and time-of-day context
- When confidence is low, it should ask for a lightweight confirmation
- Parent overrides must always be available
- The system should prefer being approximately useful over pretending to know exactly what a child consumed
- v1 launch requires an auditable event trail for inferred meals, confirmations, rejections, and overrides so the team can debug trust failures during beta

### 8.7 Sync Architecture
- Household data must sync across caregivers
- Product should acknowledge the multi-household problem in research, but v1 will not promise merged cross-household state until it has been validated in discovery
- Offline behavior should preserve the last known household state and suggestions

### 8.8 Privacy & Compliance
- Child data must be handled as sensitive
- Parents must control profile creation, deletion, and exports
- The product must avoid collecting unnecessary child data
- Any image handling or inventory detection must follow privacy-by-default principles

---

## 9. Competitive Landscape

| Product / workaround | What it does | Gap |
|---|---|---|
| Manual tracking / notes | Parent records food intake by hand | Research shows it does not stick |
| ChatGPT meal planning | Generates meal ideas on demand | Still requires the parent to translate ideas into household constraints |
| Supplements and protein hacks | Patches nutritional gaps | Does not solve dinner planning or food variety |
| Freezer-batch / meal rotation systems | Reduces planning overhead | Works, but does not provide nutrition visibility |
| Self-built tracking app | Removes some logging pain for one parent | Not broadly available, still needs productization and trust |

**FridgeKid's unique position:** It combines household inventory, kid-specific meal planning, and low-friction nutrition visibility in one parent workflow. The product is not trying to be a calorie tracker or recipe database. It is trying to reduce family food friction.

---

## 10. Risks & Mitigations

| Risk | Likelihood | Mitigation |
|---|---|---|
| Smart-fridge integration is too narrow or too difficult for v1 | High | Validate integration feasibility early; define fallback inventory path before committing full build |
| Inventory detection is inaccurate enough to break trust | High | Make low-confidence states explicit; require confirmation when uncertain; never hide uncertainty |
| Product becomes another admin tool instead of a relief tool | High | Keep manual logging optional; keep home screen simple; optimize around the meal suggestion card |
| Parents expect clinical accuracy | Medium | Explicitly frame product as household guidance, not diagnosis or treatment |
| Picky-eater households still cannot use suggestions | High | Build kid adaptations and safe-food variations into every meal suggestion |
| Multi-household family logistics are too messy for a single workflow | Medium | Limit v1 to single-household state; treat cross-household support as a follow-on problem unless discovery proves otherwise |
| Parents feel judged by nutrition messaging | Medium | Use positive, practical language only; no guilt framing |
| Stakeholders widen v1 beyond what research supports | High | Keep v1 narrowly focused on inventory, suggestions, and snapshot; require PRD revision for new workflow categories |

---

## 11. Open Questions

| # | Question | Owner | Deadline |
|---|---|---|---|
| OQ1 | Which supported smart-fridge integration will be the launch integration for v1? | Product + Engineering | Discovery |
| OQ2 | How much nutrition precision is useful before it becomes overwhelming or misleading? | Product + Clinical advisor | Discovery |
| OQ3 | What is the right unit of guidance: nutrient-level, food-group-level, or hybrid? | Product + Clinical advisor | Discovery |
| OQ4 | How should the app represent meals eaten outside the home without creating guilt or bad data? | Product + Design | Discovery |
| OQ5 | What should the paid tier include that clearly saves parent effort without bloating the product? | Product | Discovery |
| OQ6 | What exact beta success thresholds will determine whether the inventory-to-meal loop is strong enough to continue? | Product + Engineering + Design | Before beta |

---

## 12. Milestones

| Milestone | Target | Notes |
|---|---|---|
| Confirm launch smart-fridge integration feasibility | Phase 1 | Hard gate before full build |
| Engage pediatric nutrition reviewer | Phase 1 | Launch gate |
| Prototype inventory-to-meal suggestion flow | Phase 1 | Must prove low-friction value |
| Define v1 beta success thresholds | Phase 1 | Needed before beta recruitment |
| Prototype weekly nutrition snapshot | Phase 2 | Must stay simple and non-clinical |
| Test with parents matching research profiles | Phase 2 | Especially picky-eater households |
| MVP build | Phase 3 | Mobile only; supported smart-fridge households only |
| Closed beta | Phase 4 | Measure stress reduction, trust, and repeated usage |
| Launch go / no-go review | Phase 5 | Based on beta learnings, trust metrics, and technical feasibility |

---

## 13. References

- [research/pain-points.md](/Users/supriyarajeev/Documents/Claude%20folder/Training%20-%20April/research/pain-points.md)
  - Reddit, r/iosdev, February 26, 2026 — manual logging pain and self-built photo nutrition app
  - Reddit, r/blendedfamilies, February 26, 2026 — meal planning chaos across custody schedules
  - Reddit, r/ParentingADHD, February 14, 2026 — one child's rigidity controlling family meals
  - Reddit, r/workingmoms, October 11, 2025 — wish for one shared family meal across constraints
  - Reddit, r/Parenting, November 25, 2025 — supplements and "sneaky" protein workarounds
  - Reddit, r/Parenting, March 23, 2025 — escalation from waiting it out to multivitamins and professional help
