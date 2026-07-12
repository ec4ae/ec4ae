# LockedIn: Startup Strategy & Product Design

## Thesis

LockedIn wins by refusing to be "the social network for everyone with a goal." The wedge is **exam-and-certification communities in defined cohorts** (CPA, Bar, USMLE, CFA, coding bootcamp job-search sprints) — populations with a hard deadline, brutal daily discipline requirements, pre-existing study groups, and money already being spent on prep. The core insight: accountability apps don't die from lack of motivation, they die because **a broken streak currently has no product response except silence and shame** — the single highest-leverage design decision in this doc is making the day after a miss the best-designed moment in the app, not the worst. The single biggest risk isn't competition, it's that the "Lock Score" reputation layer — the actual moat — takes 12-18 months of clean verification data to become meaningful, and LockedIn will be tempted to ship vanity gamification to fake traction before that data exists, at which point it's just Strava with worse network effects.

---

## Strategic Questions

### 1. The Wedge

"Everyone with a goal" fails for the same reason every general-purpose accountability app has failed (Coach.me, Habitica, StickK, Way of Life): goals are heterogeneous, so the social graph never densifies, the content in the feed is incoherent (someone's meditation streak next to someone's deadlift PR), and there's no shared vocabulary for what "good" looks like. Network effects require homogeneity at launch, not diversity.

**Top 2 candidates considered:**

- **Fitness/physique transformation (75 Hard, cuts, marathon training).** Pro: huge existing culture (r/bodybuilding, 75 Hard has done its own viral loop for free), photo/video check-ins are a natural mechanic, Strava proves willingness to pay and post. Con: Strava, Whoop, and Fitbod already own verified fitness data and are extending into social. You'd be fighting entrenched integrations on their home turf, and fitness has the weakest "cohort" structure — everyone's on their own timeline.
- **Professional certification exams (CPA, Bar, USMLE Step 1/2, CFA Level I-III, PE exam).** Pro: hard external deadline (exam date) creates urgency no habit app can manufacture; candidates already self-organize into Discord servers and Reddit threads (r/CPA has 90k+ members, r/Mcat 200k+) desperate for structure; existing spend is enormous — CPA review courses run $2,000-3,000/candidate (Becker, UWorld), so willingness-to-pay is proven and a $15-30/month accountability layer is a rounding error by comparison; failure is expensive and public (a failed Bar attempt costs a bar-prep re-enrollment plus a delayed career), so the emotional stakes that drive daily engagement are real, not manufactured; cohorts are naturally time-boxed (a CPA cycle is 18 months, a Bar prep cycle is 10 weeks), which gives you a clean "season" structure for free. Con: smaller total population than "fitness," and once someone passes, they graduate out — churn is structural, not a failure mode.

**Choice: certification exams**, specifically starting with CPA candidates (Becker/UWorld already train users to expect $2-3k of spend and rigid daily study plans, and the AICPA publishes exact section-by-section pass rates you can use for outcome-based marketing) as the first cohort, with Bar exam and USMLE as fast-follow cohorts 2 and 3, because the go/no-go decision loop is identical (external test date, existing prep-vendor spend, existing subreddit/Discord density) and you can reuse 90% of the product. Fitness becomes cohort 4-5 once Lock Score has enough verified data to make cross-domain reputation meaningful — at that point you're not competing with Strava head-on, you're offering something Strava structurally can't: a reputation score that means the same thing whether you're grinding CPA MCQs or marathon training.

**What I'd bet on:** cohort density beats total addressable market at launch. 5,000 obsessed CPA candidates who all know the exam windows (Jan-Feb, Apr-May, Jul-Aug, Oct-Nov) and can be activated around them in synchronized waves beat 50,000 scattered "self-improvement" users.
**What would kill this:** if certification candidates turn out to prefer the free, ungated Discord/Reddit experience precisely because it's low-commitment — i.e., if the willingness to pay for structure doesn't transfer from "content" (Becker) to "accountability" (LockedIn). Validate this with a $9 paid beta before building anything else.

### 2. The Retention Death-Spiral

This is the correct question to center the entire product on. The mechanism in every failed accountability app: miss a day → app shows a broken streak / red X / declining chart → user feels judged by their own tool → user opens the app less to avoid the feeling → the absence compounds → eventually uninstall. Duolingo solved a version of this with streak freezes, but Duolingo's stakes are trivial (a vocabulary app) compared to "I might fail my CPA exam," so a straight streak-freeze copy won't be enough.

**LockedIn's answer, concretely:**

- **No punitive visual language, ever.** No red X, no "streak lost" screen, no declining line charts as the primary UI. A miss is rendered as a gap, not a failure state — visually neutral, like a rest day on a calendar, not a strikethrough.
- **The "Reset, not Restart" mechanic.** Duolingo and Snapchat both train users that a broken streak means going back to zero, which is precisely the punishment that causes rage-quits. LockedIn's Lock Score is a rolling 90-day weighted average, not a consecutive-day counter — one missed day costs a few points, not the entire history. The product's own math literally forgives you faster than the user forgives themselves.
- **Pod-triggered re-engagement, not app-triggered.** The worst thing you can do after a miss is send the user a notification from *the app* ("You broke your streak!") — that's the shame vector. Instead, when a pod member misses a check-in, LockedIn notifies one specific accountability partner ("Sam missed today — send a nudge") and lets *a human*, not the product, do the re-engagement. This converts the moment of highest churn risk into the moment accountability pods prove their value, which is the actual product-market fit test for the whole pod feature.
- **"Comeback" as a status event, not a confession.** Missing days is reframed in the product's own vocabulary as normal — the onboarding explicitly teaches "you will miss days; what matters is the return." Returning after 3+ days off triggers a distinct, positive UI moment (not congratulatory-cringe, just neutral and welcoming) rather than forcing the user to confront a graveyard of missed check-ins.
- **Cap the downside of gamification.** No leaderboard demotion mechanics, no "you dropped to bronze" loss-framing. Levels and streak-freezes only move up or hold; visible rank never drops below a floor tied to lifetime effort, so a bad week can't erase months of credibility (this is also core to why Lock Score resists being just "another leaderboard" — see Product section).

