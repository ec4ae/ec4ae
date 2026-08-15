# LockedIn: Startup Strategy & Product Design

## Thesis

The wedge is certification-exam candidates — CPA first — not "everyone with a goal." The core insight: accountability apps don't die from lack of motivation, they die because a broken streak currently has no product response except silence and shame, and the fix is a rolling reputation score plus human pod-nudges instead of app-triggered guilt. That part of the brief is sound and I'm keeping it. The rest of the brief, as written, is over-scoped, under-skeptical about the economics, and leaning on a moat ("Lock Score as portable external reputation") that is speculative, not established — nobody outside the app has a reason to trust it yet, and may never. The single biggest risk to this company is not a competitor copying the feature list. It's building all eleven features in the brief, none of them well, while the two things that actually matter — a genuinely non-punitive daily loop and enough cohort density for pods to fire reliably — are still half-finished eighteen months in. Cut first. Read on for exactly what I'd kill and why.

## Three Things Wrong With the Brief Before We Go Further

**The name is a liability, not a feature.** "LockedIn" sitting one keystroke from "LinkedIn," in the same category (professional/personal development, social, reputation-scored), is not a cute homage — it's a trademark collision waiting to happen, and Microsoft's legal team does not need to be creative to see it. This needs a trademark clearance check before a single dollar of brand-building spend, and honestly a fallback name should be scoped now, not after a cease-and-desist. Riding "lock in" slang is also borrowing equity from a meme with an unknown half-life — memes that make it into Dictionary.com shortlists are often already past peak. Don't build the five-year plan on the assumption the name ages well.

**The feature list is a five-company roadmap, not a v1.** Goal Profiles, check-ins, pods, leaderboards, coaches, Lock Score, AI Coach, six integrations, a matching marketplace, challenges, a feed, and gamification-with-cosmetics is what Strava (14 years old), Discord (11 years old), Duolingo (14 years old), and LinkedIn (23 years old) collectively ship today, not what a pre-launch company builds in year one. If the plan is "build most of this in the first 9 months," the plan is wrong, and I'm cutting harder below than the brief's own framing invites.

**"Operating system for self-improvement" is the kind of phrase that should trigger suspicion, not ambition.** Almost every consumer platform pitch reaches for "operating system for X" once it wants to sound bigger than it is — it's a positioning statement, not a strategy, and it's freely substitutable with "operating system for productivity," "for wellness," "for career," none of which would change a single downstream decision in this doc. I'm keeping it in Tier 4 because a five-year horizon is asked for, but nothing in Tier 1-3 should be built to serve that phrase. Build the CPA-candidate accountability tool. The platform narrative is a story you get to tell later if the data earns it, not a design constraint now.

---

## Strategic Questions

### 1. The Wedge

"Everyone with a goal" fails for the reason every general-purpose accountability app has failed (Coach.me, Habitica, StickK, Way of Life, all flat or dead): goals are heterogeneous, so the feed is incoherent, the social graph never densifies, and there's no shared vocabulary for what "good" looks like. Network effects need homogeneity at launch.

**Candidates considered, and why I'm rejecting the obvious one:**

- **Fitness/physique transformation.** The intuitive choice — 75 Hard already went viral for free, Strava proved willingness to pay for verified fitness data. Reject it as the *first* wedge: Strava, Whoop, and Oura already own verified fitness data and are extending into social themselves, so you'd be entering the hardest-defended part of the market first, with the weakest cohort structure (everyone's on their own timeline, no shared deadline forces synchronized engagement).
- **Certification exams (CPA, Bar, USMLE, CFA).** Hard external deadline nobody can opt out of. Existing spend is already enormous and already proves willingness to pay for structure: Becker/UWorld CPA review runs $2,000-3,000, so a $15-25/month accountability layer is a rounding error against what candidates already spend, not a new category of spend they have to be convinced to open up. Candidates already self-organize into dense communities — r/CPA (90k+ members), r/Mcat (200k+) — running the exact behavior this product formalizes, manually, in spreadsheets and megathreads, for free. Cohorts are naturally time-boxed by real exam windows, giving a season structure the product gets for free instead of having to invent. The honest downside: this is a structurally smaller population than fitness, and every graduating cohort *leaves* — churn here isn't a failure mode to fix, it's baked into the wedge, and the business model has to account for that from day one, not discover it in year two.

