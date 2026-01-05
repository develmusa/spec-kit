---
description: Create a Lean Canvas and business strategy document that crystallizes validated insights into a formal business plan.
handoffs: 
  - label: Create Product Requirements
    agent: speckit.productize
    prompt: Create PRD from business strategy
    send: true
  - label: Back to Ideation
    agent: speckit.ideate
    prompt: Revisit and refine synthetic validation
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Overview

The `/speckit.strategize` command converts your validated insights from `/speckit.ideate` into a structured business strategy using the **Lean Canvas** framework. This creates the "Business Source of Truth" that guides all subsequent product and technical decisions.

This is **Phase 1** of the Context-First Framework, bridging idea validation and product definition.

## Prerequisites

Before running this command:
- [ ] `/speckit.ideate` has been completed
- [ ] Ideation document exists at `.specify/business/01_ideation.md`
- [ ] Synthetic validation revealed positive signals to proceed

If ideation hasn't been run, prompt the user to complete it first.

## Workflow

### Step 1: Load Ideation Insights

Read `.specify/business/01_ideation.md` and extract:
- **Validated personas**: Who are the real target customers?
- **Critical pain points**: Top problems identified by multiple personas
- **Must-have features**: Features 3+ personas prioritized
- **Key objections**: Concerns that were raised and need addressing
- **Assumptions challenged**: Insights that changed the original idea

### Step 2: Create Lean Canvas

Using the template at `templates/business/strategy-template.md`, populate the Lean Canvas with specific, concrete details:

#### Problem (Top 3 Problems)

Extract from ideation:
- Which pain points did MULTIPLE personas mention?
- Which problems are most urgent/painful (pain intensity)?
- Which are currently UNSOLVED by existing solutions?

**Format:**
```markdown
| **Problem** | <ul><li>[Most critical problem - mentioned by X personas]</li><li>[Second problem - mentioned by Y personas]</li><li>[Third problem - mentioned by Z personas]</li></ul> |
```

#### Customer Segments

Based on persona analysis:
- **Primary segment**: The persona type that showed HIGHEST pain + willingness to pay
- **Early adopters**: Which personas are most likely to try new solutions? (Usually high-tech, high-pain, or existing solutions failing them)

**Format:**
```markdown
| **Customer Segments** | <ul><li>Primary: [Most promising persona archetype]</li><li>Early Adopters: [Persona types willing to try beta/MVP]</li></ul> |
```

#### Unique Value Proposition

Synthesize a single, compelling message that:
- Addresses the TOP problem
- Differentiates from alternatives personas mentioned
- Uses language/phrasing from persona quotes

**Template**: "Unlike [existing solution], [Product Name] [unique approach] for [target customer]"

**Example**: "Unlike project management tools that require training, TaskFlow uses natural language so construction foremen can manage crews from their phone in under 60 seconds"

#### Solution (Top 3 Features)

Pull from "Must-Have Features" in ideation:
- Features that 3+ personas prioritized
- Features that address the top problems
- Focus on WHAT, not HOW

**Format:**
```markdown
| **Solution** | <ul><li>[Feature addressing Problem 1]</li><li>[Feature addressing Problem 2]</li><li>[Feature addressing Problem 3]</li></ul> |
```

#### Channels

Based on persona profiles:
- Where do these personas discover new tools?
- What communities/networks are they part of?
- Who influences their decisions?

**Common channels by persona type:**
- **Enterprise personas**: LinkedIn, industry conferences, analyst reports, peer referrals
- **Startup/Tech personas**: Product Hunt, Twitter/X, HN, dev communities
- **SMB personas**: Google search, industry forums, YouTube tutorials
- **Consumer personas**: TikTok, Instagram, influencer recommendations, app stores

#### Revenue Streams

Define based on:
- Persona willingness to pay (from ideation)
- Standard pricing models in the space
- Whether this is B2B, B2C, or B2B2C

**Examples:**
- B2B SaaS: "Monthly subscription: $X per user per month"
- Freemium: "Free tier + premium at $X/month"
- Marketplace: "Transaction fee of X% on completed transactions"
- One-time: "One-time purchase of $X"

#### Cost Structure

Estimate initial costs:
- **Customer Acquisition Cost (CAC)**: Based on chosen channels
- **Development**: MVP development time/cost
- **Infrastructure**: Hosting, tools, services
- **Operations**: Support, maintenance

Be realistic. Use industry benchmarks if unsure.

#### Key Metrics

What numbers indicate success? From persona insights:
- **Activation**: [e.g., "Users create first project within 24 hours"]
- **Engagement**: [e.g., "Users log in 3+ times per week"]
- **Retention**: [e.g., "80% of users active after 30 days"]
- **Revenue**: [e.g., "Monthly Recurring Revenue (MRR)"]
- **Growth**: [e.g., "20% month-over-month user growth"]

