---
description: "Prepare current task for handoff to another AI agent"
agent: issue-tracking-expert
---

# Prepare Task Handoff

Ensure the current in-progress task has complete documentation for seamless handoff to another AI agent.

## Your Task

1. **Identify current work**: Find the task in [in-progress/](../../issue-tracking/in-progress/)
2. **Verify completeness**: Ensure all required sections are filled out
3. **Update progress log**: Document current state with timestamp
4. **Update PLANNING-BOARD**: Ensure board reflects current progress accurately
5. **Document decisions**: Record any decisions made during implementation
6. **List modified files**: Track all files changed so far
7. **Note blockers**: Document any blockers or dependencies
8. **Update test status**: Current state of unit/E2E/backend tests

## Required Documentation

### Issue File Must Have

- **Status**: Clearly marked as "In Progress"
- **Implementation Plan**: Detailed approach and strategy
- **Progress Log**:
  - What has been completed
  - What is currently being worked on
  - What remains to be done
- **Decisions Made**: Key architectural or technical choices
- **Files Modified**: Complete list with brief description of changes
- **Test Status**: Which tests are passing/failing/pending
- **Blockers**: Any dependencies or issues preventing progress
- **Next Steps**: Clear, actionable next steps for continuation

### PLANNING-BOARD.md Must Have

- **Current item status**: Latest progress on active work
- **Accurate phase information**: Current phase and completion status
- **No confusion**: Clear, concise notes about where things stand
- **Updated timestamp**: Recent "Last Updated" date
- **Consistent with issue file**: Status matches the issue file details

## Handoff Checklist

- [ ] Issue file in `in-progress/` identified
- [ ] Status section is current
- [ ] Implementation Plan is detailed and complete
- [ ] Progress Log has today's timestamp with current state
- [ ] All decisions documented with rationale
- [ ] Complete list of modified files
- [ ] Test status clearly documented
- [ ] Blockers/dependencies explicitly listed
- [ ] Next steps are clear and actionable
- [ ] PLANNING-BOARD.md updated with current progress
- [ ] PLANNING-BOARD.md timestamp is current
- [ ] No ambiguity in documentation

## Documentation Quality Standards

### Good Progress Log Entry
```markdown
**2025-10-29 14:30 - Current State**

**Completed**:
- ✅ Phase 1: Planning & Design (100%)
  - Requirements gathering complete
  - Design documents finalized
  - Architecture decisions documented
- ✅ Phase 2: Infrastructure Setup (100%)
  - Development environment configured
  - Required tools and dependencies installed
  - All configurations verified

**In Progress**:
- 🔄 Phase 3: Core Implementation (0%)
  - About to start main feature development

**Remaining**:
- ⏳ Phase 3: Complete core feature implementation
- ⏳ Phase 4: Integration & Testing
- ⏳ Phase 5: Documentation & Validation
- ⏳ Phase 6: Deployment

**Files Modified**:
- `config/settings.yml` - Added new configuration options
- `src/services/init.ts` - Created initialization scripts
- `.env.local` - Added environment variables

**Blockers**: None currently

**Next Step**: Begin core feature implementation
```

### Good PLANNING-BOARD Entry
```markdown
## 🚨 CRITICAL PRIORITY: Feature Implementation

### Major Feature Implementation (CRITICAL) 🚀
**Issue**: `in-progress/FEATURE-major-feature-implementation.md`
**Status**: ✅ **Phase 2 Complete - Phase 3 Starting**
**Branch**: `feature/major-implementation`

**✅ Phase 1 Complete**: Planning & Design
**✅ Phase 2 Complete**: Infrastructure Setup
**🔄 Phase 3 Starting**: Core Implementation

**Next Tasks**:
1. Install required dependencies
2. Create core service modules
3. Implement main business logic
```

## Constraints

- Follow [AGENTS.md](../../issue-tracking/AGENTS.md) instructions
- Keep PLANNING-BOARD.md concise (short notes only)
- Use timestamps in Progress Log (YYYY-MM-DD HH:MM format)
- Be explicit about what's done vs. what's in progress
- List actual file paths (not generic descriptions)
- Update "Last Updated" date in PLANNING-BOARD.md

## Success Criteria

- [ ] Another AI agent can read the issue file and immediately understand:
  - What has been done
  - What the current state is
  - What needs to be done next
  - What decisions have been made and why
  - What files have been changed
  - What blockers exist
- [ ] PLANNING-BOARD.md accurately reflects current progress
- [ ] No ambiguity or confusion in documentation
- [ ] All timestamps are current
- [ ] Next steps are clear and actionable

## Anti-Patterns to Avoid

❌ **Vague progress notes**
```markdown
- Made some progress on the migration
- Working on database stuff
```

✅ **Specific progress notes**
```markdown
- ✅ Completed database schema design (15 tables)
- ✅ Local development container running with all extensions
- 🔄 Currently installing required packages
```

❌ **Generic next steps**
```markdown
- Continue working on the database
```

✅ **Specific next steps**
```markdown
1. Run: `npm install required-package`
2. Create DbContext class in `src/Infrastructure/Data/PostgresDbContext.cs`
3. Define entity models for User, Team, Session entities
```

❌ **Outdated PLANNING-BOARD**
```markdown
**Last Updated**: 2025-10-15
**Status**: Starting Phase 2
```

✅ **Current PLANNING-BOARD**
```markdown
**Last Updated**: 2025-10-29
**Status**: ✅ Phase 2 Complete - Phase 3 Starting
```

## Output Format

After reviewing and updating documentation, provide a summary:

1. **Current Task**: [Name and link to issue file]
2. **Progress**: [High-level summary of what's complete]
3. **Current State**: [What's actively being worked on]
4. **Next Steps**: [3-5 specific next actions]
5. **Blockers**: [Any blockers or "None"]
6. **Documentation Status**: [Confirmation that all docs are updated]

## Related Resources

- [Issue Tracking AGENTS.md](../../issue-tracking/AGENTS.md) - Workflow guidelines
- [PLANNING-BOARD.md](../../issue-tracking/PLANNING-BOARD.md) - Current priorities
- [In-Progress Issues](../../issue-tracking/in-progress/) - Active work
