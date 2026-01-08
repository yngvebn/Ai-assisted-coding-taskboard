---
description: Get current status of planning board, ongoing work, and proposed next actions
agent: issue-tracking-expert
---

# Current Project Status

Get a comprehensive overview of the issue tracking system, including planning board state, in-progress work, and recommended next actions.

## Your Task

Generate a status report by gathering and presenting the following information:

### 1. Planning Board Status

Read [PLANNING-BOARD.md](../../issue-tracking/PLANNING-BOARD.md) and report:
- Last updated date
- Items currently in progress
- Top priorities queue
- Recently completed items

### 2. In-Progress Work

Check the `issue-tracking/in-progress/` folder:
- List all issues currently being worked on
- For each issue, summarize:
  - Issue ID and title
  - Priority and effort estimate
  - Current status/progress (from Progress Log)
  - Any blockers or dependencies
  - Next immediate steps

### 3. Recent Completions Check

Run the done view script to verify recent completions:

```powershell
.\scripts\done-view.ps1 -LastNDays 7 -ShowStats
```

Report:
- Number of issues completed in last 7 days
- Total effort completed
- Breakdown by type
- Average completion time

### 4. Backlog Statistics

Run the backlog view script for statistics:

```powershell
.\scripts\backlog-view.ps1 -ShowStats
```

Report:
- Total issue count
- Total effort hours
- Breakdown by type (bug, feature, refactor, etc.)
- Breakdown by priority (high, medium, low)

### 4. High Priority Items Ready to Start

Run to find ready high-priority items:

```powershell
.\scripts\backlog-view.ps1 -FilterPriority high
```

List any high-priority items that:
- Are in backlog (not started)
- Have no blocking dependencies
- Are ready for immediate work

### 5. Proposed Next Actions

Based on the gathered information, recommend:

1. **Immediate action**: What should be worked on next?
2. **Blocked items**: Any items waiting on dependencies?
3. **Planning board updates**: Does PLANNING-BOARD.md need updating?
4. **Quick wins**: Any small items (≤2h) that could be completed quickly?

## Output Format

Present the status in this format:

```markdown
# 📊 Project Status Report
**Generated**: [Current date and time]

## 🔄 In Progress
[List active work with status]

## 📋 Planning Board Summary
**Last Updated**: [Date from PLANNING-BOARD.md]
**Queue Size**: [Number of items]

### Current Priorities:
1. [Priority 1]
2. [Priority 2]
...

## 📈 Backlog Statistics
- **Total Issues**: X
- **Total Effort**: Y hours (~Z days)
- **High Priority**: X | **Medium**: Y | **Low**: Z
- **Types**: bugs (X), features (Y), refactors (Z), ...

## ⚡ Ready for Immediate Work
[High priority items with no blockers]

## 🎯 Recommended Next Actions
1. **Start**: [Recommended item to start]
2. **Quick Win**: [Small item that could be done quickly]
3. **Needs Attention**: [Any planning board or documentation updates needed]

## 🚧 Blocked Items
[Items waiting on dependencies]

## ✅ Recently Completed
[Last 3-5 completed items with dates]
```

## Success Criteria

- [ ] PLANNING-BOARD.md status accurately reported
- [ ] All in-progress items identified and summarized
- [ ] Backlog statistics gathered
- [ ] High-priority ready items identified
- [ ] Clear next action recommendations provided
- [ ] Any blockers or issues flagged

## Related Resources

- [PLANNING-BOARD.md](../../issue-tracking/PLANNING-BOARD.md) - Current priorities
- [issue-tracking/in-progress/](../../issue-tracking/in-progress/) - Active work
- [issue-tracking/backlog/](../../issue-tracking/backlog/) - Pending items
- [issue-tracking/done/](../../issue-tracking/done/) - Completed work
- [backlog-view.ps1](../../scripts/backlog-view.ps1) - Backlog statistics script

## Quick Commands Reference

```powershell
# Full statistics
.\scripts\backlog-view.ps1 -ShowStats

# High priority items only
.\scripts\backlog-view.ps1 -FilterPriority high

# Quick wins (sorted by effort)
.\scripts\backlog-view.ps1 -SortBy effort

# Bugs only
.\scripts\backlog-view.ps1 -FilterType bug
```