**Choice: CPA candidates first**, Bar and USMLE as fast-follow cohorts 2-3 (same deadline/spend/community-density profile, near-zero product rework), fitness deferred to phase 3+ once Lock Score has real longitudinal data to make cross-domain reputation meaningful rather than fake.

**What I'd bet on:** cohort density beats addressable market size at launch — 5,000 CPA candidates synchronized around four real exam windows a year beats 50,000 scattered "self-improvement" users with nothing in common.
**What would kill this:** if the willingness to pay doesn't transfer from *content* (Becker, a product that visibly produces exam-relevant material) to *accountability* (LockedIn, a product that produces structure around material you already have). These are different value propositions and the brief conflates them. Test this with a $9 paid beta — real money, not a survey — before writing another line of code.

### 2. The Retention Death-Spiral

This is the right question to center everything on, and it's the one part of the brief I'd defend without softening. The mechanism: miss a day → app shows a broken streak/red X/declining chart → user feels judged by their own tool → user avoids the app to avoid the feeling → absence compounds → uninstall. Duolingo's streak-freeze is a partial answer built for trivial stakes (missing a vocab day); it doesn't scale to "I might fail the CPA exam again."

**The fix, concretely, not aspirationally:**

- No red X, no "streak lost" screen, no declining line chart as primary UI. A miss renders as a neutral gap, the way a rest day looks on a calendar — not a strikethrough.
- **Lock Score is a rolling 90-day weighted average, not a consecutive-day counter.** One missed day costs a few points, not the whole history. This is a math decision, not a copy decision — it has to be built into the scoring function from the start, because retrofitting it after users have learned the counter resets is a much harder trust repair.
- **Miss handling is delegated to a human, not the app.** The worst possible move is a push notification from LockedIn itself saying "you broke your streak." Instead, one specific pod partner gets "Sam missed today — send a nudge," and a human does the re-engagement. A message from a real person has meaningfully higher reopen rates than a generic push (~3-5% CTR is the typical push benchmark per Braze/OneSignal data; a DM from someone you know is a different order of magnitude) — but this mechanism is *entirely dependent* on pods being dense enough to have someone to nudge, which does not exist on day one. Flag this dependency now: this retention fix does not work for a user with no pod, and a meaningful fraction of early users will have no pod. Don't let this section's confidence paper over that gap — see Cold-Start below.
- Levels and streaks only move up or hold, never demote. No leaderboard drop mechanics.
- A user who returns after 3+ days off gets a neutral, non-cringe welcome-back state, not a wall of missed check-ins to confront.

**What I'd bet on:** the human pod-nudge, not the removal of punitive UI, is the actual retention mechanism — softening the UI prevents active harm, but only a real person reaching out reliably reverses the death spiral.
**What would kill this:** thin pods. If cohort density is weak at launch, a broken-streak user has no nudge partner, the safety net doesn't exist, and this entire section is theory, not product. This is a hard dependency on Q4, not a parallel workstream — sequence accordingly.

### 3. Why Now

- **Cultural:** "lock in" crossed from niche slang to mainstream Gen Z usage in 2023-2025. Real tailwind, real risk: slang fades, and I've already flagged the name risk above. Don't confuse a naming-trend tailwind with a durable strategic asset.
- **AI coaching got cheap.** Cost per LLM interaction has fallen roughly two orders of magnitude since 2022-era models, which is what makes "AI coach in the loop" gross-margin-positive at a $15-25/month price point for the first time. This is real and worth building on — but be honest that "AI coach" is now a checkbox every consumer app ships, not a differentiator on its own. It's necessary infrastructure, not the moat (more on this under Defensibility).
- **Wearables/integrations are default infrastructure now**, not early-adopter novelty, which is what makes low-friction auto-verification plausible without asking users to do anything new.

**What I'd bet on:** the cultural wave buys 12-24 months of favorable brand attention that a generic "habit tracker" positioning wouldn't get.
**What would kill this:** treating the cultural wave as durable. It isn't. If the product's actual mechanics (Lock Score, pods) aren't strong enough to carry the brand once "locking in" stops being a thing people say, the company has a naming problem and a substance problem at the same time.

### 4. The Cold-Start Problem

Single-player value has to work with zero friends — if the app needs a pod to be useful on day one, it's a ghost town at launch, full stop. The Goal Profile + check-in + AI Coach loop must beat a private journal or a Notion template standalone before any social feature is switched on.

**Bootstrap plan:**

