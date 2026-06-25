# If your ICP is just a filter, you have nothing to say

- **Author:** Jordan Crawford
- **URL:** https://edge.blueprintgtm.com/p/if-your-icp-is-just-a-filter-you
- **Published:** 2026-05-09
- **Source:** Newsletter/blog scraped via Firecrawl (Note: full post is partially paywalled; the free portion is captured below.)

---

### I built a skill that works backward from won, lost, healthy, churned — finds the signals headcount-and-vertical can't.

_May 6, 2026 · Build log_

Your ICP is lazy.

"50 to 1,000 employees in vertical X." That's not an ICP. That's an Apollo filter. You've described a list of companies the same way Apollo describes a list of companies, and you've told yourself you've done strategy.

The companies that write you the biggest checks and stay the longest don't share a headcount band. They share a _situation_. A specific operational thing that happened to them six to eighteen months before they bought, that almost nobody else on the filter is going through right now. That's the actual segment. Headcount and vertical are how Apollo organized the world. They're not how your customers feel pain.

So I spent the day building a skill that does ICP the other direction. You start from the outcomes you already have — your wins, your losses, your healthy accounts, your churns — and you reconstruct what those companies _looked like_ before they bought. You hunt for signals you can pull from public data that distinguish good-fit from bad-fit. You ship a per-archetype scoring rubric instead of a one-line firmographic.

It's called `win-loss-rewind`. Annual subscribers can install it today. Below is the story of building it.

## Outcomes first, hypotheses later

The old workflow: someone in marketing writes "we sell to mid-market HR teams in financial services," everyone nods, the SDRs go work the list, and three months later half the closed-wons are credit unions and the other half are insurance brokerages and nobody's HR team makes the buying decision. The ICP didn't predict anything. It just sounded reasonable.

The new workflow inverts it. You take the customers you actually have, label each one with the outcome that matters — won, lost, healthy, churned, expanded — and treat that as ground truth. Then you ask what those four buckets had in common _before_ you ever spoke to them. Not what they look like now. What they looked like when they walked in.

This is the move Munger's been on his whole career. Invert, always invert. You don't ask "what makes a customer good?" — that's the question that gives you "mid-market vertical X." You ask "what was different about the customers who won versus the ones who didn't?" That question forces specificity. There's always a difference. Sometimes the difference isn't even something you'd have thought to look for.

## Distrust your own data first

I almost shipped this thing without Phase 0 and it would've been useless.

Here's what kept happening on test data. The CRM record says "$50K ARR, healthy customer, expansion in flight." Cool. Then I run Firecrawl on their domain and LinkedIn enrichment on their org and discover the company has one employee, no working website, and the LinkedIn page hasn't been updated in two years. That's not a customer. That's a CRM record. Whoever logged the deal moved on, the account auto-renewed once, and now the system thinks they're a healthy expansion target.

You can't build an ICP discriminator on top of records like that. The training data is poisoning the answer.

So Phase 0 of the skill is just sitting on the data and not trusting it. It cross-references CRM labels against external reality — does the company exist on LinkedIn, does the website resolve, does the headcount match what the CRM thinks. Anything that fails gets quarantined. The operator gets a `data_confidence.md` to review and approve before the rest of the pipeline runs.

This step isn't glamorous and most teams skip it. It's also the step that determines whether the rest of the work means anything.

## What the deliverable actually looks like

Skip ahead to what comes out the other end. Here's a real example from the fictional GRC SaaS test fixture I shipped with the skill — a compliance-automation product with two customer archetypes hidden in the data:

```
Archetype: Two-state legal-ops shop,
           no in-house engineer

Signal 1: State professional registrations
          in prior 18mo
  Source:     state SoS portal
  Threshold:  >= 2
  Weight:     0.55
  Lift:       4.1x train / 3.6x holdout

Signal 2: Compliance/GRC role posted
          in prior 6mo
  Source:     Firecrawl careers (keyword)
  Threshold:  present
  Weight:     0.45
  Lift:       3.5x train / 3.2x holdout

Combined fit_score
  = 0.55 * I(reg) + 0.45 * I(role)

"Looks like archetype" threshold:
  fit_score >= 0.60
```

That's the ICP. Two operational signals from public data. A weighted score. A threshold. A measured lift on training data and on a held-out 20% you didn't show the model.

Look at what's _not_ in there. No headcount band. No vertical. No revenue range. None of the things you'd find on an Apollo filter. Because none of those things actually distinguish good-fit from bad-fit for this archetype. What distinguishes them is _did this company recently expand into a second state and hire someone to own the compliance work that follows_. That's the pain segment. Everything else is noise.

The other archetype in the same fixture comes out totally different — engineering-shops who built their own compliance code internally, then watched their compliance-tagged GitHub repos go quiet for nine months because the engineer who maintained them moved on. Same company-stage. Same revenue band. Completely different signal recipe.

You'd never write the ICP "compliance-tagged GitHub repos went quiet for nine months" by hand. You'd never think to. The skill writes it for you because it works backward from who actually won.

## The vowel-name signal that died at holdout

Here's the moment I trust the work.

When the skill generates hypotheses about what distinguishes wins from losses, it generates a lot of them. Most are good. Some are nonsense. The hard part is figuring out which are which without a human reviewing every one.

In the test fixture, the hypothesis-generator coughed up something like "won customers tend to have company names starting with vowels." Apex, Atlas, Echo, Oak — four out of twelve wins, which on a small training set is a real-looking pattern. Train-set lift: about 2.4x.

It's also obviously horseshit. Company names don't predict buying behavior. The hard gates should kill it at Phase 5 because it doesn't prove pain — and they did, in this case. But suppose they hadn't. Suppose it slipped through.

Phase 6 is the safety net. You hold out 20% of your data from the start, never let any of the hypothesis-generation see it, and at the end you re-test every surviving hypothesis on the holdout. The vowel-name signal collapses to lift ≈ 1.0 on the holdout because it was a coincidence in the training set. Dead.

The real signals — state registrations, compliance roles — hold their lift on the holdout. Train 4.1, holdout 3.6. Train 3.5, holdout 3.2. They survive because they're not artifacts. They reflect actual operational pain.

This is the difference between an ICP you trust and an ICP you've fooled yourself into. You hold out 20%. You test on it. Anything that doesn't survive doesn't ship.

## So what do I do with this

If you're staring at your own customer list right now and your ICP is some version of "mid-market vertical X," here's the move. Pull your wins, your losses, your healthy accounts, your churns. Get the outcome label honest — not what the CRM says, what actually happened. Then ask the question backward: what was different about the wins, six to eighteen months before close, in their public data?

Run that question with discipline. Hold out 20% of the data. Force every hypothesis through a "this proves pain, not just correlation" filter. Reject anything that uses headcount, industry, or revenue as the discriminator — those are inputs, not signals. The signals you want are the operational events that _preceded_ the buying behavior.

That's the work. The skill automates it. But the discipline is what makes the answer real.

_— Written by Claude Opus 4.7, approved by Jordan_

[Remainder of post is for paid subscribers.]
