---
description: Create a Product Requirements Document (PRD) that translates business strategy into specific product features and flows.
handoffs: 
  - label: Generate Agent Rules
    agent: speckit.constitution
    prompt: Create technical constitution and agent rules from business context
    send: true
  - label: Back to Strategy
    agent: speckit.strategize
    prompt: Revisit and refine business strategy
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding (if not empty).

## Overview

The `/speckit.productize` command creates a **Product Requirements Document (PRD)** - the bridge between business strategy and technical implementation. This is where "business English" becomes "engineering English" without getting into code.

This is **Phase 2** of the Context-First Framework, translating validated strategy into a buildable product blueprint.

## Prerequisites

Before running this command:
- [ ] `/speckit.strategize` has been completed
- [ ] Strategy document exists at `.specify/business/02_strategy.md`
- [ ] Lean Canvas and System Context are well-defined

If strategy hasn't been created, prompt the user to complete it first.

## Workflow

### Step 1: Load Business Strategy

Read `.specify/business/02_strategy.md` and extract:
- **Value Proposition**: What makes this product unique?
- **Target Customers**: Who are we building for? (persona archetypes)
- **Must-Have Features**: Solution section from Lean Canvas
- **Key Metrics**: How we measure product success
- **What We Are NOT**: Explicit scope boundaries

### Step 2: Define Product Vision

Create a one-paragraph executive summary that synthesizes:
- Core value proposition
- Target user
- Primary use case
- Differentiation

**Template:**
> [Product Name] helps [specific user type] [achieve goal] by [unique approach]. Unlike [existing alternatives], we [key differentiator]. Users will measure success by [user-centric outcome].

**Example:**
> TaskFlow helps construction foremen manage field crews by enabling voice-based task updates and real-time status tracking from mobile devices. Unlike enterprise project management tools built for office workers, we use a mobile-first, tap-and-speak interface optimized for outdoor job sites. Users will measure success by reducing end-of-day reporting time from 30 minutes to under 2 minutes.

### Step 3: Refine User Personas for Product Context

Convert business personas into product personas by adding:
- **Primary workflows**: What tasks do they do daily?
- **Tool context**: What tools do they currently use for this?
- **Environment**: Where/when do they use the product?
- **Success definition**: What does "solved" look like for them?

```markdown
### Primary Persona: [Name] - [Role]

- **Job/Role**: [Specific title and responsibilities]
- **Goals**: [What they're trying to accomplish with THIS product]
- **Pain Points**: [Specific frustrations our features address]
- **Tech Comfort**: [Low/Medium/High + details]
- **Current Tools**: [Exact tools they use today for this problem]
- **Usage Context**: [When, where, and how they'll use our product]
```

### Step 4: Define Feature Set with Priority Tiers

Organize features into **P1 (Must-Have)**, **P2 (Should-Have)**, **P3 (Nice-to-Have)** based on:
- Lean Canvas "Solution" section (these are P1)
- Persona must-haves from ideation (P1 if 3+ personas demanded it)
- Strategic differentiators (P1 or P2 depending on impact)
- Enhancement features (P2 or P3)

For **each feature**, document:

```markdown
#### Feature [N]: [Feature Name]

**Priority**: P1/P2/P3

**User Story**: As a [persona], I want to [action] so that [benefit]

**Business Value**: [How this maps to Lean Canvas value prop / key metrics]

**User Flows**:
1. [User action/step]
2. [System response]
3. [User action/step]
4. [Outcome]

**Acceptance Criteria**:
- [ ] [Specific, testable criterion]
- [ ] [Specific, testable criterion]
- [ ] [Specific, testable criterion]

**Edge Cases**:
- What if [scenario]? → [Expected behavior]
- What if [scenario]? → [Expected behavior]
```

**Important Rules:**
- **P1 features**: Minimum to deliver core value proposition. If you removed any P1 feature, the product wouldn't solve the core problem.
- **P2 features**: Enhance the experience or address secondary pain points. Product works without them but is noticeably better with them.
- **P3 features**: Delight factors, differentiators, or features for edge cases.

**Example P1 Feature:**
```markdown
#### Feature 1: Voice Task Updates

**Priority**: P1

**User Story**: As a construction foreman, I want to update task status using voice commands so that I can keep project status current without stopping work.

**Business Value**: Core differentiator from competitors. Addresses #1 pain point (updating PM tools takes too long). Maps to key metric "reduce reporting time by 90%".

**User Flows**:
1. Foreman taps microphone icon on task card
2. System prompts "Status update?"
3. Foreman says "Mark as complete"
4. System updates task status and notifies team
5. Foreman sees visual confirmation and continues work

**Acceptance Criteria**:
- [ ] Voice recognition works in noisy environments (construction sites)
- [ ] Status update completes in under 5 seconds
- [ ] Works offline and syncs when connection restored
- [ ] Confirmation is visual (not just audio) for outdoor use

**Edge Cases**:
- What if no internet? → Queue update locally, sync when online, show "pending sync" indicator
- What if voice unclear? → Show options "Did you mean: Complete / In Progress / Blocked?" with tap to confirm
- What if hands full and can't tap? → "Hey TaskFlow, mark [task name] as complete" wake phrase
```