**What I'd bet on:** removing punitive UI is necessary but not sufficient — the pod-triggered human nudge is the actual retention mechanism, because a message from a real accountability partner has 10-50x the reopen rate of a push notification (this mirrors WhatsApp/iMessage reopen rates vs. generic app notifications, which sit around 3-5% CTR industry-wide per OneSignal/Braze benchmarks).
**What would kill this:** if pods don't form densely enough at launch for the human-nudge mechanic to fire reliably — a user with no pod has no safety net, and reverts to the exact death-spiral this section is trying to solve. This is why cold-start (Q4) and wedge selection (Q1, pre-existing cohorts) are prerequisites, not parallel workstreams.

### 3. Why Now

Three converging shifts make 2026 the moment, not 2016:

- **Cultural:** "Lock in" as vocabulary crossed from niche gym/hustle-culture slang into mainstream Gen Z usage in 2023-2025 (Dictionary.com shortlisted it as a 2024 word-of-the-year candidate) — the brand name itself rides an existing cultural wave rather than needing to create one, the way "streaks" needed Duolingo to popularize before Snapchat and BeReal could build on it.
- **Technological — cheap AI coaching:** In 2016, an "AI coach" was a chatbot with canned responses. In 2026, a GPT-5/Claude-class model can review a user's check-in photo, workout log, or MCQ performance data and produce a genuinely specific, non-generic response for fractions of a cent per interaction — the unit economics of "coach in every pocket" didn't exist a product cycle ago. This is the single biggest technological unlock: cost per AI coaching interaction has fallen roughly 100x since 2022 (GPT-3.5-era vs. current-generation small models), making a $15-30/month subscription that includes meaningful AI coaching gross-margin-positive for the first time.
- **Wearable/integration ubiquity:** Apple Health, Whoop, Oura, Strava, and GitHub-as-portfolio are now default infrastructure for the target user, not early-adopter novelties — auto-verification (Q7, Q on wellbeing) is only trustworthy and low-friction because the data already exists and users already consent to sharing it elsewhere.

**What I'd bet on:** the cultural wave (lock-in, "sigma," "discipline equals freedom" aesthetics on TikTok) gives LockedIn a 12-24 month window of favorable brand-market fit that a generic "habit tracker" positioning wouldn't get — but that wave is also a risk (see below).
**What would kill this:** cultural slang is disposable by nature. If "locking in" is a 2024-2026 meme that fades by 2028 the way "hustle culture" aesthetics partially receded post-2022, the brand needs the Lock Score/pod mechanics to carry the product on their own merits once the naming trend cools — which is why product depth (Tier 2) can't be skipped in favor of vibes-based marketing.

### 4. The Cold-Start Problem

Single-player value with zero friends: the Goal Profile + Daily Check-In + AI Coach loop must work completely alone, functioning as a superior version of a private journal/habit tracker (competing directly with Streaks, Habitica, and a Notion template) before any social layer activates. If the app requires a pod to be useful on day one, you've built a ghost town, not a product.

**Bootstrapping the first 1,000 true believers:**