- Recruit directly from r/CPA, r/Mcat, Bar-prep Discords — communities already running this behavior manually, unpaid, in a worse tool. This is the strongest cold-start signal available: you're not creating demand, you're productizing an existing one.
- Ship pre-built Season cohorts pegged to real exam windows so the first 1,000 users are pre-grouped by shared deadline, not left to organically add friends — organic friend-adding is the reliable failure mode of every Discord-clone accountability app that's tried this.
- Creator partnerships with mid-size (10k-200k subscriber) CPA/Bar-prep YouTubers/TikTokers, not celebrity-tier — this audience trusts creator recommendations over paid social at a level generic productivity-app advertising doesn't get. Target CAC in the $8-20 range; generic paid social in this category typically runs $40-80+.
- Founder-led manual pod matchmaking for the first 20-30 pods. Do not trust an algorithm with a thin user base — an algorithm needs density to be good, and it doesn't exist yet. This is a real operational cost (someone's job for months), budget for it as headcount, not as a feature.

**What I'd bet on:** the single-player loop has to be sellable on its own — if it isn't, the whole cold-start plan collapses back into needing network effects before revenue, which is a much slower and riskier path.
**What would kill this:** if the AI Coach's solo value is indistinguishable from a good ChatGPT prompt, nobody pays for LockedIn standalone, and you're stuck needing the social layer to justify the price before the social layer has any density to justify anything.

### 5. Defensibility — the weakest section of the brief, treated with appropriate skepticism

Every individual feature here is copyable in two quarters by a funded team. That's correctly diagnosed in the brief. Where I disagree with the brief is the confidence it places in "Lock Score as portable reputation" as *the* moat. Walk through what that claim actually requires: a credit score is trusted because lenders — third parties with money on the line — decided to rely on it, over decades, backed by regulation. A Lock Score is trusted by nobody outside the app until some external party (an employer, another platform) decides to grant it that status, and there is no product mechanism in this doc that makes that happen. It's a hoped-for outcome, not a built one. Calling it "the moat" today overstates what exists; the honest version is "a candidate moat, contingent on 18+ months of clean data *and* a deliberate, currently-unplanned effort to get a third party to care about it."

What's actually defensible *today*, without a future third-party bet:

- **Verified longitudinal data that can't be backdated.** Whatever it's used for, a competitor cannot manufacture your users' 18 months of history. This is real and time-compounding regardless of whether anyone external ever trusts the score.
- **Relationship density inside a specific pod.** The 5-8 people who got someone through a 10-week Bar-prep sprint are a switching cost a feature clone can't replicate, because it's relational, not featural. This is closer to LinkedIn's actual moat (your specific network) than to a reputation-score moat, and it's more defensible.
- **Why Strava/LinkedIn can't trivially bolt this on:** Strava's data model and audience are built around discrete athletic activity — retrofitting "pass the CPA exam" is a data-model rewrite with no matching demand from their existing users. LinkedIn's moat is real-name professional identity, which is structurally hostile to the vulnerable, day-47-relapse honesty this product depends on — nobody posts "I fell behind this week" where their employer can see it. Both of these are real structural barriers. Neither protects the "portable reputation" claim; they protect the data-and-relationship moat instead.

**What I'd bet on:** relationship density plus non-backdatable data compound into a real moat without needing anyone's cooperation. Treat that as the actual moat in every internal document.
**What would kill this:** spending years chasing external Lock Score adoption (employer partnerships, credentialing deals) before the data or relationship moat is strong enough to matter on its own — that's optimizing for a speculative payoff at the expense of the one that's actually in your control.

### 6. The Billion-Dollar Math — run with real skepticism, not favorable comps

Working back from a $1B outcome at an 8-12x ARR multiple: $85-125M ARR required.