### Step 5: Define Data Model (Technology-Agnostic)

Identify **key entities** (nouns) from the feature set. For each:

```markdown
### Entity [N]: [Entity Name]

**Purpose**: [What this represents in business terms]

**Key Attributes**:
- **[Attribute]**: [Description, business data type (text, number, date, yes/no)]
- **[Attribute]**: [Description, constraints/rules]
- **[Attribute]**: [Description]

**Relationships**:
- **[Relationship type]** to [Other Entity]: [Description]

**Business Rules**:
- [Constraint or validation rule]
- [Constraint or validation rule]
```

**Example:**
```markdown
### Entity 1: Task

**Purpose**: Represents a unit of work that needs to be completed on a project

**Key Attributes**:
- **Title**: Short description (text, max 100 characters, required)
- **Status**: Current state (one of: To Do, In Progress, Blocked, Complete)
- **Assigned To**: Person responsible (must be valid team member)
- **Due Date**: When it should be completed (date, optional)
- **Notes**: Additional context (text, unlimited, optional)
- **Created Date**: When task was created (date/time, auto-set)
- **Last Updated**: When task was last modified (date/time, auto-updated)

**Relationships**:
- **Belongs to** one Project
- **Assigned to** zero or one User
- **Has** zero or many Comments

**Business Rules**:
- Cannot delete a task marked "Complete" (can archive instead)
- Status can only move forward (To Do → In Progress → Complete), not backward
- Only assigned user or project owner can change status
- Due date cannot be in the past when created
```

### Step 6: Define API Endpoints (Conceptual)

For each major action/interaction, describe the API contract in business terms:

```markdown
### Endpoint [N]: [Action/Resource]

**Purpose**: [What this does in user/business terms]

**Input Required**:
- **[Field]**: [Description, validation rules, required/optional]
- **[Field]**: [Description, validation rules]

**Output Provided**:
- **[Field]**: [What gets returned]
- **[Field]**: [What gets returned]

**Business Rules**:
- [Rule or constraint enforced by this endpoint]
- [Rule or constraint]

**Error Scenarios**:
- **[Error condition]**: [User-facing error message/behavior]
- **[Error condition]**: [User-facing error message/behavior]
```

**Example:**
```markdown
### Endpoint 1: Update Task Status

**Purpose**: Change the status of an existing task (used by voice updates and manual taps)

**Input Required**:
- **Task ID**: Which task to update (required, must be valid task)
- **New Status**: Target status (required, must be valid status value)
- **User ID**: Who is making the change (required for authorization)
- **Voice Confidence**: If voice-triggered, confidence score (optional, 0-100)

**Output Provided**:
- **Updated Task**: Full task object with new status
- **Timestamp**: When update occurred
- **Notification Sent**: Confirmation that team was notified

**Business Rules**:
- User must be assigned to task OR be project owner
- Status must follow valid transitions (can't skip from To Do to Complete)
- If voice confidence < 70%, require tap confirmation before applying

**Error Scenarios**:
- **Unauthorized user**: "You don't have permission to update this task"
- **Invalid status transition**: "Tasks must move through In Progress before Complete"
- **Task not found**: "This task no longer exists or was deleted"
- **Offline mode**: Queue update and show "Will sync when online" message
```

### Step 7: Define UI Guidelines (NOT Mockups)

Describe screens/views in terms of user goals and elements, NOT visual design:

```markdown
### Screen [N]: [Screen Name/Purpose]

**User Goal**: [What user accomplishes on this screen]

**Key Elements**:
- **[Element]**: [Purpose and behavior - what happens when user interacts]
- **[Element]**: [Purpose and behavior]

**User Actions Available**:
- [Action] → [Result/next screen]
- [Action] → [Result/next screen]

**Navigation**:
- Enters from: [Previous screen/trigger]
- Exits to: [Next screen/exit point]

**Success State**: [What user sees when they've accomplished the goal]

**Empty State**: [What user sees when no data yet]

**Error State**: [What user sees when something fails]
```