- Recruit directly from the wedge's existing dense communities — r/CPA, r/Mcat, r/LawSchool's Bar-prep threads, and CPA/Bar-prep Discord servers already have thousands of self-organizing, deadline-driven members who are *already* running ad hoc accountability threads ("Day 47 of Becker, MCQ score log") manually in Google Sheets and subreddit megathreads. This is the strongest possible cold-start signal: the behavior already exists, unpaid, in a worse tool.
- Ship with pre-built "Season" cohorts pegged to real exam windows (e.g., "CPA Jan-Feb 2027 Cohort") so the first 1,000 users are automatically grouped by shared deadline before they've added a single friend — the pod is pre-populated by the platform, not left to organic friend-adding, which is the single biggest cold-start failure mode of Discord-clone accountability apps.
- Partner with 3-5 mid-size CPA/Bar-prep YouTubers and TikTok creators (10k-200k subscriber range, not celebrity-tier) for revenue-share or flat-fee placements — this audience trusts creator recommendations over app-store ads at a 2016 order of magnitude, and CAC through this channel should land in the $8-20 range versus $40-80+ for generic paid social in the productivity-app category (Duolingo's own blended CAC has historically been reported in the low-teens to $20s per install, and CPA candidates are a much narrower, more purchase-intent audience than "everyone who wants to learn Spanish").
- Founder-led manual matchmaking for the first 20-30 pods: literally assign pod membership by hand for the earliest cohort rather than trusting the matching algorithm (Tier 2) to work with a thin user base — an algorithm needs density to be good, and density doesn't exist yet.

**What I'd bet on:** the single-player loop (Goal Profile, check-in, private Lock Score, AI Coach) needs to be good enough that a solo user pays for it with zero social features working — this de-risks the whole cold-start problem because it means the business doesn't require network effects to reach revenue, only to reach scale.
**What would kill this:** if the AI Coach's single-player value is indistinguishable from ChatGPT-with-a-good-prompt, users won't pay for LockedIn standalone, and the whole cold-start bet collapses back into needing the pod/social layer to matter from day one.

### 5. Defensibility

Every individual feature — check-ins, streaks, leaderboards, pods, AI coaching — is copyable by a funded team in two quarters; this is the correct level of paranoia to have. The actual moat has to be structural, not feature-based:

- **Lock Score as portable reputation, built on verified longitudinal data.** A leaderboard is copyable in a sprint. A reputation score that took 18 months of consistent, cross-source-verified (Apple Health + Strava + GitHub + exam-provider data) behavior to build is not copyable — a competitor can build the UI in a week, but they can't backdate your users' 18 months of check-in history. This is the same mechanic that makes a credit score or a StackOverflow reputation score defensible: the data moat compounds with time and is worthless to fake retroactively.
- **Network density within cohorts, not network size.** LinkedIn's moat isn't "many users," it's that your specific professional network is on LinkedIn and switching costs you your connections. LockedIn's moat should be that your specific accountability pod — the 5-8 people who've seen you through a 10-week Bar prep sprint — exists on LockedIn and nowhere else. Strava can bolt on "pods" as a feature; it cannot bolt on the specific relationships your pod has built over 10 weeks of daily co-accountability.
- **Why Strava/LinkedIn specifically can't just bolt this on:** Strava's entire product culture and data model is built around discrete, GPS-timestamped athletic activities — retrofitting "pass the CPA exam" or "save $20k" as a first-class goal type is a data-model-level rewrite, not a feature flag, and Strava's core user base (athletes) has no organic reason to want CPA-candidate pods in their feed, so even a technically-possible bolt-on would dilute their core product without a matching audience. LinkedIn's moat is professional identity tied to real names and employers — the vulnerable, day-47-relapse honesty that makes accountability check-ins valuable is structurally incompatible with a platform where your boss might see your feed. This is not a minor UX tweak for LinkedIn to fix; it is existential to their trust model.

**What I'd bet on:** data-moat-through-time (Lock Score) plus relationship-moat-through-cohort-density (pods) compound together — a user with an 18-month verified Lock Score *and* a pod of five people who've supported them through two exam cycles has enormous switching costs that no feature clone can replicate in month one.
**What would kill this:** if Lock Score verification integrations (Q on schema/architecture) turn out to be gameable or low-trust, the entire reputation moat is fake, and LockedIn is just a leaderboard app with extra steps.

### 6. The Billion-Dollar Math

Working backward from a $1B outcome, assuming a SaaS-style revenue multiple of 8-12x ARR (reasonable for a high-retention consumer-subscription business, roughly where Duolingo trades), LockedIn needs **$85-125M ARR**.

| Revenue Stream | Plausible ARPU/Take | Scale Required | Verdict |
|---|---|---|---|
| Consumer subscription ($15-25/mo, ~$180-300/yr) | ~$220/yr blended (accounting for annual-plan discounts) | ~400-500k paying subscribers | **Carries the business.** This has to be the core engine — comparable to Duolingo's ~$40/yr blended ARPU but priced far higher because the audience (exam candidates already spending $2-3k on prep) has a much higher willingness-to-pay than casual language learners. |
| Coach/expert marketplace (15-20% platform take on programs sold) | If coaches collectively generate $30-50M GMV, platform take is $5-9M | Requires thousands of active paying coaches — a multi-year build | **Meaningful but not primary at scale**, comparable to Patreon/Substack-style take rates; strong secondary line once Lock Score gives buyers a trust signal for which coaches are legitimate. |
| Verified certification/employer partnerships (B2B2C — e.g., a CPA review company or employer wellness program licensing Lock Score data/cohorts) | $50-200k per enterprise deal | 100-300 deals for $15-30M | **Real but slow-building**, requires Lock Score to be trusted as a credential first — a Tier-4/Year-3+ line, not a launch line. |
| Cosmetics/gamification IAP | $1-3/mo blended among a minority of users | Rounding error at this audience size | **Rounding error.** Discipline-focused users are not the same psychographic as skin-buying mobile-game users; don't build a cosmetics economy expecting it to matter financially — it exists for retention/identity signaling, not revenue. |

**Honest read:** subscription has to do 80-90% of the work. 400-500k paying subscribers at ~$220/year blended ARPU is the real target — for context, Duolingo has ~8-9M subscribers at a lower price point; LockedIn's bet is a narrower audience at 5-6x the price point, which is a defensible bet given certification-exam candidates' proven prep spend, but it is a real bet, not a guarantee. The coach marketplace and B2B credentialing lines are what make the multiple defensible (they signal a platform, not just an app) but neither carries the top-line number alone in the first five years.

**What I'd bet on:** price high relative to habit-tracker comps ($15-25/mo, not $5-8/mo) because the wedge audience's reference price point is a $2-3k prep course, not a $5 habit app — underpricing against that anchor leaves money on the table and, worse, signals low seriousness to a status-conscious, achievement-oriented buyer.
**What would kill this:** if the wedge audience treats LockedIn as a nice-to-have accountability layer on top of Becker/UWorld rather than a must-have, willingness-to-pay collapses toward habit-tracker pricing ($5-8/mo) and the whole billion-dollar math needs 2-3x the subscriber count to work.

### 7. The Wellbeing Tension

This is a real design constraint, not a PR footnote. Leaderboards plus discipline framing plus a "Lock Score" plus streaks is, unmitigated, a toxic-productivity machine — and the mental-health/wellness use case (someone using LockedIn to track therapy homework, or recovery milestones) sits in direct tension with a leaderboard culture built around grindset aesthetics.

**Concrete lines drawn:**

- **Leaderboards are opt-in and pod-scoped, never global by default.** A global leaderboard turns every goal into a competition against strangers, which is precisely the comparison trap Instagram already causes. Default visibility is private-to-you or shared-with-your-pod only; global rankings exist but require explicit opt-in per goal, and are off by default for any goal category tagged "health/recovery" (mental health, addiction recovery, weight-loss-for-medical-reasons) — the product actively prevents leaderboard-ification of categories where competition is actively harmful.
- **No streak-shaming, covered in Q2, is also a wellbeing feature, not just a retention feature** — the same design choice serves both goals simultaneously, which is the right kind of design decision to look for.
- **Rest and recovery are first-class goal states, not failure states.** A user can log a planned rest day distinctly from a missed day; the AI Coach is explicitly prompted (and this is a hard product requirement, not a nice-to-have) to recognize patterns consistent with overtraining, burnout, or compulsive check-in behavior (e.g., a user checking in obsessively multiple times a day, or someone whose "streak" behavior looks compulsive rather than healthy) and to surface a supportive, non-judgmental prompt to rest — this is a guardrail explicitly in the AI Coach's system design (Tier 2), not an afterthought.
- **No public shaming mechanics, ever, full stop.** No "who fell off" call-outs, no public rankings-by-decline, no pod features that let members publicly mock a lapsed member. Moderation policy (Tier 2) treats "shaming a pod member for missing check-ins" as a bannable offense, not just discouraged behavior.
- **The line between "addictive" and "healthy addictive":** the product optimizes for return-after-lapse (Q2) and long-horizon consistency, not for maximum daily session time or maximum notification volume. Duolingo's own well-documented notification aggression ("the owl") is explicitly something to avoid emulating — LockedIn should feel more like a supportive coach who checks in appropriately than a nagging app optimizing DAU at the cost of user sentiment. This is a real trade-off against short-term engagement metrics, and it should be made deliberately and stated internally, not discovered after a growth team over-optimizes notifications in year two.

**What I'd bet on:** treating "return after lapse" as the north-star retention metric instead of "consecutive-day streak length" changes what the whole team optimizes for, and produces a fundamentally healthier product than copying Duolingo's mechanics wholesale.
**What would kill this:** if growth pressure in year 2-3 pushes the team toward Duolingo-style aggressive notification tactics to hit engagement targets, the wellbeing positioning becomes marketing copy contradicted by the actual product, which is a brand-destroying credibility gap for a platform whose entire premise is authenticity over performance.

---

## Tier 1 — Strategy

### Vision & Mission

**Vision:** Become the operating system for self-improvement — the layer where a person's real, verified effort toward any goal accumulates into a portable, credible record of who they are becoming, not who they're pretending to be.

**Mission (near-term, launch-scoped):** Give ambitious people with a deadline — starting with certification-exam candidates — a daily accountability system that makes consistency easier to sustain than to abandon, and makes their effort verifiable to coaches, peers, and eventually employers.

### Wedge and Expansion Sequence

| Phase | Cohort | Why This Order | Unlocks |
|---|---|---|---|
| 0 (Beta, 0-3 mo) | CPA candidates (r/CPA, Becker/UWorld communities) | Proven spend, hard deadline, dense pre-existing communities, clean season structure (quarterly exam windows) | Validates willingness to pay for accountability layered on top of existing prep spend |
| 1 (Launch, 3-9 mo) | + Bar exam candidates, USMLE Step 1/2 | Identical structural properties to CPA (deadline, spend, community density); near-zero product rework | Cross-cohort Lock Score comparability; proof the model generalizes beyond one exam type |
| 2 (9-18 mo) | + coding bootcamp job-search sprints, CFA | Same deadline-driven structure; GitHub integration becomes a natural verification source | First real use of "collaboration marketplace" (co-founder/study-group matching) since coding cohorts want peers, not just accountability |
| 3 (18-30 mo) | + fitness transformation (75 Hard-style challenges) | By now Lock Score has 18+ months of cross-domain verified data, so a fitness cohort strengthens the reputation graph instead of diluting it with an unproven mechanic | Proves the "any goal" thesis with real data behind it, not just marketing |
| 4 (30+ mo) | + general self-improvement (financial goals, creative practice, habit-building) | Platform, not app — Lock Score is now a recognizable credential across domains | Coach marketplace and B2B credentialing lines become viable at scale |

### Personas

**1. Priya, 26, CPA candidate, second attempt at FAR section.**
Goal: pass FAR within her 18-month rolling window before her first-attempt credits expire. Fear: failing again and having to restart the entire 18-month clock, which would mean the $3,000 she's already spent on Becker was wasted and she'd have to explain a second failure to her firm's partners. Why she'd quit LockedIn: if check-ins feel like one more thing to perform for an audience rather than a private tool that helps her actually pass — she has zero tolerance for anything that feels like a "cringe" productivity-influencer aesthetic, and will delete instantly if she senses the app cares more about her posting than her passing.

**2. Marcus, 34, software engineer training for a return to competitive powerlifting after a 3-year injury layoff, also trying to ship a side project.**
Goal: total 1200 lbs across squat/bench/deadlift within 12 months while shipping a SaaS side project on nights and weekends. Fear: re-injury from overtraining, and more quietly, the shame of having "let himself go" during the layoff — he does not want a fitness app that makes him relive a public decline. Why he'd quit: if the leaderboard forces him to compete against people who never took a 3-year break, making his "progress" look like mediocrity by comparison rather than the genuine comeback it is — this is exactly the pod-scoped-not-global leaderboard design point in Q7.

**3. Danielle, 41, going through outpatient treatment for alcohol use disorder, using structured daily check-ins as part of her recovery plan alongside a therapist.**
Goal: 180 days of verified sobriety and consistent attendance at IOP (intensive outpatient) sessions. Fear: relapse being visible to anyone, and the compounding shame of a broken streak actively harming her recovery rather than supporting it — for this persona specifically, punitive streak UI isn't just bad retention design, it's a genuine harm vector. Why she'd quit: any hint of gamified competition, public visibility, or streak-shame turns the app from a support tool into a surveillance/judgment tool, which could set back actual clinical recovery, not just app engagement. This persona is the sharpest test of the Q7 wellbeing guardrails and should be a standing reference case in every product review, not an edge case.

### Competitive Teardowns

| Platform | What We Steal | What We Exploit |
|---|---|---|
| **LinkedIn** | Professional-identity-linked credibility signals; "verified" badges/credentials as trust shorthand | LinkedIn's status-signaling culture (humble-brag posts, engagement-bait) is exactly what makes it useless for honest accountability — nobody posts "I fell behind this week" on LinkedIn. We build the platform where that honesty is the point, and Lock Score becomes a credential LinkedIn can't offer because its entire culture rewards performance over truth. |
| **Instagram** | Visual, low-friction content creation (Stories-style ephemeral check-ins); strong creator/influencer tooling patterns for coaches | Instagram optimizes for aesthetic highlight-reel content and rewards attention/appearance over substance — the exact dynamic that makes it psychologically corrosive for people trying to build real discipline. We exploit this by making the feed literally incapable of rewarding a beautiful photo with no verified progress behind it — Lock Score, not likes, drives visibility. |
| **Strava** | Auto-verification via device/app integrations; kudos-as-lightweight-social-proof; segment/challenge mechanics | Strava's social graph and product model are single-domain (athletic activity) and its "kudos" carries no real weight (it's a like by another name) — we exploit the fact that Strava has never built cross-domain reputation, and its entire cohort/challenge structure is athlete-only, leaving certification/career/financial goal-seekers completely unserved. |
| **Discord** | Persistent, always-on community spaces (servers/channels) with real-time voice/chat for pods; strong small-group identity | Discord has zero structure — no goal tracking, no verification, no reputation system, so accountability servers today are just chat channels where people manually self-report with no product support. We exploit this gap directly: we're "Discord with a spine," giving the community layer Discord already proved people want, plus the structure Discord will never build because it's not a discipline product, it's a chat product. |
| **Reddit** | Deep community self-organization around niche, high-stakes goals (r/CPA, r/GetMotivated, r/stopdrinking); anonymity as a feature for vulnerable disclosure | Reddit has no persistence or personalization — a "Day 47" post scrolls away in 24 hours and there's no cumulative record, no verification, and no reputation that follows the user. We exploit this by being the place where that same vulnerable, anonymous-if-desired disclosure culture gets a permanent, structured home with actual continuity. |
| **Duolingo** | Streak mechanics, streak-freeze forgiveness, gamified XP/levels, mascot-driven notification personality, "just five minutes a day" low-friction habit design | Duolingo's mechanics are proven at massive scale but are built for a low-stakes, low-shame domain (language learning) — its notification aggression ("the owl") works because failing to learn Spanish today isn't emotionally loaded the way failing to study for the Bar is. We exploit this by taking Duolingo's forgiveness mechanics (streak freeze logic) but explicitly rejecting its notification aggression, tuning tone to the higher stakes of our audience. |