| Revenue Stream | Realistic Assumption | Scale Required | Verdict |
|---|---|---|---|
| Consumer subscription | Habit and accountability apps convert free users to paid in the low single digits typically, and even Duolingo — the best-in-class comp, 14 years and $180M+ of funding in — converts roughly 7-8% of MAU to paid, at a blended ARPU closer to $35-40/yr, well below its sticker price. Assume LockedIn does *better* on ARPU (higher-intent, higher-spend audience) but do not assume better conversion — a certification candidate's free alternative (Reddit, Discord, a spreadsheet) is genuinely good, not a strawman. | ~400-500k paying subscribers at ~$200-220/yr blended, which at a 5-8% conversion rate implies **5-8M+ total registered users** in the wedge-and-adjacent cohorts before this line alone carries the business | **Load-bearing, but the required top-of-funnel is much larger than the wedge (CPA candidates number in the low hundreds of thousands total in the US per year) can supply alone.** This is the single most important number in this document: the CPA/Bar/USMLE wedge, even fully saturated, likely cannot produce enough registered users to hit this on its own. The subscription line only works at this scale if phase 3-4 expansion (fitness, general self-improvement) actually happens and actually converts — which is a bet on execution 3+ years out, not a launch-year fact. |
| Coach/expert marketplace | 15-20% take rate, comparable to Patreon/Substack | Needs thousands of active paying coaches and real GMV — a multi-year build requiring the reputation system to already be trusted, which Section 5 just established is not guaranteed | **Real secondary line, not a rescue plan if subscription underperforms** |
| B2B/credentialing partnerships | $50-200k per enterprise deal | 100-300 deals for $15-30M | **Contingent on the speculative external-trust bet in Section 5 actually landing. Do not put this in a year-1-3 plan.** |
| Cosmetics/IAP | $1-3/mo among a minority | — | **Rounding error, correctly deprioritized. Don't let a growth team chase this for a vanity DAU number.** |

**The honest read the brief doesn't say out loud: this may not be a billion-dollar business on the CPA/Bar/USMLE wedge alone.** The wedge is right for cold start and for proving the mechanics cheaply and credibly. It is very likely too small, by total population, to be the whole business. The billion-dollar outcome — if it exists — requires the phase 3-4 expansion into fitness and general self-improvement to work, at Duolingo-or-better conversion economics, which is a real bet with real execution risk, not a rounding detail to mention once and move past.

**What I'd bet on:** price at $15-25/mo (anchored against the $2-3k prep-course reference price, not against $5 habit-app comps) and treat the wedge explicitly as a proof-of-mechanics phase, not the revenue plan — say this internally so nobody is surprised in year 2 when CPA-alone growth plateaus.
**What would kill this:** believing the wedge is the business. It's the beachhead. If the team optimizes for maximizing CPA-cohort revenue instead of proving the mechanics fast enough to expand on schedule, the company tops out as a profitable niche product, not a venture-scale outcome — which might genuinely be the right choice, but it should be a deliberate choice, not a surprise.

### 7. The Wellbeing Tension

Real constraint, correctly flagged in the brief. Leaderboards + discipline framing + a reputation score, unmitigated, is a toxic-productivity machine, and it sits in direct tension with any user using this for mental health or recovery goals.

**Lines drawn, not suggestions:**

- Leaderboards are pod-scoped and opt-in by default, globally off by default, and *hard-disabled* — not just default-off, actually unavailable regardless of user preference — for any goal tagged health/recovery. This is a product-level rule the user cannot override, because the burden of protecting a vulnerable user from a bad setting choice shouldn't sit with that user.
- Rest and planned recovery are first-class states, logged distinctly from a missed day. The AI Coach is required, not merely encouraged, to recognize compulsive check-in patterns (multiple check-ins a day, escalating frequency inconsistent with the stated goal) and respond with a prompt toward rest — this is a hard requirement in the system prompt/guardrails, reviewed like a safety spec, not a nice-to-have copy tweak.
- Public shaming of a lapsed pod member is a bannable moderation offense from day one, not a "discouraged" community guideline.
- **North-star metric is return-after-lapse rate, not streak length or notification CTR.** This is the one line item in this whole document I'd insist on being non-negotiable, because it's the metric choice that prevents a growth team in year 2 from quietly re-deriving Duolingo's owl-notification aggression under revenue pressure. If leadership won't commit to this metric in the actual OKRs, the wellbeing section is marketing copy, not product truth, and I'd say so directly to the team before launch.

**What I'd bet on:** making return-after-lapse the metric the growth team is compensated against, not just a value statement in a deck — metrics that don't touch comp don't survive a hard quarter.
**What would kill this:** the entirely predictable failure mode where a VP of Growth two years in proposes "just a little more notification volume" to hit a DAU target, and nobody in the room remembers this section exists. Write the metric into the actual OKR doc now, not just this strategy doc.

---

## Tier 1 — Strategy

### Vision & Mission

**Vision:** the platform where real, verified effort toward a goal accumulates into a record credible enough to matter — eventually. Not a launch-year claim; see Tier 4.

**Mission (what actually launches):** give certification-exam candidates a daily accountability system where a bad day makes them more likely to come back, not less, starting with CPA candidates.

### Wedge and Expansion Sequence