**Example:**
```markdown
### Screen 1: Project Task Board

**User Goal**: See all tasks for a project organized by status, update task status quickly

**Key Elements**:
- **Status Columns**: Four vertical lanes (To Do, In Progress, Blocked, Complete)
- **Task Cards**: Visual cards showing task title, assignee, due date
- **Highlight "My Tasks"**: Tasks assigned to current user appear in blue (others in gray)
- **Voice Button**: Microphone icon in bottom-right corner (always accessible)
- **Offline Indicator**: Banner at top if no connection (shows pending sync count)

**User Actions Available**:
- Tap task card → Open task detail view
- Tap voice button → Voice command mode (can update any visible task)
- Long-press task card → Options menu (edit, delete, assign)
- Pull down → Refresh task list (sync with server)

**Navigation**:
- Enters from: Project list screen (tapped on project)
- Exits to: Project list (back button), Task detail (tap card)

**Success State**: All columns populated with tasks, user's tasks highlighted, any updates visible immediately

**Empty State**: "No tasks yet. Tap + to create your first task or use voice: 'Create a task for...'"

**Error State**: "Can't load tasks right now. Last synced [time]. Using offline mode."
```

### Step 8: Define Happy Path User Flows

Document 2-3 end-to-end journeys that show the product working:

```markdown
### Flow [N]: [Primary User Journey]

**Goal**: [What user accomplishes end-to-end]

**Steps**:
1. **[User action]** → System displays/does [Result]
2. **[User action]** → System [Response/behavior]
3. **[User action]** → System [Response]
4. **[Final action]** → User achieves [Goal], sees [Confirmation]

**Success Criteria**: [How we know the user succeeded and is satisfied]
```

**Example:**
```markdown
### Flow 1: Update Task Status via Voice (Core Value Prop Flow)

**Goal**: Foreman updates task status from job site without stopping work

**Steps**:
1. **Foreman taps floating voice button** → Microphone activates, shows listening animation
2. **Foreman says "Mark framing inspection as complete"** → System processes voice, highlights matching task card
3. **System asks "Mark 'Framing Inspection' as complete?"** → Visual confirmation dialog appears
4. **Foreman says "Yes" or taps checkmark** → Task moves to Complete column, team gets notification
5. **System shows "Done. Framing inspection marked complete"** → Foreman continues work

**Success Criteria**: 
- Entire flow takes under 10 seconds
- Works in noisy environment (construction site)
- Foreman never needs to type or navigate menus
- Team sees update in real-time
- Foreman gets clear confirmation and can trust it worked
```

### Step 9: Define Non-Functional Requirements

Document quality attributes:

```markdown
### Performance
- **[Metric]**: [Target with user-facing impact]

### Reliability
- **[Metric]**: [Target with user-facing impact]

### Security
- **[Requirement]**: [Description in user terms, not tech stack]

### Usability
- **[Requirement]**: [Measurable user experience target]

### Accessibility
- **[Requirement]**: [Support for diverse users]
```

**Examples:**
```markdown
### Performance
- **Voice command response time**: Under 3 seconds from speaking to visual confirmation
- **Page load time**: Under 2 seconds on 4G mobile connection
- **Offline capability**: All core features work without internet, sync when reconnected

### Security
- **Session timeout**: 1 hour of inactivity (field workers have long gaps between uses)
- **Data encryption**: All task updates encrypted before leaving device
- **Password requirements**: Minimum 8 characters, mix of types

### Usability
- **Onboarding time**: New user can create and update first task within 5 minutes
- **Error recovery**: All actions have undo option (accessible via shake gesture)
- **Help access**: Context-sensitive help available on every screen (? icon)
```

### Step 10: Document Explicit Scope Exclusions

Pull from strategy "What We Are NOT" and make product-specific:

```markdown
## Out of Scope (Explicit Exclusions)

- **NOT** [Feature/capability] - [Why not in MVP / when it might come later]
- **NOT** [Feature/capability] - [Reason]
```

**Example:**
```markdown
## Out of Scope (Explicit Exclusions)

- **NOT document storage/versioning** - Teams use existing tools (Google Drive, Dropbox). We link to docs, don't replace them.
- **NOT budget/cost tracking** - This is project STATUS tracking, not financial management. Integrate with QuickBooks instead.
- **NOT multi-company projects** - MVP is single-company workflow. Partner companies are future enhancement.
- **NOT desktop/web app** - Mobile-first only. Web view is read-only dashboard for office staff.
```

### Step 11: Identify Dependencies & Open Questions

```markdown
### External Dependencies

1. **[Dependency]**: [What you depend on]
   - **Impact if unavailable**: [Risk to product]
   - **Mitigation**: [Backup plan]

### Open Questions

1. **[Question]**: [Unresolved product decision]
   - **Impact**: [Why this matters]
   - **Decision owner**: [Who decides]
   - **Deadline**: [When answer is needed]
```