#### Unfair Advantage

Something that CANNOT be easily copied or bought:
- **Network effects**: Gets better with more users
- **Proprietary data**: Unique dataset competitors don't have
- **Expert team**: Domain expertise that takes years to build
- **Partnerships**: Exclusive relationships
- **Timing**: First-mover in emerging space

⚠️ **Common mistakes** (these are NOT unfair advantages):
- "Our team is passionate" (anyone can be passionate)
- "We'll execute better" (not measurable)
- "Superior technology" (can be copied)

If you truly have no unfair advantage, be honest: "None yet - relying on execution speed"

### Step 3: Write System Context

This is THE MOST IMPORTANT section. It becomes the foundation for all technical decisions.

#### What This Business IS

Write 2-3 paragraphs that define:
- **Core value proposition**: What problem for whom?
- **Business model**: How does money flow?
- **Target customer**: Specific segment, not "everyone"
- **Competitive positioning**: How you're different
- **Key metrics**: How you measure success

**Example:**
> TaskFlow is a mobile-first project management tool built specifically for field service teams in construction, HVAC, and electrical trades. Unlike enterprise PM tools designed for office workers, TaskFlow uses voice-to-text and simple tapping interfaces that work for foremen managing 5-15 workers on job sites. We make money through a $15/user/month subscription paid by contracting companies. Our primary customers are GCs and specialty contractors with 10-100 employees who currently manage work through text messages, paper checklists, and whiteboard photos. We measure success through daily active usage (target: 80%) and project completion velocity (target: 20% faster than paper-based workflows).

#### What This Business IS NOT

Be explicit about exclusions to prevent scope creep:

**Format:**
```markdown
- **NOT** [Adjacent market you're avoiding] - [Why]
- **NOT** [Feature set you won't build] - [Why]
- **NOT** [Business model you're rejecting] - [Why]
- **NOT** [Customer segment you're excluding] - [Why]
```

**Example:**
```markdown
- **NOT** a general-purpose project management tool for all industries
- **NOT** a document collaboration platform (no file versioning, no real-time co-editing)
- **NOT** a free consumer app (requires company subscription)
- **NOT** targeting solo freelancers or enterprise companies over 500 employees
```

### Step 4: Conduct Premortem Analysis

Imagine it's 2 years in the future and the business failed. What went wrong?

Create **5 failure scenarios** across different risk categories:

#### Category Examples:
1. **Product-Market Fit**: "We built a solution nobody wanted"
2. **Competition**: "A competitor crushed us"
3. **Execution**: "We ran out of money before finding traction"
4. **Market Timing**: "We were too early/too late"
5. **Unit Economics**: "CAC was higher than LTV"

For each scenario:

```markdown
### Failure Scenario [N]: [Category]

**What went wrong**: [Specific, detailed failure story]

**Early warning signs**:
- [Measurable signal you'd see 3-6 months before failure]
- [Another early indicator]
- [Another early indicator]

**Mitigation strategy**:
- [Concrete action to prevent or detect this failure mode]
```

**Example:**
```markdown
### Failure Scenario 1: Product-Market Fit

**What went wrong**: Field workers loved TaskFlow during demos, but actual daily usage dropped to 10% after the first week. Teams went back to text messages because our app required too many taps to update job status. We built features managers wanted, not features workers needed.

**Early warning signs**:
- Users completing onboarding but not creating 2nd project
- Session length under 2 minutes (just checking, not doing work)
- Support tickets about "too complicated" or "just give me a checkbox"

**Mitigation strategy**:
- Shadow 10 field workers for full shifts before building MVP
- Weekly on-site user testing with actual workers (not managers)
- Implement 1-tap status updates in MVP (no multi-step workflows)
```

### Step 5: Refine Customer Profile

Based on Lean Canvas, create detailed target customer profile(s):

```markdown
### Primary Customer Segment

- **Demographics**: [Age, location, income, job role - be specific]
- **Psychographics**: [Attitudes, values, behaviors]
- **Current Behavior**: [Exactly how they solve this problem today - name specific tools/methods]
- **Pain Intensity**: [Rate 1-10 how badly they feel this pain]
- **Willingness to Pay**: [Specific budget range they have for solutions]
- **Decision Process**: [Who decides to buy? How long does it take? What criteria do they use?]
```

### Step 6: Define Go-to-Market Strategy

Create a 3-phase roadmap:

