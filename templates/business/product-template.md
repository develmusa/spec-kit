# Product Requirements Document: [PRODUCT NAME]

**Created**: [DATE]  
**Status**: Draft  
**Phase**: Product (Blueprint for Development)  
**Based on Strategy**: [Link to strategy.md]

## Executive Summary

### Product Vision

[One paragraph describing what this product is and why it matters. Pull from the System Context in strategy.md]

### Success Metrics

- **[Metric 1]**: [Target value] by [Timeline]
- **[Metric 2]**: [Target value] by [Timeline]
- **[Metric 3]**: [Target value] by [Timeline]

## User Personas (from Ideation)

### Primary Persona: [Name]

- **Job/Role**: [Title]
- **Goals**: [What they want to achieve]
- **Pain Points**: [Specific frustrations]
- **Tech Comfort**: [Low/Medium/High]

### Secondary Persona: [Name]

- **Job/Role**: [Title]
- **Goals**: [What they want to achieve]
- **Pain Points**: [Specific frustrations]
- **Tech Comfort**: [Low/Medium/High]

## Feature Set (MVP)

<!-- Prioritized features that map to business strategy -->

### P1: Must-Have Features (Core Value Proposition)

#### Feature 1: [Feature Name]

**User Story**: As a [persona], I want to [action] so that [benefit]

**Business Value**: [Why this matters to the business - maps to Lean Canvas]

**User Flows**:
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Acceptance Criteria**:
- [ ] [Specific testable criterion]
- [ ] [Specific testable criterion]
- [ ] [Specific testable criterion]

**Edge Cases**:
- What if [scenario]? → [Expected behavior]
- What if [scenario]? → [Expected behavior]

---

#### Feature 2: [Feature Name]

**User Story**: As a [persona], I want to [action] so that [benefit]

**Business Value**: [Why this matters]

**User Flows**:
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Acceptance Criteria**:
- [ ] [Specific testable criterion]
- [ ] [Specific testable criterion]

**Edge Cases**:
- What if [scenario]? → [Expected behavior]

---

#### Feature 3: [Feature Name]

**User Story**: As a [persona], I want to [action] so that [benefit]

**Business Value**: [Why this matters]

**User Flows**:
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Acceptance Criteria**:
- [ ] [Specific testable criterion]
- [ ] [Specific testable criterion]

**Edge Cases**:
- What if [scenario]? → [Expected behavior]

---

### P2: Should-Have Features (Enhanced Experience)

#### Feature 4: [Feature Name]

**User Story**: As a [persona], I want to [action] so that [benefit]

**Business Value**: [Why this matters]

**User Flows**:
1. [Step 1]
2. [Step 2]

**Acceptance Criteria**:
- [ ] [Specific testable criterion]
- [ ] [Specific testable criterion]

---

### P3: Nice-to-Have Features (Delight Factors)

#### Feature 5: [Feature Name]

**User Story**: As a [persona], I want to [action] so that [benefit]

**Business Value**: [Why this matters]

**User Flows**:
1. [Step 1]
2. [Step 2]

**Acceptance Criteria**:
- [ ] [Specific testable criterion]

---

## Data Model (High-Level)

<!-- Technology-agnostic data entities -->

### Entity 1: [Entity Name]

**Purpose**: [What this represents]

**Key Attributes**:
- **[Attribute]**: [Description, type in business terms]
- **[Attribute]**: [Description, type in business terms]
- **[Attribute]**: [Description, type in business terms]

**Relationships**:
- **[Relationship]** to [Entity 2]: [Description]

**Business Rules**:
- [Rule about this entity]
- [Rule about this entity]

---

### Entity 2: [Entity Name]

**Purpose**: [What this represents]

**Key Attributes**:
- **[Attribute]**: [Description, type in business terms]
- **[Attribute]**: [Description, type in business terms]

**Relationships**:
- **[Relationship]** to [Entity 1]: [Description]

**Business Rules**:
- [Rule about this entity]

---

## API Endpoints (Technology-Agnostic)

<!-- Describe the contract, not the implementation -->

### Endpoint 1: [Action/Resource]

**Purpose**: [What this does in business terms]

**Input Required**:
- **[Field]**: [Description, validation rules]
- **[Field]**: [Description, validation rules]

**Output Provided**:
- **[Field]**: [Description]
- **[Field]**: [Description]

**Business Rules**:
- [Rule or constraint]
- [Rule or constraint]

**Error Scenarios**:
- **[Error condition]**: [Expected response to user]
- **[Error condition]**: [Expected response to user]

---

### Endpoint 2: [Action/Resource]

**Purpose**: [What this does in business terms]

