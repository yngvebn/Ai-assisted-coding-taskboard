---
description: Resume work on an in-progress task handed off by another AI agent
agent: issue-tracking-expert
---

# Resume Work on In-Progress Task

**CRITICAL** NEVER commit and push unless asking the user first

## Your Task

You are resuming work that was started by another AI agent. Your goal is to pick up where they left off and continue the implementation seamlessly.

1. **Find in-progress work**: Check [in-progress/](../../issue-tracking/in-progress/) folder for active tasks
2. **Read handoff documentation**: Review the issue file(s) in `in-progress/` to understand:
   - What has been completed so far
   - What the current state is
   - What decisions have been made
   - What files have been modified
   - What blockers exist
   - What the next steps are
3. **⚠️ CHECK FOR CODE REVIEW FEEDBACK FIRST**: Before proceeding with implementation:
   - Look for "Code Review Feedback" or "Review Comments" section in the issue file
   - Check for pull request comments or review feedback documented in the issue
   - Check for "Needs Revision" or similar status indicators
   - **If feedback exists**: Address ALL review feedback BEFORE continuing implementation
   - Document feedback resolution in progress log with references to specific comments
   - Only proceed to step 5 after all feedback is addressed
4. **Review PLANNING-BOARD**: Read [PLANNING-BOARD](../../issue-tracking/PLANNING-BOARD.md) to see current status and priorities
5. **Verify your understanding**: If anything is unclear about the handoff state, ask the user for clarification
6. **Resume implementation**: Continue from the documented "Next Steps" (only after addressing any review feedback)
7. **Update progress log**: Add entries to the issue file's progress log as you work (with timestamps)
8. **Update PLANNING-BOARD**: Keep the planning board current with your progress
9. **Complete or handoff**: When done, move to `done/` OR prepare another handoff using [handoff prompt](handoff.prompt.md)

## Constraints

- Follow instructions in [issue-tracking/AGENTS.md](../../issue-tracking/AGENTS.md)
- Keep PLANNING-BOARD.md updated (max 3-5 items, short notes only)
- Update issue progress log in real-time with timestamps (YYYY-MM-DD HH:MM format)
- Run tests to verify completion
- Don't start multiple issues simultaneously
- Respect decisions and approach documented by previous AI agent
- If you disagree with previous approach, discuss with user before changing direction

## Success Criteria

- [ ] In-progress issue file reviewed and understood
- [ ] PLANNING-BOARD.md reviewed and current
- [ ] Previous AI's "Next Steps" completed or progressed
- [ ] Progress log updated with your work (timestamped entries)
- [ ] PLANNING-BOARD.md status reflects current state
- [ ] Tests passing (or failing tests documented with analysis)
- [ ] Either:
  - [ ] Issue completed and moved to `done/` with final summary, OR
  - [ ] Handoff documentation prepared for next AI agent

## What to Look for in Handoff Documentation

The previous AI should have documented:

### In the Issue File
- **Status section**: Current state (In Progress, Blocked, Needs Revision, etc.)
- **Code Review Feedback**: Any PR comments or review feedback requiring action
- **Progress Log**: Timestamped entries showing:
  - ✅ What has been completed
  - 🔄 What is currently being worked on
  - ⏳ What remains to be done
  - 🔍 Review feedback that needs addressing
- **Decisions Made**: Architectural or technical choices and rationale
- **Files Modified**: List of changed files with brief descriptions
- **Test Status**: Which tests pass/fail/are pending
- **Blockers**: Any dependencies or issues preventing progress
- **Next Steps**: Clear, actionable items for you to continue

### In PLANNING-BOARD.md
- Latest status of the in-progress task
- Current phase or milestone
- Recent timestamp ("Last Updated")
- Consistency with the issue file

## Handoff Quality Check

If the handoff documentation is incomplete or unclear:
1. ⚠️ Flag the issue with the user
2. Ask clarifying questions about:
   - What was actually completed
   - What the current state is
   - What needs to be done next
3. Update the documentation yourself before proceeding
4. Consider reviewing git history to understand recent changes

## Progress Log Format

When adding your own progress entries, use this format:

```markdown
**2025-11-18 14:30 - [Your Action]**

**Code Review Feedback Addressed** (if applicable):
- 🔍 [Specific feedback point] → [How it was addressed]
- 🔍 [Another feedback point] → [Resolution]

**Completed**:
- ✅ [Specific achievement with details]
- ✅ [Another achievement]

**In Progress**:
- 🔄 [What you're currently working on]

**Next Steps**:
- ⏳ [Next specific action]
- ⏳ [Following action]

**Files Modified**:
- `path/to/file.ts` - [Description of change]

**Blockers**: [None or describe blocker]
```

## Related Resources

- [Handoff Prompt](handoff.prompt.md) - Use this to prepare handoff to next AI
- [Issue Tracking AGENTS.md](../../issue-tracking/AGENTS.md) - Workflow guidelines
- [PLANNING-BOARD.md](../../issue-tracking/PLANNING-BOARD.md) - Current priorities
- [In-Progress Issues](../../issue-tracking/in-progress/) - Active work