| Phase | Cohort | Why This Order | Unlocks |
|---|---|---|---|
| 0 (Beta, 0-3mo) | CPA candidates | Proven spend, hard deadline, dense free communities to recruit from, natural season structure | Tests willingness to pay for accountability layered on existing prep spend — the load-bearing assumption in Section 1 and 6 |
| 1 (3-9mo) | + Bar, USMLE | Same structural profile, near-zero product rework | Proof the model generalizes past one exam type |
| 2 (9-18mo) | + coding bootcamp job search, CFA | Same deadline-driven structure; GitHub integration becomes genuinely useful | First real use of the matching marketplace (deferred until now, see Tier 2) |
| 3 (18-30mo) | + fitness transformation | Only once Lock Score has 18+ months of real cross-domain data — otherwise this cohort dilutes the reputation signal instead of strengthening it | This is the phase the billion-dollar math in Section 6 actually depends on — treat it as the real second act, not a footnote |
| 4 (30mo+) | + general self-improvement | Platform narrative becomes earned, not asserted | B2B/credentialing lines become plausible, per Section 5's caveat |

### Personas

**Priya, 26, CPA candidate, second attempt at FAR.** Fear: failing again, burning the $3,000 already spent on Becker, and having to explain a second failure to her firm. Would quit LockedIn instantly if it feels like performing for an audience rather than a private tool that helps her pass — zero tolerance for productivity-influencer aesthetics.

**Marcus, 34, engineer returning to competitive lifting after a 3-year injury layoff, also shipping a side project.** Fear: re-injury, and more quietly, being compared against people who never took a break. Would quit if a leaderboard puts his comeback next to someone else's uninterrupted progress and makes it look like mediocrity — the exact scenario pod-scoped-not-global leaderboards exist to prevent.

**Danielle, 41, outpatient treatment for alcohol use disorder, using check-ins alongside a therapist.** Fear: relapse becoming visible, and a broken streak actively harming her recovery rather than supporting it. For this persona, punitive streak UI isn't a retention bug, it's a harm vector — she should be the standing reference case in every product review that touches gamification, not an edge case remembered only when someone raises it.

### Competitive Teardowns

| Platform | Steal | Exploit |
|---|---|---|
| **LinkedIn** | Verified-credential trust shorthand | Its status-signaling culture makes it structurally unable to host honest "I fell behind" content — nobody posts that where their employer can see it |
| **Instagram** | Low-friction ephemeral content creation | Rewards appearance over substance; we make the feed structurally incapable of rewarding a good photo with no verified progress behind it |
| **Strava** | Auto-verification via integrations, lightweight social proof | Single-domain (athletic), no cross-domain reputation, no structure for career/financial/exam goals |
| **Discord** | Persistent small-group spaces, real-time chat | Zero structure — no tracking, no verification, no reputation; accountability servers today are just chat with manual self-report |
| **Reddit** | Deep self-organization around high-stakes goals, anonymity for vulnerable disclosure | No persistence — a "Day 47" post scrolls away in 24 hours with no cumulative record |
| **Duolingo** | Streak-freeze forgiveness mechanics, low-friction daily habit design | Notification aggression works because failing to learn Spanish today is low-stakes; failing to study for the Bar is not — steal the forgiveness math, reject the nagging |

### Monetization Strategy

See Section 6. Subscription is load-bearing but the wedge alone likely can't supply enough volume to hit venture-scale numbers — say so internally, plan phase 3-4 expansion as the actual second act, not an afterthought slide.

### Go-to-Market & Viral Growth Loops

- **Cohort-seeded virality:** productize the megathread — pre-built Season cohorts timed to real exam windows, seeded via creator partnerships, letting existing community density do the inviting (a Becker study group of 8 migrating together beats 8 individually-acquired users).
- **Lock Score as a shareable, factual credential** ("127-day verified CPA study streak, 94% MCQ accuracy trend") — closer to a Strava activity share or a GitHub contribution graph than an Instagram highlight, both of which have proven durable, non-cringe sharing behavior.
- **Coach-led acquisition** once the marketplace exists (deferred, see Tier 2) — a coach with an existing audience becomes a channel, Substack/Patreon-style.