### Monetization Strategy

See Q6 (Billion-Dollar Math) for the full breakdown. Summary: consumer subscription ($15-25/mo tiered by cohort — CPA/Bar/USMLE candidates can bear higher price points given existing prep spend) is the primary engine; coach/expert marketplace take-rate is a strong secondary line that also reinforces the Lock Score trust moat (coaches with verified track records via Lock Score command premium pricing, giving the marketplace a reason to exist beyond generic Patreon-style hosting); B2B/credentialing partnerships are a longer-horizon, higher-margin line that only becomes viable once Lock Score has enough longitudinal data to be trusted externally (realistically year 3+).

### Go-to-Market & Viral Growth Loops

- **Primary loop — cohort-seeded virality:** because the wedge audience already self-organizes into subreddit/Discord megathreads, the go-to-market motion is "productize the megathread" — launch pre-built Season cohorts timed to real exam windows, seed them via creator partnerships (Q4), and let existing community density do the inviting (a Becker study group of 8 friends migrating together is a stronger activation unit than 8 individually-acquired users).
- **Secondary loop — Lock Score as a shareable credential:** once a user has a meaningful Lock Score (e.g., "127-day verified CPA study streak, 94% MCQ accuracy trend"), the product should make it trivially easy to share that specific, factual, non-performative credential externally (a static, verifiable card, not a boastful post) — this is a fundamentally different viral mechanic than Instagram's "look how good my life looks," it's closer to a Strava activity share or a GitHub contribution graph, both of which have proven durable, non-cringe sharing behavior.
- **Tertiary loop — coach-led acquisition:** verified coaches building programs on the platform bring their existing audiences (a CPA tutor with 5,000 YouTube subscribers becomes a acquisition channel once the marketplace exists), which is a classic Substack/Patreon-style creator-led growth loop.

