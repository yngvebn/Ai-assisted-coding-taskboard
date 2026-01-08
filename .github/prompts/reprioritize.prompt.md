---
description: "Re-prioritize bugs and features in the issue-tracking system"
agent: issue-tracking-expert
---

# Re-prioritize Issue Tracking

Analyze and re-prioritize the bugs and features in the `issue-tracking/` folder based on impact, urgency, dependencies, and user value.

Clean up PLANNING-BOARD, keeping it short and concise, and remove any reference to completed material

## Prerequisites

**CRITICAL**: Read these files first to understand the workflow:
- `issue-tracking/AGENTS.md` - Complete workflow rules and PowerShell scripts reference
- `.github/agents/issue-workflow.agent.md` - Agent-specific instructions for issue management
- `.github/copilot-instructions.md` - Repository-wide guardrails and patterns

## Tools Available

Use these PowerShell scripts to analyze and manage issues:

```powershell
# View all issues with statistics and filtering
.\scripts\backlog-view.ps1 -ShowStats
.\scripts\backlog-view.ps1 -FilterPriority high
.\scripts\backlog-view.ps1 -FilterType bug
.\scripts\backlog-view.ps1 -SortBy effort

# Create new issue (if reprioritization reveals gaps)
.\scripts\issue-create.ps1 -Type feature -Title "Issue name" -Priority high -Effort 2h -Labels "label1,label2" -NonInteractive

# Start working on prioritized issue
.\scripts\issue-start.ps1 ISSUE-ID

# Mark issue complete
.\scripts\issue-complete.ps1 ISSUE-ID
```

**Scripts provide structured output** for easy parsing by AI agents.

## Tasks

### 1. Analyze Current State

Use the backlog-view script to get comprehensive statistics:

```powershell
.\scripts\backlog-view.ps1 -ShowStats
```

Read the following files to understand current priorities:
- `issue-tracking/PLANNING-BOARD.md` - Current top 3-5 priorities
- `issue-tracking/backlog/` - All pending issues (use script to list)
- `issue-tracking/in-progress/` - Currently active work
- `issue-tracking/done/` - Recently completed work (for context)

### 2. Review All Issues

**Use the backlog-view script to filter and analyze:**

```powershell
# View high priority items
.\scripts\backlog-view.ps1 -FilterPriority high

# View all bugs
.\scripts\backlog-view.ps1 -FilterType bug

# Sort by effort (quickest wins first)
.\scripts\backlog-view.ps1 -SortBy effort
```

For each issue, the frontmatter contains:
- **id**: Issue identifier (auto-generated from filename)
- **type**: bug | feature | refactor | explore
- **priority**: high | medium | low
- **effort**: Time estimate (2h, 4h, 1d, 3d, 1w)
- **status**: backlog | in-progress | done | wont-fix
- **labels**: Array of tags for filtering/grouping
- **depends_on**: Array of issue IDs that must complete first
- **blocks**: Array of issue IDs waiting on this issue
- **created/updated/started/completed**: Timestamps

Analyze each issue for:
- **User impact**: Who is affected and how severely
- **Technical complexity**: Implementation effort (AI agents can work faster)
- **Business value**: ROI and strategic alignment
- **Dependencies**: What blocks this or what it blocks
- **Quick wins**: High impact + low effort

### 3. Prioritization Criteria

Rank issues based on these principles:

**Critical (Do First - Blocking Issues)**:
- Bugs blocking core functionality for users
- Security vulnerabilities
- Data loss or corruption risks
- Authentication/authorization issues
- Issues causing user churn or support tickets
- Features required by dependencies

**High Priority (Do Soon - High Impact)**:
- Bugs affecting user experience but not blocking
- Features that provide significant user value
- Technical debt causing significant friction
- Dependencies for planned work
- Error handling and resilience improvements

**Medium Priority (Evaluate - Moderate Impact)**:
- Quality of life improvements
- Features requested by users (validate impact)
- Refactoring for maintainability
- Non-critical enhancements

**Low Priority (Defer - Nice to Have)**:
- Future enhancements
- Minor bugs with workarounds
- Experimental features
- Low-impact polish or optimization

### 4. Update PLANNING-BOARD.md

Update the Planning Board with the top 3-5 priorities:

**Rules** (from AGENTS.md):
- Keep it short: Maximum 3-5 items
- Priority order: Most important at top
- Actionable: Clear and specific
- Update timestamp
- Link to issue files

**Format**:
```markdown
### 1. [Issue Title] (STATUS)
**Issue**: `backlog/[FILENAME].md`
**Status**: [Ready to Start/Blocked/Investigating]
**Notes**: [One-line explanation of priority/dependencies]
```