| Risk | Mitigation |
|---|---|
| Cohort graduates and churns structurally | Explicit alumni status — graduates become marketplace coaches for the next cohort, converting structural churn into supply |
| Naming/trademark collision with LinkedIn | Clear trademark before spend; have a fallback name scoped, not discovered under legal pressure |
| Wedge population too small to hit venture-scale numbers on its own | Treat phase 3-4 expansion as the real second act and fund/plan it accordingly, don't discover the ceiling in year 3 |
| Verification gamed (fake health data, staged photos) | Multi-source cross-verification, no single self-report point counts fully toward Lock Score |
| Growth pressure pushes toward Duolingo-style notification aggression | Return-after-lapse in the actual OKRs, tied to comp, not just this doc |
| Better-funded competitor copies the feature surface | Moat is data-and-relationship density (Section 5), not features — respond by deepening cohorts, not by racing to out-feature them |

---

## Tier 2 — Product

### Prioritized Feature List: Build / Defer / Kill

I'm cutting harder than the brief's own framing invites, because "everything at once" is the actual biggest execution risk in this document.

| Feature | Decision | Why |
|---|---|---|
| Goal Profiles | **Build now** | Core primitive, nothing else works without it |
| Daily check-ins (photo/video/voice/timer) | **Build now**, manual + basic photo only; deep auto-verification is separate line below | Core loop |
| Accountability Pods (5-8 people, chat) | **Build now**, platform-seeded per Season cohort, not user-organic at launch | Load-bearing for the entire retention thesis in Section 2 |
| Pod leaderboards | **Build now**, opt-in, pod-scoped, hard-disabled for health/recovery goals | Needed for the accountability mechanic; the wellbeing constraint is not optional |
| Pod video/voice calls | **Kill for v1, revisit in v2 only if pod chat usage justifies it** | Expensive engineering for unproven demand; the brief lists this casually, it isn't casual to build reliably |
| Coach/expert marketplace | **Kill until Lock Score has real data (post-cohort-2, ~12-18mo)** | Launching a marketplace with no trust signal is an unverified Fiverr clone with extra branding — worse than not having one |
| Lock Score | **Build now**, deliberately simple (consistency + basic verification tiers only) | Must start accumulating data day one; the sophisticated anti-gaming version is a v2 problem, don't gold-plate this before there's data to protect |
| AI Coach | **Build now, narrow** — check-in feedback and basic lapse-pattern flags only | This is infrastructure, not differentiation (Section 3) — don't let it eat a disproportionate share of early engineering time chasing a "smart assistant" narrative |
| Integrations | **Build 2 at launch: Apple Health, exam-provider score import where available.** Everything else (Strava, GitHub, Duolingo, Kindle, Notion) **deferred** | The brief lists six; each is real integration-partner work, not a checkbox. GitHub earns its place in phase 2 when the coding cohort arrives, not before |
| Collaboration marketplace / AI matching | **Kill for v1-v2, revisit at phase 2** | Irrelevant to solo-studying CPA candidates; the brief treats this as core, it isn't for this wedge |
| Challenges (75 Hard-style) | **Build now, thin wrapper on existing Goal Profile primitives** | Cheap, high viral leverage, 75 Hard already has organic reach we can ride |
| Progress feed | **Build now, pod-scoped only, no global feed** | A global feed at launch with thin content density looks like a ghost town and actively damages first impressions |
| Gamification: XP/streaks/levels | **Build now**, redesigned per Section 2's anti-shame rules (never demote) | Core loop reinforcement |
| Cosmetics | **Kill for v1-v3** | Rounding-error revenue (Section 6), pure distraction from core loop polish |
| Global public leaderboards | **Kill, not deferred** | Directly contradicts Section 2 and Section 7; there is no version of this that's safe to ship later without redesigning it from scratch anyway |
| Cross-domain "everyone with a goal" matching/feed | **Kill until phase 3+** | Premature by the wedge logic in Section 1 — building this early actively undermines the cohort-density strategy |

### The Core Daily Loop

1. Optional morning prompt from the AI Coach, grounded in the Goal Profile — informational, not guilt-inducing.
2. Check-in: under 15 seconds for the common case. Friction here is the single highest-leverage UX metric in the product.
3. Specific, non-generic feedback tied to actual data ("94% today, up from 89% last week"), not templated praise.
4. Optional pod visibility, lightweight kudos/comments — never a public feed.
5. Lightweight end-of-day reflection (voice note or short text) — the qualitative, non-gameable signal.
6. Miss handling: no app-triggered notification. Pod-nudge queues for one partner the next morning (Section 2).

### Lock Score

**Inputs, rolling 90-day weighted window, not lifetime-cumulative:** check-in consistency (largest weight), verification tier of each check-in, trend direction on goal-specific metrics, pod engagement quality (nudging others counts, not just receiving), longevity (an older verified history weights more per data point than a recent burst).

