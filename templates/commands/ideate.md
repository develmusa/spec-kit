---
description: Run synthetic validation with AI-generated personas and focus groups to validate business ideas before building.
handoffs: 
  - label: Create Business Strategy
    agent: speckit.strategize
    prompt: Create business strategy and Lean Canvas
    send: true
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Overview

The `/speckit.ideate` command initiates the **Context-First Framework** - an AI-native approach to validating business ideas through synthetic user research before writing any code.

This is **Phase 0** of the Spec-Driven Development process, designed for entrepreneurs and product teams who want to:
- Validate a business idea before investing in development
- Discover critical objections through simulated user feedback
- Identify must-have vs. nice-to-have features
- Challenge assumptions through AI-powered personas

## Workflow

### Step 1: Initialize Business Planning Structure

Create the business planning directory structure if it doesn't exist:

```bash
mkdir -p .specify/business
```

### Step 2: Capture the Raw Idea

The user input `$ARGUMENTS` contains their business idea description. If empty, prompt them:

```text
Please describe your business idea. Include:
- What problem are you solving?
- Who has this problem?
- How does your solution work?
- Why is this better than existing solutions?
```

Save this to `.specify/business/01_ideation.md` using the template at `templates/business/ideation-template.md`.

### Step 3: Generate Synthetic User Personas

Create **5 distinct user personas** that represent potential customers or users affected by the problem space. For each persona:

**Diversity Requirements:**
- Vary demographics (age, income, job role)
- Include both power users and novices
- Mix early adopters with skeptics
- Represent different use cases or contexts
- Include at least one persona who might NOT need this solution

**Persona Profile Template:**
```markdown
### Persona [N]: [Name] - [Role/Type]

- **Age**: [Age range]
- **Job Title**: [Specific role]
- **Salary Range**: [Range appropriate to role]
- **Primary Pain Point**: [Specific frustration with current solutions - be detailed]
- **Goals**: [What they're trying to achieve]
- **Tech Savviness**: [Low/Medium/High + explanation]
- **Quote**: "[A characteristic statement this persona would say about the problem]"
```

**Example Personas for a Project Management Tool:**
- Sarah Chen, 34 - Startup CTO (High tech, wants speed)
- Michael Rodriguez, 51 - Enterprise PMO Director (Low tech, wants compliance)
- Aisha Okoye, 28 - Freelance Designer (Medium tech, wants simplicity)
- David Kim, 42 - Construction Foreman (Low tech, needs mobile-first)
- Emma Watson, 25 - College Student (High tech, tight budget, might use free alternatives)

### Step 4: Run Synthetic Focus Group

**Instructions for AI:**
You will now conduct a multi-round focus group where you embody each persona and critique the business idea from their unique perspective. This is NOT about being positive - it's about discovering fatal flaws BEFORE building.

#### Round 1: Initial Pitch

1. Craft a concise elevator pitch (2-3 sentences) based on the raw idea
2. For each persona, generate a response that:
   - Reflects their specific pain points and context
   - Identifies aspects that appeal OR concern them
   - Raises questions from their perspective
   - May include skepticism or objections

**Record the pitch and all 5 persona responses in the transcript section.**

#### Round 2: Addressing Objections

1. Synthesize the top 3-4 objections raised
2. Draft a response addressing these concerns
3. Have each persona react to your response:
   - Some may be convinced
   - Some may raise deeper concerns
   - Some may reveal deal-breakers

**Record your response and all persona reactions.**

#### Round 3: Feature Prioritization

Ask each persona: **"If you could only have ONE feature from this product on day 1, what would it be?"**

This reveals:
- What's actually valuable vs. what you THINK is valuable
- Whether different personas need fundamentally different features (market segmentation signal)
- Minimum viable feature set

**Record all responses.**

### Step 5: Extract Key Insights

Analyze the focus group transcript and populate these sections:

#### Critical Objections Discovered
Identify **3-5 objections** you hadn't considered. For each:
- **Category**: (e.g., "Market Timing", "Competition", "User Behavior", "Unit Economics")
- **Description**: What the objection is
- **Raised by**: Which personas raised it
- **Impact**: High/Medium/Low
- **Solution approach**: How you might address it (or if it's a pivot signal)

#### Must-Have Features (Validated)
List features that **3+ personas** independently identified as critical.

#### Nice-to-Have Features
List features mentioned by 1-2 personas.

#### Features to Drop
List features from your original idea that **zero personas** requested or actively opposed.

#### Assumptions to Validate
Identify **2-4 assumptions** you made that personas challenged:
```markdown
1. **Assumption**: [What you assumed]
   - **Reality**: [What personas revealed]
   - **Action**: [What you'll do differently]
```

### Step 6: Validation Report

Present a summary to the user:

```markdown
## Ideation Validation Summary

### ✅ Strong Signals (Proceed to Strategy)
- [Signal 1]
- [Signal 2]

### ⚠️ Warning Signs (Address Before Proceeding)
- [Warning 1]
- [Warning 2]

### 🚫 Pivot Signals (Consider Fundamental Changes)
- [If any deal-breakers emerged]

### Recommended Next Steps
- [Specific actions based on findings]
```

### Step 7: Save and Transition

1. Save the complete ideation document to `.specify/business/01_ideation.md`
2. Inform the user:

```markdown
## Ideation Phase Complete

📄 **Artifact created**: `.specify/business/01_ideation.md`

### What You Learned
- [Top 3 insights]

### Ready for Next Phase?

If the validation signals are positive, run:

\`\`\`
/speckit.strategize
\`\`\`

This will create your Lean Canvas and business strategy based on these validated insights.

**Note**: This is an AI simulation. Consider conducting real user interviews to validate these synthetic findings before major investment.
```

## Guidelines for Synthetic Personas

### Make Them Realistic
- Give them specific names and detailed backgrounds
- Base their concerns on real-world constraints (budget, time, existing tools)
- Include personal quirks and communication styles
- Reference specific alternatives they currently use

### Make Them Brutally Honest
- Personas should NOT be cheerleaders
- They should poke holes in weak assumptions
- They should mention competitors you forgot about
- They should reveal inconvenient truths (e.g., "I'd just use the free version of X")

### Make Them Diverse in Perspective
- **The Pragmatist**: Wants proven solutions, risk-averse
- **The Innovator**: Willing to try new things, values cutting-edge
- **The Budget-Conscious**: Price-sensitive, seeks alternatives
- **The Power User**: Has complex needs, current solutions frustrate them
- **The Skeptic**: Questions whether the problem is worth solving

## Anti-Patterns to Avoid

❌ **Don't** make all personas love the idea  
✅ **Do** have at least 2 personas raise significant concerns

❌ **Don't** make personas generic ("users", "customers")  
✅ **Do** create specific, named individuals with detailed contexts

❌ **Don't** ignore objections that emerged  
✅ **Do** document every concern, even uncomfortable ones

❌ **Don't** skip to building after validation  
✅ **Do** proceed to `/speckit.strategize` to formalize business logic

## Success Criteria

This phase is successful when:
- [ ] 5 distinct, realistic personas created
- [ ] 3 rounds of focus group completed
- [ ] At least 3 critical objections discovered
- [ ] Feature prioritization reveals must-haves
- [ ] Assumptions challenged and documented
- [ ] Clear recommendation on whether to proceed, pivot, or stop

## Remember

**The goal is NOT to validate your idea.**  
**The goal is to STRESS-TEST your idea and discover fatal flaws before investing months of development.**

The best outcome might be discovering you need to pivot - that's a win, not a failure.