**Input Required**:
- **[Field]**: [Description, validation rules]

**Output Provided**:
- **[Field]**: [Description]

**Business Rules**:
- [Rule or constraint]

**Error Scenarios**:
- **[Error condition]**: [Expected response to user]

---

## User Interface Guidelines

<!-- NOT mockups - descriptions of what users see and do -->

### Screen 1: [Screen Name/Purpose]

**User Goal**: [What users accomplish here]

**Key Elements**:
- **[Element]**: [Purpose and behavior]
- **[Element]**: [Purpose and behavior]
- **[Element]**: [Purpose and behavior]

**User Actions Available**:
- [Action] → [Result]
- [Action] → [Result]

**Navigation**:
- Enters from: [Previous screen/action]
- Exits to: [Next screen/action]

**Success State**: [What indicates the user succeeded]

**Empty State**: [What user sees when no data]

**Error State**: [What user sees when something fails]

---

### Screen 2: [Screen Name/Purpose]

**User Goal**: [What users accomplish here]

**Key Elements**:
- **[Element]**: [Purpose and behavior]
- **[Element]**: [Purpose and behavior]

**User Actions Available**:
- [Action] → [Result]

**Navigation**:
- Enters from: [Previous screen/action]
- Exits to: [Next screen/action]

---

## Happy Path User Flows

### Flow 1: [Primary User Journey]

**Goal**: [What the user accomplishes end-to-end]

**Steps**:
1. **[Action]** → System displays [Result]
2. **[Action]** → System [Behavior]
3. **[Action]** → System [Behavior]
4. **[Action]** → User achieves [Goal]

**Success Criteria**: [How we know user succeeded]

---

### Flow 2: [Secondary User Journey]

**Goal**: [What the user accomplishes]

**Steps**:
1. **[Action]** → System displays [Result]
2. **[Action]** → System [Behavior]
3. **[Action]** → User achieves [Goal]

**Success Criteria**: [How we know user succeeded]

---

## Non-Functional Requirements

<!-- Quality attributes, still technology-agnostic -->

### Performance

- **[Metric]**: [Target] (e.g., "Page load in under 2 seconds")
- **[Metric]**: [Target] (e.g., "Support 1000 concurrent users")
- **[Metric]**: [Target]

### Reliability

- **[Metric]**: [Target] (e.g., "99.9% uptime")
- **[Metric]**: [Target] (e.g., "Data backup every 24 hours")

### Security

- **[Requirement]**: [Description] (e.g., "User passwords must be encrypted")
- **[Requirement]**: [Description] (e.g., "Session timeout after 30 minutes of inactivity")
- **[Requirement]**: [Description]

### Usability

- **[Requirement]**: [Target] (e.g., "New user can complete signup in under 3 minutes")
- **[Requirement]**: [Target] (e.g., "All actions provide immediate feedback")

### Accessibility

- **[Requirement]**: [Description] (e.g., "Support keyboard navigation")
- **[Requirement]**: [Description] (e.g., "Color contrast meets WCAG AA standards")

## Out of Scope (Explicit Exclusions)

<!-- Prevent scope creep by documenting what we're NOT building -->

- **NOT** [Feature/capability] - [Reason why not now]
- **NOT** [Feature/capability] - [Reason why not now]
- **NOT** [Feature/capability] - [Reason why not now]

## Dependencies & Assumptions

### External Dependencies

1. **[Dependency]**: [Description]
   - **Impact if unavailable**: [Risk]
   - **Mitigation**: [Backup plan]

2. **[Dependency]**: [Description]
   - **Impact if unavailable**: [Risk]
   - **Mitigation**: [Backup plan]

### Assumptions

1. **[Assumption]**: [Description]
   - **Validation approach**: [How to verify]

2. **[Assumption]**: [Description]
   - **Validation approach**: [How to verify]

## Open Questions

<!-- Unresolved items that need answers before development -->

1. **[Question]**: [Description]
   - **Impact**: [Why this matters]
   - **Decision owner**: [Who decides]
   - **Deadline**: [When we need answer]

2. **[Question]**: [Description]
   - **Impact**: [Why this matters]
   - **Decision owner**: [Who decides]
   - **Deadline**: [When we need answer]

## Next Steps

- [ ] Review PRD with stakeholders
- [ ] Get mockups/wireframes created (optional - can use tools like v0.dev)
- [ ] Resolve open questions
- [ ] Ready to generate agent-specific rules file (`.cursorrules`, `CLAUDE.md`, etc.)
- [ ] Proceed to `/speckit.constitution` to establish technical principles
- [ ] Then use `/speckit.specify` to create technical specification