**Explicitly not inputs:** follower count, likes/kudos received, pods joined, content production value, posting frequency independent of actual completion. This is the entire mechanism by which the score resists being a popularity contest — there is no term in the function for social approval.

**Verification tiers, highest to lowest trust:**
1. Third-party API-verified (Apple Health, exam-provider score import, later GitHub/Strava) — hardest to fake without faking the underlying real action.
2. Cross-corroborated self-report (photo + in-app timer + optional context).
3. Single-source self-report — counts toward consistency, contributes minimally to "verified achievement," and is transparently labeled as lower-tier so nobody can misrepresent it.

**Anti-gaming:** rolling window (not cumulative) kills the front-load-then-coast attack. Verification-tier transparency prevents misrepresenting self-report as device-verified. Anomalous spikes after long gaps soft-cap score growth pending sustained behavior — a throttle, not a ban.

**Why it resists popularity, and where the claim has to stay honest:** the scoring function structurally can't be gamed by social approval, because approval isn't an input. That's real. What it does *not* do, and what Section 5 already flagged, is make anyone outside the app trust the number — that's a separate, unsolved problem, and this section shouldn't be read as implying it's solved.

### AI Coach: Capabilities and Guardrails

**Capabilities at launch, deliberately narrow:** check-in feedback grounded in actual data trends; basic Goal Profile-grounded Q&A; lapse-risk pattern flags surfaced supportively ("want help getting back on track?" never "you're falling behind"); compulsive-check-in/overtraining pattern recognition with a mandatory prompt toward rest.

**Guardrails, non-negotiable:** never medical, legal, or financial advice beyond general encouragement — for recovery-tagged goals, explicitly logistical/supportive only (did you attend your session), with a hard prompt toward real professional resources when patterns suggest crisis, never an attempt to handle it in-app. Never guilt, shame, or comparison-to-others language — a content-policy constraint on the system prompt, not a style guideline. Never impersonates a human coach. Rate-limited to avoid the notification aggression flagged in Section 7.

### Community, Challenges, Moderation

Pods: 5-8 people, platform-seeded via Season cohorts at launch, chat only (no calls, see kill list above). Challenges: time-boxed programs (75 Hard-style) wrapping the Goal Profile primitive, primary vehicle for organic growth. Moderation: shaming a lapsed pod member is a bannable offense from day one, enforced with the seriousness of a harassment policy, not a footnote — report/mute/block tooling ships at launch given how vulnerable the check-in content can be (recovery, health, financial struggle).

### Matching Algorithm (Phase 2+, not before)

When cohort density supports it: shared goal category and timeline, complementary schedule, Lock Score tier (pairing wildly mismatched consistency levels produces frustration on one side and shame on the other — a direct Section 7 constraint on the algorithm design), and stated communication-style preference (tough-love vs. gentle — mismatched tone is a plausible churn driver, worth surveying explicitly at pod formation).

### Gamification and the Anti-Shame Model

XP and levels move up or hold, never down. Streak-freeze tokens (2-3/month, replenishing) borrow Duolingo's forgiveness math, paired with the rolling-window Lock Score so a fully-spent freeze still can't cause catastrophic score loss. Seasons tied to real exam windows reset Challenge/pod-cohort structures for a psychological fresh start, but never reset Lock Score itself — the moat depends on that data surviving every season transition.

### MVP → V5 Roadmap

| Version | Scope | Cohort |
|---|---|---|
| MVP (0-3mo) | Goal Profiles, manual + photo check-ins, consistency-only Lock Score, pre-seeded pods, narrow AI Coach, Apple Health only | CPA beta, ~1,000 users |
| V1 (3-9mo) | + verification-tier Lock Score, pod chat, Challenges, exam-score import | + Bar, USMLE |
| V2 (9-18mo) | + Coach marketplace (only once Lock Score has real data), richer AI Coach, anti-gaming sophistication | + Coding bootcamp, CFA |
| V3 (18-30mo) | + Matching marketplace, GitHub/Strava integrations, cross-cohort Lock Score comparability | + Fitness — the phase the billion-dollar math depends on |
| V4-V5 (30mo+) | + General self-improvement goals, employer API access to Lock Score (consent-gated), platform narrative earned by data, not asserted | General audience |

---

## Tier 3 — Design & Engineering

### Information Architecture

