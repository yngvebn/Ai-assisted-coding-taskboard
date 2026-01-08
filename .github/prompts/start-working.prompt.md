---
description: Continue work on the next priority from the issue tracking system
agent: issue-tracking-expert
---

# Continue Work on Next Priority

**CRITICAL** NEVER commit and push unless asking the user first

**IMPORTANT** Always follow PLANNING-BOARD, even if the user has a document open

## Your Task

1. **Check current priorities**: Read [PLANNING-BOARD](issue-tracking/PLANNING-BOARD.md) to see what's next
1a. **If PLANNING-BOARD is empty**: use [Reprioritize prompt](.github/prompts/reprioritize.prompt.md) to reprioritize, and then go to step 1
2. **Select top priority**: Pick the first item from the planning board (unless blocked)
3. **Assess workload**: If the item is high-effort, follow instructions in [Split epic prompt](.github/prompts/split-epic.prompt.md) and reprioritize accordingly
4. **Move to in-progress**: Move the issue file from `backlog/` to `in-progress/`
5. **Read the issue file**: Understand problem, acceptance criteria, and technical context
6. **Make sure you understand**: If the issue is unclear, or have uncertaincies - ask the user followup questions, otherwise continue to tep 6.
7. **Don't do too much**: If the task seems too complex, break it down further and add new tasks in the backlog - Update PLANNING-BOARD accordingly
8. **Add implementation plan**: Update the issue file with detailed approach
9. **Update planning board**: Mark status as "In Progress" in PLANNING-BOARD.md
10. **Implement the solution**: Follow the workflow in [AGENTS](../../issue-tracking/AGENTS.md)
11. **Update progress**: Keep issue file and planning board current during work
12. **CRITICAL - ENSURE TESTS PASS**: Always ensure all tests pass before moving to done
13. **Complete**: Move to `done/` when finished, update planning board

## Constraints

- Follow instructions in [issue-tracking/AGENTS.md](../../issue-tracking/AGENTS.md)
- Keep PLANNING-BOARD.md updated (max 3-5 items, short notes only)
- Update issue progress log in real-time
- Run tests to verify completion
- Don't start multiple issues simultaneously

## Success Criteria

- [ ] Top priority issue moved to in-progress/
- [ ] Implementation plan added to issue file
- [ ] PLANNING-BOARD.md status updated
- [ ] Solution implemented following acceptance criteria
- [ ] All tests passing
- [ ] Issue file updated with final status
- [ ] Issue moved to done/
- [ ] PLANNING-BOARD.md updated (item removed, next priority added)

## Current Status

See `issue-tracking/PLANNING-BOARD.md` for:
- Top 5 current priorities
- Status of each item
- Blocking dependencies
- Effort estimates