**Risks and mitigations table:**

| Risk | Mitigation |
|---|---|
| Cohort graduates and churns structurally (passed the CPA exam = no more reason to use the app) | Design explicit "alumni" status in Lock Score/pod structure — graduated users become mentors/coaches for the next cohort, converting structural churn into supply for the marketplace (Q2 persona expansion) rather than pure loss |
| "Lock in" cultural trend fades, brand feels dated by 2028 | Product depth (Lock Score data moat, pod relationships) must carry the brand once the slang fades — track this explicitly, don't let brand marketing substitute for product substance |
| Verification integrations get gamed (fake Apple Health data, screenshotted fake progress) | Multi-source cross-verification (Tier 3 security model) — no single self-reported data point counts toward Lock Score without a corroborating signal |
| Growth-stage pressure pushes toward Duolingo-style notification aggression, contradicting wellbeing positioning | Make "return-after-lapse rate," not "notification CTR" or "streak length," the explicit north-star metric in growth OKRs from day one — a metric choice, not just a values statement |
| Competitor with more capital (a funded Strava competitor, or Strava itself) copies the surface features fast | Moat is data-over-time + pod relationship density (Q5) — the correct response is to accelerate cohort depth and Lock Score data accumulation, not to out-feature a better-funded copycat |

---

## Tier 2 — Product

### Prioritized Feature List: Build / Defer / Kill