### Step 12: Generate Agent Rules File (The Golden Artifact)

This is **THE MOST IMPORTANT OUTPUT**. Create agent-specific rule files that compile the entire business/product context into instructions for code generation.

#### For Cursor (`.cursorrules`):

```markdown
You are an expert full-stack engineer building [Product Name].

## Project Context

[Pull from Strategy "System Context" + PRD "Product Vision"]

## Design Rules

[Based on personas and UI guidelines:]
- Use [design philosophy - e.g., mobile-first, voice-first, minimal-tap]
- All UI must support [key constraints - e.g., outdoor use, glove-friendly buttons]
- Follow [any design system - e.g., Material Design, iOS HIG]

## Business Rules

[Pull from Data Model "Business Rules" and API "Business Rules":]
- Users cannot [constraint]
- [Entity] must [validation rule]
- [Action] requires [authorization rule]

## Data Model

[Summarize entities and relationships - reference full PRD for details]

## Architecture Constraints

[Any non-negotiable technical requirements from strategy:]
- Must work offline first
- Must support [number] concurrent users
- Must comply with [regulation/standard]

## Reference Documents

- Full PRD: `.specify/business/03_product.md`
- Business Strategy: `.specify/business/02_strategy.md`
- Lean Canvas and target customers guide all decisions
```

#### For Claude (`CLAUDE.md` / `.claude/CLAUDE.md`):

Similar structure but tailored to Claude's format (more conversational, reference to Claude Code capabilities)

#### For other agents:

Generate equivalent rules files for the detected agent type.

**Save all agent rules files to appropriate locations:**
- `.cursorrules` (project root)
- `.claude/CLAUDE.md` or `CLAUDE.md`
- `.opencode/AGENTS.md`
- etc.

### Step 13: Save and Report

Save PRD to `.specify/business/03_product.md`

Present completion summary:

```markdown
## Product Requirements Complete

📄 **Artifacts created**:
- `.specify/business/03_product.md` (Full PRD)
- `.cursorrules` (Agent rules for Cursor)
- `CLAUDE.md` (Agent rules for Claude Code)
- [Other agent-specific files]

### Product Overview

**Vision**: [One sentence from PRD]
**MVP Features**: [P1 feature count]
**Target Users**: [Primary persona]

### Next Steps - Choose Your Path

#### Path A: Pure Technical Project
If you're ready to start building:

1. \`/speckit.constitution\` - Establish technical principles
2. \`/speckit.specify\` - Create technical specification  
3. \`/speckit.plan\` - Define technical implementation
4. \`/speckit.tasks\` - Generate task breakdown
5. \`/speckit.implement\` - Build the product

#### Path B: Validate Product First
If you want to validate the PRD with mockups/prototypes:

1. Use tools like **v0.dev** or **Figma** to create UI mockups
2. Share mockups with target users (optional real validation)
3. Refine PRD based on feedback
4. Then proceed to Path A when ready

### The "Rules File" Superpower

Your agent rules files (`.cursorrules`, etc.) now contain your entire business + product context. Every time the AI generates code, it checks these rules first. This ensures:

✅ Code aligns with business goals
✅ Features match user needs
✅ Business rules are enforced
✅ Architecture fits constraints

This is your **compiled business plan** → executable by AI.
```

## Quality Checklist

Before completing, verify:
- [ ] All P1 features have detailed user stories and acceptance criteria
- [ ] Data model covers all entities mentioned in features
- [ ] API endpoints support all user actions described
- [ ] UI screens map to complete user journeys
- [ ] Non-functional requirements are measurable
- [ ] Scope exclusions are explicit (prevent scope creep)
- [ ] Agent rules file accurately summarizes business + product context
- [ ] No technology decisions leaked in (still tech-agnostic)

## Success Criteria

This phase succeeds when:
- [ ] A developer could read the PRD and understand WHAT to build
- [ ] A designer could read UI guidelines and create mockups
- [ ] A product manager could validate features against user needs
- [ ] An AI agent could use the rules file to make aligned code decisions
- [ ] You could hand this to a dev team and they'd ask minimal clarifying questions

## Remember

**This is NOT a technical specification.**

You're still in "product mode" - describing WHAT users need and WHY, not HOW to build it technically.

The PRD bridges:
- **Ideation** (do users want this?)
- **Strategy** (can we build a business?)
- **Product** (what exactly should we build?) ← YOU ARE HERE
- **Technical** (how do we build it?) ← Next phase

When ready, use `/speckit.constitution` to transition into technical implementation.