**Phase 1: Launch (Months 0-3)**
- Goal: [First 10 customers? Product-market fit validation?]
- Target: [Specific sub-segment, by name if possible]
- Channels: [The 1-2 channels you'll focus on]
- Success Metrics: [How you know Phase 1 worked]

**Phase 2: Growth (Months 3-12)**
- Goal: [Scale to $X revenue? Expand to new segment?]
- Target: [Broader market or adjacent segment]
- Channels: [Proven channels + 1-2 new experiments]
- Success Metrics: [Targets for this phase]

**Phase 3: Scale (Months 12-24)**
- Goal: [Market leader? Sustainable unit economics?]
- Target: [Full addressable market]
- Channels: [Optimized mix]
- Success Metrics: [Long-term targets]

### Step 7: Document Assumptions & Dependencies

#### Critical Assumptions

List 3-5 assumptions that, if wrong, would kill the business:

```markdown
1. **[Assumption]**: [What you're assuming is true]
   - **How to validate**: [Specific test/experiment]
   - **Timeline**: [When you'll validate this - before MVP? During beta?]
```

**Example:**
```markdown
1. **Assumption**: Construction foremen will trust a mobile app for managing $100K+ projects
   - **How to validate**: Shadow 5 foremen, measure current pain with existing tools, test willingness to adopt
   - **Timeline**: Before starting MVP development (Month 0)
```

#### External Dependencies

What must be true that you DON'T control?

```markdown
1. **[Dependency]**: [What you depend on]
   - **Risk level**: High/Medium/Low
   - **Mitigation**: [Backup plan]
```

### Step 8: Analyze Competition

Create competitive landscape table:

```markdown
| Competitor | Strengths | Weaknesses | Our Advantage |
|------------|-----------|------------|---------------|
| [Name] | [What they do well] | [Where they fall short for YOUR customer] | [Why customer would choose you] |
```

**Include:**
- 3-4 direct competitors
- 2-3 indirect competitors / substitutes (e.g., "Excel + Email")

### Step 9: Save and Report

Save complete strategy to `.specify/business/02_strategy.md`

Present summary to user:

```markdown
## Business Strategy Complete

📄 **Artifact created**: `.specify/business/02_strategy.md`

### Your Business at a Glance

**Value Proposition**: [One sentence]
**Target Customer**: [One sentence]
**Revenue Model**: [One sentence]
**Unfair Advantage**: [One sentence]

### Critical Risks Identified
1. [Top risk from premortem]
2. [Second risk]
3. [Third risk]

### Assumptions to Validate ASAP
1. [Most critical assumption]
2. [Second assumption]

### Next Steps

Your business strategy is now your "source of truth." Ready to define the product?

\`\`\`
/speckit.productize
\`\`\`

This will create a Product Requirements Document (PRD) that translates business strategy into product features.
```

## Quality Checklist

Before completing, verify:
- [ ] Lean Canvas has ALL 9 boxes filled with specific details (no vague placeholders)
- [ ] System Context clearly defines what you ARE and ARE NOT
- [ ] Premortem includes 5 realistic failure scenarios with mitigation strategies
- [ ] Customer profile is specific enough to identify real people
- [ ] Revenue model has actual numbers (even if estimated)
- [ ] Key metrics are measurable and actionable
- [ ] Assumptions are testable and have validation timelines
- [ ] Competition analysis includes REAL alternatives (not "no competitors")

## Common Mistakes to Avoid

❌ **Vague value props**: "We make project management better"  
✅ **Specific value props**: "15-person construction crews update job status in 30 seconds via voice commands instead of 10-minute end-of-day reports"

❌ **"Everyone" as target**: "Small and enterprise businesses"  
✅ **Specific target**: "General contractors with 10-100 employees managing 5-30 active projects"

❌ **No real unfair advantage**: "Our team is passionate"  
✅ **Real unfair advantage**: "Our CTO spent 10 years building scheduling systems at the largest construction software company"

❌ **Ignoring competition**: "No direct competitors"  
✅ **Honest competition**: "Competing with Buildertrend (too expensive), Procore (too complex), and Excel + texting (free but chaotic)"

## Success Criteria

This phase succeeds when:
- [ ] A non-technical person could understand the business from the Lean Canvas
- [ ] The System Context could guide an engineer's technical decisions
- [ ] Premortem scenarios feel realistic (not generic)
- [ ] You could go recruit your first 10 customers based on this strategy
- [ ] Critical assumptions have clear validation plans

## Remember

**This is your Business Plan.**

In the AI-native world, a business plan isn't a 50-page PDF that nobody reads. It's a living document that:
- Guides product decisions (next step: PRD)
- Becomes system context for AI agents
- Gets refined as you validate assumptions
- Prevents scope creep by defining boundaries

Proceed to `/speckit.productize` when ready to define WHAT you'll build.