| Feature | Decision | Justification |
|---|---|---|
| Goal Profiles (missions, milestones, timelines) | **Build now** | Core primitive everything else depends on; must exist at launch |
| Daily Lock-In Check-Ins (photo/video/voice/timer) | **Build now**, auto-verification deferred per-integration | The core loop; ship with manual + basic photo check-in first, add deep integrations (Q below) incrementally |
| Accountability Pods (groups, chat) | **Build now**, scoped small (5-8 people, pre-seeded per Season cohort) | Central to the retention mechanism (Q2); must exist at launch, but keep it simple — chat + check-in visibility only, no calls yet |
| Pod leaderboards | **Build now**, opt-in and pod-scoped only, never global by default | Needed for the accountability mechanic, but must respect Q7 wellbeing guardrails from day one, not bolted on later |
| Pod video/voice calls | **Defer to V2** | Nice-to-have social layer; not core to the retention loop, and building reliable calls is expensive engineering for a feature with unproven demand at this stage |
| Coaches & Experts marketplace | **Defer to V2 (post-cohort-2)** | Needs Lock Score data to be meaningful as a trust signal for buyers first (Q6); launching a marketplace with no reputation signal is just an unverified Fiverr clone |
| Lock Score reputation system | **Build now**, start simple (consistency + basic verification), sophisticate over time | This is the moat (Q5) — must start accumulating data from day one even though the sophisticated anti-gaming version comes later |
| AI Coach | **Build now**, narrow scope at launch (check-in review, encouragement, basic pattern-spotting) | Single-player value driver (Q4); full personalized coaching/planning is a V2-V3 sophistication, not a launch requirement |
| Smart integrations (Apple Health, Strava, GitHub, Duolingo, Kindle, Notion) | **Build 2-3 at launch (Apple Health, GitHub for coding cohort, exam-provider score imports where available), defer the rest** | Spreading thin across 6+ integrations at launch dilutes engineering effort; pick the 2-3 that matter most for the wedge cohort and expand as cohorts expand (Phase 2 adds GitHub relevance) |
| Collaboration marketplace (accountability partners, co-founders, study groups) with AI matching | **Defer to Phase 2 (coding bootcamp cohort)** | Doesn't matter for CPA solo-study candidates at launch; becomes relevant when coding/co-founder cohorts arrive |
| Challenges (75 Hard, coding streaks) | **Build now, lightweight version** | Cheap to build as a wrapper around existing Goal Profile + check-in primitives; strong viral/marketing value (75 Hard already has organic reach) |
| Progress-first feed | **Build now**, pod-scoped by default, no global public feed at launch | Needed for the social loop, but a global feed at launch with thin content density will look like a ghost town — start pod-scoped, expand once density exists |
| Gamification (XP, streaks, levels, cosmetics, seasons) | **Build streaks/levels now (redesigned per Q2's anti-shame rules); defer cosmetics** | Streaks/levels are core loop reinforcement; cosmetics are a rounding-error revenue line (Q6) and a distraction from core loop polish at launch |
| Global public leaderboards | **Kill (for launch), reconsider only opt-in later** | Directly conflicts with Q7 wellbeing design and Q2 anti-shame retention design; the naive "engagement" case for this is exactly the trap that makes accountability apps toxic |
| Cross-domain "everyone with a goal" feed/matching | **Kill until Phase 3+** | Premature — the wedge strategy (Q1) explicitly depends on NOT doing this until cohort density and Lock Score data justify it |

### The Core Daily Loop

1. **Morning prompt (optional, not aggressive):** AI Coach surfaces today's plan based on the user's Goal Profile (e.g., "3 FAR MCQ sets today, per your Becker schedule") — informational, not guilt-inducing.
2. **Check-in:** user logs progress — could be a photo, a timer completion, an auto-synced data point (MCQ score import, GitHub commit, Apple Health workout), or a simple manual confirmation. Friction is minimized; a check-in should take under 15 seconds for the common case.
3. **Immediate, specific feedback:** not a generic "Great job!" — the AI Coach or Lock Score delta reflects something specific ("94% on today's set, trending up from last week's 89%").
4. **Pod visibility (optional per goal):** check-in becomes visible to the user's pod, enabling lightweight kudos/comments — not a public feed.
5. **End-of-day/week reflection:** lightweight prompt for context behind the numbers (a voice note, a short text reflection) — this is where the qualitative, non-gameable signal lives, useful both for the user's own record and eventually for coach/AI context.
6. **Miss handling (Q2 mechanic):** if no check-in by end of day, no punitive notification from the app; instead, the pod-nudge mechanic queues a prompt to one pod partner the next morning.

### Lock Score System

**Inputs (weighted, rolling 90-day window, not lifetime-cumulative):**
- Check-in consistency (% of planned days with a completed check-in) — largest single weight
- Verification tier of each check-in (see below) — verified data counts more than self-report
- Trend direction (improving/plateauing/declining on goal-specific metrics, e.g., MCQ accuracy, weight trend, savings rate)
- Pod engagement quality (giving, not just receiving, accountability — nudging others counts positively, incentivizing pro-social behavior rather than pure self-tracking)
- Longevity (a 400-day verified history carries more weight per data point than a 10-day history, rewarding sustained behavior over recent bursts)

**Explicitly NOT inputs:** follower count, likes/kudos received, number of pods joined, content "quality" (production value of photos/videos), posting frequency independent of actual check-in completion. This is the exact mechanism by which Lock Score resists becoming a popularity contest — the scoring function has no term for social approval, only for verified behavior.

**Verification tiers (highest to lowest trust weight):**
1. **Third-party API-verified** (Apple Health workout data, GitHub commit history, Strava activity, exam-provider score import) — highest weight, near-impossible to fake without also faking the underlying real-world action.
2. **Cross-corroborated self-report** (a photo check-in plus a timer that ran in-app plus geolocation-optional context) — moderate weight, harder to fake than a single signal.
3. **Single-source self-report** (a typed check-in with no supporting signal) — lowest weight, counts toward consistency streaks but contributes minimally to the "verified achievement" portion of the score, and is clearly labeled as such to other users (transparency about verification tier is itself an anti-gaming and anti-shame design choice — nobody is penalized for lacking access to a wearable, but nobody can fake top-tier trust either).

**Anti-gaming design:**
- Score is a rolling weighted window, not a cumulative counter — this alone kills the "front-load fake activity, coast on reputation forever" attack that plagues systems like inflated follower counts or old Yelp reviews.
- Verification tier transparency means a user can't misrepresent unverified self-report as device-verified data — the UI always shows provenance.
- Sudden anomalous spikes (e.g., a week of implausibly perfect data after months of gaps) trigger a soft flag that temporarily caps score growth pending continued consistent behavior — modeled conceptually on anti-fraud rate-limiting, not a punitive ban, just a "prove it over time" throttle.
- No score component rewards content production (photo/video quality) independent of the underlying verified action — this closes the Instagram-style "look impressive" exploit at the scoring-function level, not just a policy level.

**Why it resists popularity:** because the scoring function structurally has no term for social approval (likes, followers, comments), gaming Lock Score requires actually doing the underlying work consistently over months — which is, definitionally, the thing the platform is trying to encourage. This is the same design principle that makes a credit score or a real professional certification hard to fake: the cost of faking it converges toward the cost of just doing the real thing.

### AI Coach: Capabilities and Guardrails

**Capabilities at launch:**
- Review check-in content and surface specific, non-generic feedback tied to the user's actual data trend (not templated praise).
- Answer goal-specific planning questions grounded in the user's Goal Profile and check-in history (e.g., "Based on your last 3 weeks of MCQ scores, here's where your weak areas are").
- Pattern recognition for early lapse risk (declining check-in frequency, declining scores) — surfaced supportively, framed as "want help getting back on track?" not "you're falling behind."
- Wellbeing pattern recognition (Q7): flag potential overtraining, compulsive check-in behavior, or signs of burnout, and respond with a supportive prompt toward rest rather than more grinding.

**Explicit guardrails:**
- Never gives medical, legal, or financial advice beyond general encouragement and pattern observation — for a mental-health/recovery-tagged goal (Danielle's persona), the AI Coach's role is explicitly supportive/logistical (did you attend your session, how are you feeling), never a substitute for or imitation of clinical guidance, and the product should prompt users toward real professional support resources when patterns suggest genuine crisis, not attempt to handle it in-app.
- Never uses guilt, shame, or comparison-to-others language, full stop — this is a hard content-policy constraint on the system prompt/guardrails, not a style preference.
- Transparent about being AI — no impersonation of a "real" coach; positioned clearly as a supportive tool that complements, not replaces, the human coach marketplace and pod relationships.
- Rate-limited/tuned to avoid notification aggression (Q7) — proactive AI Coach messages are infrequent and high-signal, not a constant nagging presence.

### Community Systems: Pods, Challenges, Moderation

- **Pods:** 5-8 people, formed either by platform-seeded Season cohorts (launch mechanism, Q4) or by user-initiated invite once the matching algorithm (below) is mature enough to trust. Pod chat is lightweight (text + async voice notes at launch; live calls deferred to V2). Pod-level visibility of check-ins is opt-in per Goal Profile, not automatic.
- **Challenges:** structured, time-boxed programs (75 Hard-style) that a user can attach to a Goal Profile; completion contributes positively to Lock Score under the same verification-tier rules as any other check-in. Challenges are the primary vehicle for organic/viral growth (Q GTM) since they're inherently shareable and have proven cultural reach independent of LockedIn.
- **Moderation:** shaming a pod member for a missed check-in, mocking lapses, or any public ridicule of a lapse is an explicit, bannable policy violation (Q7) — enforced with the same seriousness as harassment policy on any social platform, not treated as a minor community-guidelines footnote. Report/mute/block tooling ships at launch, not as a V2 add-on, given the vulnerability of the check-in content users are sharing (recovery, health, financial struggles).

### Matching Algorithm (Collaboration Marketplace / Pod Formation, Phase 2+)

Once cohort density supports it (Phase 2, coding/co-founder cohorts), matching considers: shared goal category and sub-timeline (e.g., same exam window, same job-search sprint length), complementary schedule/availability, Lock Score tier (matching users of roughly comparable consistency levels, since a highly consistent user paired with a highly inconsistent one tends to produce frustration on one side and shame on the other — a direct application of the Q7 wellbeing lens to algorithm design), and stated communication-style preferences (some users want tough-love accountability, others want gentle encouragement — mismatched tone is a likely churn driver worth explicitly surveying for at pod-formation time).

### Gamification System and the Anti-Shame Retention Model

XP and levels reinforce consistency (verified check-ins earn XP; levels are a monotonically non-decreasing reflection of lifetime effort, per Q2's "never demote" design). Streak-freeze mechanics (2-3 forgiveness tokens per month, replenishing) borrow Duolingo's proven forgiveness pattern but pair it with the rolling-window Lock Score math (Q2) so that even a fully-spent freeze doesn't cause catastrophic score loss. Seasons (tied to real exam windows for the wedge cohort) give natural reset points that feel like fresh starts, not failures — critically, a new Season does NOT zero out Lock Score (which is lifetime/rolling), it only resets Challenge-specific and pod-cohort structures, so users get the psychological benefit of a fresh start without the moat-destroying effect of literally discarding their reputation data.

### MVP → V5 Roadmap

| Version | Scope | Cohort |
|---|---|---|
| MVP (0-3mo) | Goal Profiles, manual + basic photo check-ins, simple Lock Score (consistency-only), pre-seeded pods, lightweight AI Coach (feedback only), 1-2 integrations (Apple Health) | CPA beta, ~1,000 users |
| V1/Launch (3-9mo) | + verification-tier Lock Score, pod chat, Challenges, GitHub integration, exam-score import | + Bar, USMLE |
| V2 (9-18mo) | + Coach/expert marketplace, pod calls, richer AI Coach (planning, pattern-spotting), anti-gaming score sophistication | + Coding bootcamp, CFA |
| V3 (18-30mo) | + Collaboration marketplace/AI matching, cross-cohort Lock Score comparability, B2B credentialing pilots | + Fitness transformation |
| V4-V5 (30mo+) | + General self-improvement goal types, employer/partner API access to Lock Score (with user consent), full "operating system" positioning | General audience |

---

## Tier 3 — Design & Engineering

### Information Architecture

Top-level navigation: **Today** (check-in home, AI Coach surface) → **Progress** (Goal Profile detail, Lock Score history/trend) → **Pod** (chat, pod-scoped feed/leaderboard) → **Discover** (Challenges, coach marketplace once live) → **Profile** (Lock Score summary, verified achievement record, privacy controls). This mirrors Duolingo's flat, single-purpose-tab structure rather than Instagram's feed-first IA, deliberately — the home screen is "what do I need to do today," not "what is everyone else doing."

### Mobile Wireframes (screen-by-screen)

- **Today screen:** top third shows today's planned check-in(s) from active Goal Profiles as large, tappable cards (Linear-style clean typography, generous whitespace, no clutter); middle shows current Lock Score as a calm, non-alarmist number/trend line (Apple Health-style simple line, not a gamified dial); bottom shows a single AI Coach message card, dismissible, never more than one at a time to avoid notification-fatigue-in-UI-form.
- **Check-in flow:** single-purpose modal, minimal steps — select Goal Profile (if multiple active) → capture (photo/video/voice/timer/auto-sync confirmation) → optional short reflection text → confirm. Target: under 15 seconds for the common case, matching Duolingo's "lesson can't feel like a chore" design philosophy applied to check-ins instead of lessons.
- **Progress/Goal Profile detail:** milestone timeline (Notion-style clean checklist/timeline hybrid), historical check-in calendar rendered with neutral (not red/green pass-fail) coloring per Q2 — gaps are visually quiet, not alarming.
- **Pod screen:** simple chat thread plus a compact, opt-in-only leaderboard module at the top (collapsed by default, not the dominant visual element) — the design intentionally under-emphasizes competitive ranking relative to the chat/support function.
- **Profile/Lock Score screen:** Strava-activity-page-inspired layout — a clean summary of verified achievement history, badges/levels, and a shareable card generator (for the external virality loop, Q GTM) that's factual and understated rather than boastful in tone.

### Desktop Experience

Desktop is secondary at launch (mobile-first, matching the check-in-heavy daily-use pattern), but serves coaches and power users well: a dashboard view for coaches managing multiple mentees' programs (V2+), and a richer Goal Profile planning/editing surface (setting up milestones, timelines) that benefits from more screen real estate than a phone check-in flow needs.

### Database Schema (high-level)

Core entities: `users`, `goal_profiles` (user_id, category, target, timeline, visibility), `check_ins` (goal_profile_id, timestamp, verification_tier, source_integration, raw_data_ref, reflection_text), `lock_scores` (user_id, rolling_window_start, computed_score, component_breakdown — recomputed on a schedule, not stored as a single mutable field, to preserve historical auditability), `pods` (cohort_id, season_id, member_user_ids), `pod_memberships`, `integrations` (user_id, provider, oauth_token_ref, last_sync), `challenges`, `challenge_participants`, `coach_profiles` and `coach_programs` (V2+), `moderation_reports`. Verification data from integrations is stored with explicit provenance/source fields throughout — this isn't a schema nicety, it's structurally required for the Lock Score verification-tier system (Tier 2) to function and be auditable.

### Technical Architecture & Recommended Stack

Standard, boring, proven choices are correct here — this product's differentiation is in the data model and product decisions (Lock Score, anti-shame design), not in novel infrastructure, so infra risk should be minimized: React Native for mobile (single codebase, fastest path to iOS/Android parity for a cross-platform-critical product), a typed backend (Node/TypeScript or similar) with Postgres as the primary store (relational integrity matters a lot here — Lock Score computation is fundamentally a relational aggregation problem), a job queue for async Lock Score recomputation and integration syncs, object storage for check-in media, and a thin AI Coach service layer calling a hosted LLM API (Claude or GPT-class) rather than self-hosting models at this stage — the unit economics (Q3) work fine on API pricing at launch scale, and self-hosting is a distraction until usage volume justifies the operational overhead.

### Security & Privacy Model

Verification without surveillance is the core tension: integrations (Apple Health, Strava, GitHub) should pull the minimum data needed for verification (e.g., "a workout occurred on this date matching this duration," not full raw health metrics history), with explicit per-integration, revocable consent, and clear user-facing explanation of exactly what data is used for Lock Score computation versus what's discarded. Sensitive goal categories (mental health, recovery, financial goals) get elevated default privacy (private-to-self or pod-only, never eligible for opt-in-to-global-leaderboard regardless of user preference — a hard product-level guardrail, not left to user choice, because the platform shouldn't put the burden of protecting a vulnerable user on that user's own settings literacy). Data retention and deletion follow standard GDPR/CCPA-grade user rights (export, delete, including the nuance that Lock Score's data-moat design must still fully honor deletion requests — the moat is about aggregate platform data density and relationship depth, not about holding any individual user's data hostage).

---

## Tier 4 — Horizon

### Five-Year Vision

Year 1-2: prove the wedge (certification exams), prove the retention mechanism (return-after-lapse, not streak-length, as the core metric), prove willingness to pay at $15-25/mo. Year 3: Lock Score has enough longitudinal, cross-domain data to function as an actual portable credential — this is the inflection point where LockedIn stops being "an app for CPA candidates" and starts being infrastructure. Year 4-5: employer and institutional partnerships (a hiring manager who trusts a verified 400-day Lock Score the way they'd trust a LinkedIn recommendation, but harder to fake), a mature coach marketplace where Lock Score-verified expertise commands real pricing power, and goal categories expanding well beyond the original wedge (financial goals, creative practice, parenting/family goals) because the underlying primitives — verified check-ins, rolling reputation, anti-shame pod accountability — generalize.

### The Path from "Study-Group App" to "Operating System for Self-Improvement"

The path runs through data, not features: every new goal category and cohort adds to the same underlying Lock Score graph, and the platform's value to any single user compounds as the graph gets denser (more verification integrations, more comparable peers, more coach expertise available) — this is the textbook definition of a platform transition, and it's why the wedge-first sequencing (Q1) isn't just a go-to-market tactic, it's the only viable path to the "operating system" vision. Trying to be the operating system on day one (the "everyone with a goal" trap named at the start of this document) would have produced a shallow, undifferentiated product with no cohort dense enough to prove any of the core mechanics — CPA candidates first is not a smaller version of the vision, it's the only sequence that actually arrives at it.
