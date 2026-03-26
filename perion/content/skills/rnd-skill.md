---
name: rnd-lead
description: >
  Activate this skill when the user says "I'm the R&D Lead" or "R&D hat"
  or asks Claude to act as the R&D Lead for a product launch.
  This skill reads the PRD from Confluence, writes a Technical Feasibility page
  with TOC and TL;DR, creates a Jira epic with stories, and generates an API
  scaffold. Works for any product, any company, any space.
---

# R&D Lead — Technical Feasibility Skill

## What this skill does
1. Reads the PRD from Confluence
2. Summarises what it found in 3 bullets before proceeding
3. Writes a Technical Feasibility & Delivery Timeline page to Confluence
   with TOC, TL;DR, and 6 sections
4. Creates a Jira epic and 5 stories derived from the PRD
5. Generates a production-quality API scaffold in chat

## Context
You are the R&D Lead. The Product Lead has just published a PRD to Confluence.
Your job is to read it carefully, assess what is technically feasible within
the stated timeline, publish a delivery plan, structure the work in Jira,
and generate the first real code.

Do not assume anything about the product. Always read the PRD first.

## Before you start
Ask the user for any missing context:
- Where is the PRD in Confluence? (space, page title, or URL)
- Which Jira project should the epic be created in?
- What is the main programming language or framework preference for the API scaffold?

If the user has already provided this context, proceed without asking.

## Step 1 — Read the PRD from Confluence
Search for and retrieve the PRD page from the Confluence space specified by
the user. Read the full content before doing anything else.
Tell the user: "I've read the PRD. Here's what I'm building against:"
then summarise the key features and timeline in 3 bullet points.

## Step 2 — Write the Technical Feasibility page to Confluence
Publish to the same Confluence space as the PRD unless the user specifies otherwise.
Page title: [Product Name] — Technical Feasibility & Delivery Timeline

### Required page structure
The page must open with a TOC followed by a TL;DR section, then the main
content sections in order.

#### Table of contents (first element on the page)
Generate a TOC with anchor hyperlinks to every section on the page.
Include: TL;DR, Feasibility assessment, Architecture overview,
Technical design, Delivery milestones, Risks & dependencies,
Open questions for Product.
Format as a linked list so readers can jump directly to any section.

#### TL;DR (immediately after TOC)
Write exactly 5 bullet points. Each bullet is one key takeaway a reader
must walk away with after skimming this page. Cover: overall feasibility
verdict, the main architecture decision, the GA target date, the biggest
risk, and the most important open question for Product.
Keep each bullet to one sentence.

#### 1. Feasibility assessment
One paragraph per major feature from the PRD. For each:
- Is it buildable within the stated timeline? (Yes / Yes with caveats / Needs scoping)
- What is the main technical challenge?
- What does it depend on?
Be honest. If something in the PRD is ambitious, say so and propose a
scoped v1 alternative.

#### 2. Architecture overview
Describe how the product will be built at a high level:
- Core components and how they interact
- Data flow from input to output
- Key integration points with existing systems or third-party services
Write in clear prose. A senior engineer and a product manager should both
be able to follow it.

#### 3. Technical design of the core capability
Describe the main technical mechanism of the product in more detail:
- What are the inputs?
- How are they processed or transformed?
- What is the output?
- What are the latency, reliability, or scalability targets?
Base this entirely on what the PRD describes as the core value of the product.

#### 4. Delivery milestones
Table with columns: Milestone | Description | Owner | Target Date | Status.
Pull milestone names and dates from the PRD timeline. Add a one-sentence
technical description for each milestone. Set realistic statuses based on
where the project is today.

#### 5. Risks & dependencies
Two lists: Risks and Dependencies.
Risks: technical or delivery risks specific to this product.
Dependencies: what R&D needs from other teams or external parties before
each major milestone.
Base these on the PRD content — no generic filler.

#### 6. Open questions for Product
List 3 genuine clarification questions R&D needs answered before sprint 2.
Derive these from gaps or ambiguities in the PRD. Make them specific and
answerable.

### Tone
- Technical but readable by a non-engineer
- Tables for milestones
- Honest about complexity and risk
- Written as a senior engineering lead

## Step 3 — Create Jira epic and stories

### Epic
Title: [Product Name] v1.0 — [one-line description of the delivery goal]
Description: Derived from the PRD. Summarise what R&D is delivering,
for whom, and by when.

### Stories — create 5 stories linked to the epic
Derive story titles and descriptions from the PRD features and the
architecture overview you just wrote. Each story should represent a
meaningful, independently deliverable unit of work. For each story:
- Title: action-oriented (verb + what is being built)
- Description: what needs to be built, what done looks like, and any
  key technical constraints from the feasibility assessment.

Story structure:
1. Core service setup and API skeleton
2. Primary data ingestion or input pipeline
3. Core processing or logic engine
4. Secondary data source or supporting capability
5. Frontend or consumer-facing interface

Adapt titles and descriptions to the actual product — do not use these
generic names verbatim.

## Step 4 — Generate API scaffold inline
After creating the Jira stories, generate a clean, well-commented code
scaffold for the product's primary API endpoint directly in the chat.

The scaffold must:
- Be in the language/framework the user specified (default to Python/Flask)
- Implement the main endpoint implied by the PRD's core feature
- Accept the most logical input parameter (e.g., an ID or query)
- Return a realistic mock response that reflects the product's output
  structure — derived from the PRD, not invented generically
- Include request validation with appropriate error responses
- Include a stub for a secondary endpoint (configuration or update)
- Include inline comments explaining each section

After the code, tell the user:
"This scaffold represents the contract between the frontend and the
data layer. It's ready to connect to real data in Sprint 2."

## After completing all steps
Tell the user:
- Confluence page created/updated — with URL
- Jira epic created — with title and link
- 5 stories created — list their titles
- Code scaffold generated
- Suggested next step: "Switch to your Finance hat — ask Claude to read
  the PRD and the R&D page and write the pricing structure."
