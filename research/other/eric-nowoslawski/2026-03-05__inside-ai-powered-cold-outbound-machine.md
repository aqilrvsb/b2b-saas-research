# Inside Eric Nowoslawski's AI-Powered Cold Outbound Machine

- **Author:** Eric Nowoslawski (interviewed by Brendan J Short, The Signal)
- **URL:** https://www.thesignal.club/p/inside-eric-nowoslawskis-ai-powered-cold-outbound-machine
- **Published:** 2026-03-05
- **Source:** Newsletter/blog scraped via Firecrawl

---

### How he runs 250 Clay tables simultaneously, wrote 2M lines of code without being a developer, and cut his OpenAI bill from $15K/mo by renting his own GPUs

I recently sat down with Eric Nowoslawski to talk about how he's building one of the most technically advanced AI-powered cold outbound machines in the world.

In fact, he may be the _best_ person I know when it comes to modern-day outbound. Hard stop.

Eric runs Growth Engine X, which has 52 concurrent clients (he's worked with companies like Notion, Intercom, Instantly.ai, Clay, and Secureframe), he rips 2 billion tokens per day through OpenAI, and has 250 Clay tables running simultaneously.

Maybe most interestingly, he's also never written a line of code. Until 45 days ago, when he started using Cursor and Claude Code. But since then, he's written 2 million lines of code.

### Claude Code vs. Clay: When do you use each?

A year ago, the people I knew who were going all-in on Clay have added Claude Code to their stack since the start of this year.

Eric's take: It's an obvious evolution. Clay's original hypothesis was to give software engineering powers to as many people as possible. They thought a spreadsheet interface would help visualize integrations since people were used to Excel.

But Claude Code gives software engineering capabilities to everyone on another level. Instead of setting up columns and clicking around, you can use your voice to set things up. And it compounds—when you figure something out once, you save it and reuse it.

**Why Clay still matters:**

1. **Edge cases and visual building.** Even with perfect models, some edge cases are easier to solve with a visual builder.
2. **Software maintenance.** People underestimate how much effort it takes to maintain code. Eric had something working perfectly two days ago—it's broken now.
3. **Claygent.** Still a marvel of a GTM feature.
4. **API queuing.** Clay's native integrations handle rate limits automatically. If Prospio has a 10 requests/second limit and you're hitting it across 50 tables, Clay manages that. With Claude Code, you'd have to build that yourself.
5. **Pre-negotiated contracts.** Clay has 150+ data providers. Maybe you just want one data point from HG Insights—do you want an HG Insights contract, or do you want to spend a few Clay credits?

Eric's current split: Claude Code handles TAM building and email finding. Then everything flows into Clay for "final mile delivery"—whatever AI enrichment needs to happen, Claygent calls, and pushing leads into SmartLead.

### The GTM tech stack: flexibility vs. power

A visual of how GTM tools trade off ease of use against flexibility and power:

- **Bottom right:** Incumbent data and sequencing tools. Super easy to use, but not very flexible or powerful.
- **Middle:** Signal-based tools that productized signals/automation (person-level intent better than 6Sense/Demandbase). More powerful, but harder to use.
- **Further up:** Clay. Pretty hard to use, but very flexible and powerful.
- **Even further:** n8n and Make.
- **Very top left:** Hand-coding something (Cursor, Claude Code, etc.). Most powerful and flexible, but historically the hardest to use.

All of these tools are rapidly getting easier to use as vibe coding improves. For GTM leaders, the question isn't "which tool should I use?" It's "where on this spectrum should my team be investing time?" The answer is probably: move up the curve faster than you think you should.

Tools Eric uses day-to-day: Prospeo (contact/company data), RapidAPI, Clay (orchestration/final mile), Apify (scraping), Exa and Parallel.ai (AI search), Supabase (database), Railway (internal apps), Trigger.dev (background jobs).

### How should GTM teams learn AI coding?

His answer: Everyone needs to use these tools. It's mandatory.

**We're in a bubble.** Most of the world has not "seen the light" yet. We think everyone knows how easy it is to scrape Google Maps or enrich a CRM. They don't. The problems are basic. The solutions are now accessible. That's the gap.

**Five things everyone in GTM should try with Claude Code:**

1. **Customer insight discovery.** Look at your CRM—leads from last month, closed deals, lost deals. Find patterns.
2. **Basic TAM building.** Connect to an API like Prospio. Pull your entire TAM into a database.
3. **Build your own database.** Pay $3 for Supabase. Get used to having your own data infrastructure.
4. **Analyze your recorded calls.** Pull all your calls, ask Claude how to improve.
5. **Build your own email finder.** Guess the six most common email permutations, validate all with a MillionVerifier account. The one that comes back valid is the email.

**AI scales your existing quality.** AI doesn't replace people; it scales whatever you already have. If you're good at writing emails, AI scales good emails. If you're sending bad emails, it scales bad emails. The companies that will win have strong fundamentals—good positioning, offers, copy—then use AI to scale them.

### The marshmallow test for building internal tools

Eric used to spend four hours every Friday on domain management (pull all domains, get reply rates for 7/14-day windows, flag underperformers, rotate backups, order new domains, update Supabase).

**The framework:**
1. What is the overall thing you want to accomplish?
2. What are the tiny steps within that?
3. What API documentation is tied to each step?
4. What does "done" look like for each step—not just the end?

**The marshmallow test:** The teams that win build version one, make sure it works, then build version two on top. Don't have Claude build the whole thing—build itty bitty fraction steps and verify each one.

**Bonus: The Loom transcript trick.** When doing something manually, record a Loom while narrating each step. Give the transcript to Claude. You got the work done AND have documentation for automation. The transcript becomes the prompt.

### How Eric cut a $15K/month OpenAI bill

**Solution 1: Batch API.** For high-volume clients (30,000-100,000 emails/day), plan out every lead and process them in a single, cheaper batch.

**Solution 2: Cached Inputs.** If you send the same prompt prefix repeatedly, OpenAI gives you 50% off input tokens for the cached portion. The trick: move the variable data to the END of the prompt, keep the instruction layer static. That triggers cached inputs more often.

**Future: Rented GPUs.** Eric went down a rabbit hole on Vast.ai—renting GPUs to process AI requests for $0.60/hour. At scale, a million requests per day for $12-13. First use case: Google Maps contact finding.

## Top 3 changes in outbound in the last 6 months

**1. Domains are dying faster than before.** Domains get burned quicker. You need a system to monitor reply rates (below 0.7% = cancel) and backup domains ready to rotate in. For most companies, SmartLead or Instantly solves this.

**2. LinkedIn strategy (don't orchestrate with email).** You can send way more emails than LinkedIn messages. Use LinkedIn sparingly for three plays:
- **Monitor case study company pages.** When someone in your ICP engages with a post from your case study company, reach out: "I'm a video agency and I do the video stuff for Clay. Would love to talk."
- **Website de-anonymization.** Install Leadfeeder, Snitcher, RB2B, Visual Visitor. Use free trials. Keep whichever gets highest reply rate. Automate LinkedIn messages to site visitors.
- **Competitor content engagement.** Anyone in your ICP engaging with competitors' content gets a normal outreach message (don't mention the engagement).

**3. Email as an ad platform.** Cold email has become an ad channel. Facebook's best advertisers run 50+ ads simultaneously because Facebook makes orchestrating tests easy. Now with Claude Code, set up SmartLead campaigns programmatically, distribute inboxes, write if-then routing, launch 20 campaigns in one go. Treat cold email like Facebook ads. Run 20-50 campaigns at once. Test subject lines, CTAs, case studies, offers.

### TAM requirements: Why 100K contacts is the minimum

Eric believes you need 100K contacts in your market to do automated outbound (especially with an agency). He won't take clients with fewer than 100,000 contacts in their TAM. Paying an agency for a 4,000 account TAM doesn't make sense—you'll run out of people to email in a month or two. Those companies should set it up themselves with Instantly or Smartlead for $500-1,000/month and do less scale.

### Summary key themes

1. We're in a bubble. Most people have no idea what's possible.
2. Claude Code is the next tool in the stack (but Clay still has a role).
3. Move up the flexibility/power curve.
4. The leadership mandate is real: "You MUST use these tools."
5. Start small with AI coding. Break everything into micro-steps.
6. AI scales your existing quality.
7. Treat email like ads. Run 20-50 simultaneous campaigns.
8. 100K TAM minimum. If you can't scale, don't pay agency fees.

**Follow Eric Nowoslawski on LinkedIn** (https://www.linkedin.com/in/outboundphd/) — He posts daily on cold outbound and AI-powered GTM. Eric runs Growth Engine X (https://www.growthenginex.com/).
