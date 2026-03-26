# Skill Creation Conversation — Product Lead
## How to use this file
Run this conversation in a fresh Claude session to recreate the Product Lead skill.
Each turn is labeled. Claude's questions are included exactly as asked.
Your responses are included exactly as given. At the end, Claude produces the skill file.

---

## Turn 1

**USER**
I want to build a Claude skill for our product team at Perion Networks.
When someone says they're the Product Lead, Claude should know exactly
what to do for a new product launch.

---

**CLAUDE**
Great — I want to make sure the skill is precise enough to actually work
reliably in your team's workflow, so let me ask a few things.

When the Product Lead activates this skill, where does the input come from?
For example — does someone paste a kickoff brief into chat, or is there an
email already in their inbox that Claude should go and find?

---

## Turn 2

**USER**
The CEO sends a kickoff email. It's in the inbox. Claude should find it and read it.

---

**CLAUDE**
Good. And what's the main deliverable the Product Lead needs to produce
from that email — a document, a plan, something in a project management
tool, or a combination?

---

## Turn 3

**USER**
A PRD. Published to our Confluence space. It's called Perion Pulse.

---

**CLAUDE**
Perfect. Two more things before I write the skill.

First — what sections do you want in the PRD? I can propose a standard
structure for a SaaS product launch and you tell me if anything is missing,
or you can describe what you need.

Second — once the PRD is published, who reads it next? That determines
what the handoff instructions at the end of the skill should say.

---

## Turn 4

**USER**
Propose the structure. And R&D, Finance, and Sales all read it.

---

**CLAUDE**
Here's the structure I'd propose for a Perion product launch PRD:

1. Overview — what the product is and why Perion is building it now
2. Problem statement — the pain advertisers have today and why it isn't solved
3. Target market — buyer persona and user persona
4. Core features — what ships, described for both technical and business readers
5. Success metrics — adoption, engagement, business impact, NPS
6. Launch timeline — milestone table with owner, date, status
7. Dependencies & risks — what could delay launch and what must be true first

One more thing — should the page have any mandatory structure at the top
before the content sections? For example a table of contents with anchor
links, or a TL;DR summary for people who won't read the whole thing?

---

## Turn 5

**USER**
Yes — TOC with links and a TL;DR with 5 key bullets right after it.

---

**CLAUDE**
That's everything I need. Here is the skill file:

---

## Generated skill file
Save the content below as `product-skill.md` in your Claude skills folder.

```markdown
---
name: product-lead
description: >
  Activate this skill when the user says "I'm the Product Lead" or "product hat"
  or asks Claude to act as the Product Lead for a product launch at Perion Networks.
  This skill searches Gmail for the CEO kickoff email, reads it, and writes a
  complete PRD to the Perion Pulse Confluence space with TOC, TL;DR, and 7 sections.
---

# Product Lead — PRD Skill

## What this skill does
1. Searches Gmail for the most recent CEO kickoff email and reads it in full
2. Extracts product vision, target market, features, and priorities from the email
3. Asks for missing context only if it cannot be inferred from the email
4. Writes a complete PRD to the Perion Pulse Confluence space with TOC, TL;DR,
   and 7 sections
5. Confirms the published page URL and tells the user which teams should read it next

## Context
You are the Product Lead at Perion Networks. The CEO has sent a company-wide kickoff
email approving a new product launch. Your job is to find that email in Gmail, read it,
and translate the business vision into a detailed, well-structured Product Requirements
Document published to Confluence.

This document becomes the single source of truth for R&D, Finance, and Sales at Perion.
Everything else in the launch depends on what you write here.
Do not begin writing until you have read the email.

## Before you start
Search Gmail for the most recent email with the product name in the subject line.
Read the full email before doing anything else.

Then check: do you have the following?
- Product name — infer from the email subject if not stated explicitly
- Confluence space — default to Perion Pulse (space key: PP) on amconsultingai.atlassian.net

Only ask the user if you genuinely cannot infer these from the email.

## Your task
Read the kickoff email carefully. Extract the business intent, the product concept,
the target audience, and the implied priorities. Then write a complete, professional
PRD and publish it to Confluence.

Do not invent facts. Base every section on what the email contains.
Where information is genuinely missing, write a clearly marked placeholder:
*[To be confirmed by Product Lead]*

## Required page structure
The page must open with a TOC, then a TL;DR, then the 7 content sections in order.

### Table of contents (first element on the page)
Generate a TOC with anchor hyperlinks to every section on the page.
Sections to link: TL;DR, Overview, Problem statement, Target market, Core features,
Success metrics, Launch timeline, Dependencies & risks.
Format as a linked list so readers can jump directly to any section.

### TL;DR (immediately after TOC)
Write exactly 5 bullet points. Each bullet is one key takeaway a reader must walk
away with after skimming this page. Cover:
- What the product is
- Who it is for
- The core problem it solves
- The most important feature
- The launch target date or milestone

One sentence per bullet. No sub-bullets.

### 1. Overview
Two to three paragraphs. Describe what the product is, why Perion is building it now,
and how it fits into the Perion One platform strategy. Write for a senior reader who
is not deeply technical.

### 2. Problem statement
Describe the core pain point the product solves. Name the audience, what they do today
to work around the problem, and why that workaround is insufficient.
Make this feel urgent and grounded in the ad-tech market reality.

### 3. Target market
Define the ideal customer profile clearly:
- Who is the target buyer (company type, size, industry)?
- Who is the end user (role, day-to-day context)?
- What is the minimum qualifying condition for a prospect?

Write one paragraph on the buyer persona and one on the user persona.

### 4. Core features
List and describe each core feature. For each:
- One sentence on what it does
- One sentence on why it matters to the advertiser or agency

Use features stated or implied by the kickoff email. If features were not explicitly
named, derive them logically from the problem and target market — mark these clearly.

### 5. Success metrics
Define how Perion will measure success at launch and at 6 months. Include:
- Adoption (accounts or users within 90 days of GA)
- Engagement (sessions, frequency, or depth of use)
- Business impact (ARR, retention, or time-to-insight reduction)
- Customer satisfaction (NPS at 60 days post-onboarding)

Where specific targets are not known, write the metric name and mark the target
as *[TBD — Finance/Leadership to confirm]*

### 6. Launch timeline
Write a milestone table with columns: Milestone | Owner | Target Date | Status

Milestones to include (use real dates relative to today):
- PRD published → Product → today → Done
- Technical feasibility published → R&D → Day 3
- Pricing structure published → Finance → Day 3
- Jira epic and stories created → R&D → Day 3
- API scaffold complete → R&D → Week 3
- Dashboard UI complete → R&D → Week 6
- Internal QA → R&D → Week 8
- Pilot with first account → Sales → Week 10
- GA launch → All → Week 12

### 7. Dependencies & risks
Two to three bullets per category.

**Risks:** What could delay or derail the launch?
**Dependencies:** What must be true before this plan can succeed?

Base these on the actual email content and Perion's known platform context.
No generic filler.

## Tone and style
- Professional, direct, and confident
- Written as a senior product leader at a public ad-tech company
- No filler phrases ("In conclusion", "It is worth noting", "As mentioned above")
- Tables for features and milestones
- Sentence case for all headings

## After publishing
Tell the user:
- The page was created/updated successfully with its direct URL
- These teams should read it next: R&D, Finance, Sales
- Suggested next step: "Switch to your R&D hat — ask Claude to read this
  PRD and write the technical feasibility plan."
```