### 5. Update Issue Priorities

For each issue file that changed priority, update the **frontmatter**:

```yaml
---
id: FEATURE-example
type: feature
priority: high  # ← Update this (was: medium)
effort: 1d
status: backlog
labels: [critical, mvp]
depends_on: []
blocks: []
created: 2025-11-24
updated: 2025-11-24  # ← Update this to current date
started: null
completed: null
---
```

Also add a note in the file body explaining the priority change.

Ensure labels are accurate and reflect current categorization.

### 6. Provide Summary

Generate a summary showing:
- **What changed**: Which issues moved up/down in priority
- **Rationale**: Why priorities were adjusted
- **Next steps**: Recommended action for top priority
- **Blocked items**: Issues waiting on dependencies
- **Statistics**: Updated counts by priority level

## Input Variables

Optional context from user:
- **Focus area**: ${input:focus:any specific area to prioritize (e.g., bugs, specific feature)}
- **Timeline**: ${input:timeline:any timeline constraints (e.g., "need to launch in 2 weeks")}
- **User feedback**: ${input:feedback:recent user complaints or requests}

## Guidelines

Follow all rules from [issue-tracking/AGENTS.md](../../issue-tracking/AGENTS.md):
- Don't exceed 3-5 items on Planning Board
- Remove completed items (don't accumulate history)
- Update timestamp on Planning Board
- Cross-reference related issues
- Document rationale for priority changes
- Consider dependencies between issues

## Output Format

Provide structured output with clear sections:

### 1. Analysis Summary
**Use script output** for accurate statistics:
```powershell
.\scripts\backlog-view.ps1 -ShowStats
```

Report:
- Total backlog count by type (bugs, features, refactors)
- Current PLANNING-BOARD item count

**Backlog Statistics** (from `.\scripts\backlog-view.ps1 -ShowStats`):
- Total backlog: 52 items
- Total effort: 2143 hours (~267.9 days)
- By type: 30 features, 19 refactors, 2 bugs, 1 exploration
- By priority: 8 high, 29 medium, 15 low
- Current PLANNING-BOARD: 0 items (needs update)
- Blocked items: 3 (waiting on dependencies)

## Recommended Top 5 Priorities

1. **BUG-login-page-dark-mode-poor-contrast** (HIGH → HIGH)
   - Rationale: Accessibility blocker, affects all dark mode users
   - Effort: 2h (quick win)
   - Impact: Critical accessibility compliance (WCAG AA)
   - Dependencies: None
   - **Quick Win**: ✅ High impact + low effort

2. **REFACTOR-sessions-controller-service-extraction** (HIGH → HIGH)
   - Rationale: Blocks testability, 3,038 lines violates SRP
   - Effort: 14h
   - Impact: Enables unit testing, unblocks other work
   - Dependencies: None
   - Blocks: Future feature work requiring session services

3. **FEATURE-basic-topic-friction** (MEDIUM → HIGH)
   - Rationale: Low-tech high-value insights, quick to implement
   - Effort: 12h
   - Impact: Immediate value for users, no AI required
   - Dependencies: None
   - Labels: do-early, low-tech-high-value

4. **FEATURE-integrations-linear-export-tests** (HIGH → HIGH)
   - Rationale: Integration already exists, needs test coverage
   - Effort: 1d
   - Impact: Prevents regressions, production readiness
   - Dependencies: None

5. **PERFORMANCE-OPTIMIZATION-COMPLETE-ANALYSIS** (HIGH → MEDIUM)
   - Rationale: Important but defer until after launch (3w effort)
   - Effort: 3w
   - Impact: 50-80% DB load reduction (but not blocking)
   - Dependencies: None
   - Note: Defer to post-launch optimization phase

## Updated PLANNING-BOARD.md

```markdown
# Current Priorities (Updated: 2025-11-24)

**Rules**: Max 3-5 items, priority order, remove when done

### 1. Fix Dark Mode Login Contrast (READY)
**Issue**: `backlog/BUG-login-page-dark-mode-poor-contrast.md`
**Priority**: HIGH | **Effort**: 2h | **Type**: Bug
**Status**: Ready to Start
**Notes**: Quick accessibility fix, WCAG AA compliance blocker

### 2. Extract Session Services from Controller (READY)
**Issue**: `backlog/REFACTOR-sessions-controller-service-extraction.md`
**Priority**: HIGH | **Effort**: 14h | **Type**: Refactor
**Status**: Ready to Start
**Notes**: Enables testability, unblocks future features (3,038 LOC → services)

### 3. Basic Topic/Friction Tracking (READY)
**Issue**: `backlog/FEATURE-basic-topic-friction.md`
**Priority**: HIGH | **Effort**: 12h | **Type**: Feature
**Status**: Ready to Start
**Notes**: Low-tech high-value insights, no AI dependencies

### 4. Linear Integration Test Coverage (READY)
**Issue**: `backlog/FEATURE-integrations-linear-export-tests.md`
**Priority**: HIGH | **Effort**: 1d | **Type**: Feature
**Status**: Ready to Start
**Notes**: Production readiness, prevent regressions
```

## Priority Changes Made

**Promoted to HIGH**:
- `FEATURE-basic-topic-friction`: medium → high (low-tech high-value, quick to deliver)

**DemoUsed `.\scripts\backlog-view.ps1 -ShowStats` for accurate statistics
- [ ] PLANNING-BOARD.md has 3-5 items maximum
- [ ] Items are in priority order (highest impact first)
- [ ] All linked issue files exist in `issue-tracking/backlog/`
- [ ] Timestamp is updated on PLANNING-BOARD.md
- [ ] Dependencies are documented (checked `depends_on` frontmatter)
- [ ] Rationale is clear for each priority
- [ ] Updated `priority` and `updated` fields in frontmatter for changed issues
- [ ] Quick wins (high impact + low effort) are identified
- [ ] Blocked items are listed with their dependencies

## User Input Variables

Respect user context when provided:
- **${input:userText}**: General prioritization guidance
- **${input:focus}**: Specific area to prioritize (e.g., "bugs only", "performance")
- **${input:timeline}**: Timeline constraints (e.g., "launch in 2 weeks")
- **${input:feedback}**: Recent user complaints or feature requeststraction`: Remains HIGH
- `FEATURE-integrations-linear-export-tests`: Remains HIGH

## Blocked Items

**3 issues waiting on dependencies**:

1. `FEATURE-cross-session-similarity-panels` (medium, 3d)
   - Depends on: `FEATURE-semantic-recurrence-detection`
   - Impact: AI-powered cross-session insights

2. `FEATURE-insights-phase6-ux-polish` (low, 3d)
   - Depends on: `FEATURE-insights-phase4-ai-enhancement`
   - Impact: UX polish for AI features

3. `FEATURE-dynamic-template-info-pages` (medium, 2w)
   - Depends on: `FEATURE-ai-template-recommendation-engine`
   - Impact: Personalized template guidance

## Next Action

**Start with**: `BUG-login-page-dark-mode-poor-contrast`

```powershell
.\scripts\issue-start.ps1 BUG-login-page-dark-mode-poor-contrast
```

**Why this first**:
- ✅ Quick win (2h effort)
- ✅ High user impact (accessibility blocker)
- ✅ No dependencies
- ✅ Production blocker (WCAG AA compliance)
- ✅ Builds momentum with fast completion

**Expected outcome**: Accessible login page for dark mode users, WCAG AA compliant
## Analysis Summary
- Total backlog: 14 items (9 bugs, 4 features, 1 refactor)
- Current PLANNING-BOARD: 1 item
- Blocked items: 1 (FEATURE-discussion-summary-sidebar)

## Recommended Top 5 Priorities

1. **BUG-lean-coffee-topics-not-appearing-in-voting** (HIGH)
   - Rationale: Blocks core voting workflow, affects all users
   - Effort: 1-2 hours
   - Impact: Critical functionality

2. **BUG-allocate-votes-button-disabled** (HIGH)
   - Rationale: Prevents voting from starting, high user impact
   - Effort: 2-3 hours
   - Impact: Blocks feature usage

3. **FEATURE-session-summary-ai** (MEDIUM)
   - Rationale: High user value, premium feature revenue
   - Effort: 3 days
   - Dependency: None

4. **BUG-discussion-title-disappears** (MEDIUM)
   - Rationale: User confusion, but workarounds exist
   - Effort: 1 hour
   - Impact: UX degradation

5. **REFACTOR-simplify-pricing-tier-upgrade-flow** (LOW)
   - Rationale: Technical debt, but not blocking users
   - Effort: 1 day
   - Impact: Developer experience

## Priority Changes Made
- BUG-lean-coffee-topics-not-appearing-in-voting: Medium → High
- BUG-allocate-votes-button-disabled: Low → High
- FEATURE-session-summary-ai: Low → Medium

## Next Action
Start with BUG-lean-coffee-topics-not-appearing-in-voting (estimated 1-2 hours)
```

## Validation

Before finalizing:
- [ ] PLANNING-BOARD.md has 3-5 items maximum
- [ ] Items are in priority order
- [ ] All linked issue files exist
- [ ] Timestamp is updated
- [ ] Dependencies are documented
- [ ] Rationale is clear for each priority