Today (check-in home, AI Coach) → Progress (Goal Profile detail, Lock Score trend) → Pod (chat, pod-scoped leaderboard) → Discover (Challenges, marketplace once it exists) → Profile (Lock Score summary, privacy controls). Flat, single-purpose-tab structure like Duolingo, deliberately not feed-first like Instagram — home screen answers "what do I need to do today," not "what is everyone else doing."

### Mobile Wireframes

- **Today:** planned check-ins as large tappable cards, generous whitespace; Lock Score as a calm trend line, not a gamified dial; one dismissible AI Coach message, never stacked.
- **Check-in flow:** single modal — select Goal Profile → capture → optional reflection → confirm. Under 15 seconds for the common case.
- **Progress detail:** milestone timeline, check-in calendar in neutral (not red/green pass-fail) coloring — gaps are visually quiet.
- **Pod screen:** chat is the dominant element; leaderboard is a collapsed, opt-in module at the top, intentionally under-emphasized relative to the brief's framing of leaderboards as a headline feature.
- **Profile/Lock Score:** Strava-activity-page-inspired — verified achievement history, levels, a factual/understated shareable card (not boastful) for the GTM loop.

### Desktop

Secondary at launch (mobile-first, matches check-in-heavy daily use). Serves coaches (V2+ dashboard for managing mentees) and Goal Profile planning, which benefits from more screen space than a phone check-in flow needs.

### Database Schema (high-level)

`users`, `goal_profiles` (user_id, category, target, timeline, visibility), `check_ins` (goal_profile_id, timestamp, verification_tier, source_integration, raw_data_ref, reflection_text), `lock_scores` (user_id, rolling_window_start, computed_score, component_breakdown — recomputed on schedule, stored historically for auditability, not overwritten in place), `pods`/`pod_memberships` (cohort_id, season_id), `integrations` (user_id, provider, oauth_token_ref, last_sync), `challenges`/`challenge_participants`, `coach_profiles`/`coach_programs` (V2+ only), `moderation_reports`. Verification provenance is stored explicitly throughout — required for the verification-tier system to be auditable, not a nicety.

### Technical Architecture & Stack

Boring, proven choices deliberately — the differentiation here is the data model and product decisions, not infrastructure novelty, so infra risk should be minimized, not explored. React Native (single codebase for platform parity), typed backend (Node/TypeScript) on Postgres (Lock Score computation is fundamentally relational aggregation), a job queue for async score recomputation and integration syncs, object storage for check-in media, a thin AI Coach service layer against a hosted LLM API rather than self-hosted models — unit economics work fine on API pricing at this scale, self-hosting is a distraction until volume justifies the operational overhead.

### Security & Privacy Model

Integrations pull the minimum needed for verification ("a workout occurred on this date matching this duration," not full raw health history), explicit revocable per-integration consent, clear user-facing explanation of what feeds Lock Score versus what's discarded. Sensitive goal categories (mental health, recovery, financial) get elevated default privacy — private-to-self or pod-only, never eligible for global leaderboard opt-in regardless of user preference, a hard product guardrail per Section 7, not left to settings literacy. Standard GDPR/CCPA-grade export/delete rights, honored fully even though the data moat depends on aggregate density — the moat is about platform-wide density and relationship depth, not about holding any individual user's data hostage, and it should never be designed to feel that way.

---

## Tier 4 — Horizon

### Five-Year Vision

Years 1-2: prove the wedge, prove return-after-lapse as the retention mechanism, prove willingness to pay at $15-25/mo — and be honest internally about whether the wedge alone is approaching the ceiling flagged in Section 6. Year 3: Lock Score has enough cross-domain longitudinal data that the "portable reputation" claim graduates from speculative to plausible — this is the actual inflection point, and it should be treated as unproven until it happens, not assumed. Years 4-5: if and only if that inflection lands, employer/institutional partnerships, a coach marketplace with real pricing power, and goal categories well beyond the original wedge become viable.

### The Path from "Study-Group App" to "Operating System for Self-Improvement"

The path runs through data and relationship density, not through building more features faster. Every new cohort adds to the same Lock Score graph, and the product's value compounds as that graph densifies — that's a real platform dynamic, and it's exactly why trying to be the "operating system" on day one (the everyone-with-a-goal trap this document opened by rejecting) would produce a shallow product with no cohort dense enough to prove any of it. CPA candidates first isn't a smaller version of the vision. It's the only sequence that has a chance of earning it — and "earning it" means the phase 3-4 expansion actually has to work, at real conversion economics, not just get mentioned in a five-year slide.
