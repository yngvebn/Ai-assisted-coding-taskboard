---
description: Clean and streamline the planning board to show only current priorities
agent: issue-tracking-expert
---

Clean the [PLANNING-BOARD.md](../../issue-tracking/PLANNING-BOARD.md) to maintain focus on active priorities.

## Objective

Keep the planning board lean and actionable:
- Show only **current 3-5 priorities** in ranked order
- Remove all completed work from the main priorities section
- Simplify header to essential context only
- Update timestamp
- **Check if done/ folder needs archival** (if >20-25 items, suggest running archive script)

## Cleaning Process

### 1. Review Current State

Read `issue-tracking/PLANNING-BOARD.md` and identify:
- Completed items in the priorities section (marked ✅ or "Complete")
- Outdated context or verbose descriptions
- Items that should be deferred to backlog
- Timestamp that needs updating

### 2. Clean Top Priorities Section

**Remove:**
- All completed items (already tracked in Recent Completions)
- Items marked "DONE", "Complete", or with ✅ status
- Long completion summaries (keep these in issue files, not board)
- Verbose historical context

**Keep:**
- 3-5 current priorities in ranked order (most important first)
- Brief rationale for each (1-2 sentences max)
- Status indicators (⏰ ready, 🔧 blocked, etc.)
- Effort estimates and impact assessment

### 3. Streamline Header

Rewrite header to include only:
- Last updated timestamp: `**Last Updated**: ${input:date:YYYY-MM-DD}`
- Current project phase (e.g., "🟡 DEVELOPMENT" or "🟢 PRODUCTION")
- 2-3 bullet points on current focus/strategy

Remove:
- Long instructions (keep detailed rules in AGENTS.md instead)
- Historical context
- Verbose philosophical statements

### 4. Verify Deferred Section

Ensure deferred items are:
- Clearly marked as not urgent
- Briefly explained (1 sentence max per category)
- Grouped by type (features, refactors, performance, etc.)

### 5. Check Archive Status

Before finalizing, check if the done/ folder needs maintenance:
```powershell
# Count items in done folder
Get-ChildItem -Path issue-tracking/done -Filter "*.md" -File | Measure-Object | Select-Object -ExpandProperty Count
```

**If count > 20-25 items**, suggest to user:
```
💡 The done/ folder has [N] items (target: ~20). Consider archiving old issues:
   .\scripts\archive-old-issues.ps1 -WhatIf    # Preview
   .\scripts\archive-old-issues.ps1            # Archive (90+ days old)
```

### 6. Final Checks

Confirm:
- Exactly 3-5 items in Top Priorities
- No completed items in priorities section
- Header is concise (≤ 10 lines)
- Timestamp updated to today
- Each priority has: title, brief context, effort, impact
- Recent Completions section exists but is separate from priorities
- Archive status checked (done/ folder size)

## Example Structure

```markdown
# Planning Board

**Last Updated**: 2025-01-11 - Focus on feature completion

**Context**: 🟡 DEVELOPMENT - Preparing for initial release
- Priority: Core features and stability
- Strategy: Complete critical features, then user testing

---

## Top Priorities

### 1. Core Feature Implementation (HIGH - Release Critical) ⏰
**Issue**: `backlog/FEATURE-implement-core-feature.md`
**Effort**: 2-3 days | **Impact**: Required before initial release
**Next Action**: Move to in-progress

### 2. [Next Priority]
...

---

## Recent Completions (2025-01-11) ✅
[Keep brief summaries of last 1-2 completions only]

---

## Deferred Priorities
[Grouped lists with 1-sentence rationale per group]
```

## Common Issues

❌ Leaving completed items in priorities
✅ Move to Recent Completions or remove entirely

❌ Verbose header with full instructions
✅ Keep header to ≤ 10 lines, move details to AGENTS.md

❌ More than 5 priorities listed
✅ Defer lower-priority items to backlog

❌ Missing timestamp update
✅ Always update "Last Updated" date

❌ Ignoring bloated done/ folder (>25 items)
✅ Run archive script to move old completions to archive/

## Related Scripts

- `.\scripts\archive-old-issues.ps1` - Archive old completed issues (90+ days)
- `.\scripts\done-view.ps1 -ShowStats` - View completion statistics
- `.\scripts\backlog-view.ps1 -FilterPriority high` - Review backlog priorities
