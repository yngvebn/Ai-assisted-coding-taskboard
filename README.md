# AI-Assisted Coding Taskboard

A generalized, file-based issue-tracking system designed for AI-assisted software development. This repository provides agents, skills, and automation scripts to manage the complete lifecycle of development tasks from bug reports to feature completion.

## TLDR

**What is this?** A lightweight, transparent task management system optimized for AI collaboration.

**Core workflow:**
1. Report bugs/features with `/report-issue` → Creates documented issue in `backlog/`
2. Start work with `/start-working` → Picks top priority, implements with TDD, moves to `done/`
3. Manage priorities in `PLANNING-BOARD.md` (3-5 items max)
4. Track everything with PowerShell scripts and YAML frontmatter

**Key benefits:**
- ✅ File-based (no database, fully transparent)
- ✅ AI-optimized workflows with specialized agents
- ✅ TDD-first approach with continuous testing
- ✅ Real-time progress tracking
- ✅ Production-ready with risk assessment framework
- ✅ Automated with PowerShell scripts

## Quick Start

### For Users Wanting Help

```
/repo-help
```

This invokes the comprehensive help skill that explains:
- How the system works
- Available agents, skills, and prompts
- Common workflows and scripts
- Best practices and troubleshooting

### For Users Reporting Issues

```
/report-issue
```

This skill will:
1. Ask clarifying questions about your bug/feature
2. Investigate the codebase thoroughly
3. Identify root causes and affected components
4. Create a comprehensive issue file ready for implementation

### For Users Starting Work

```
/start-working
```

This skill will:
1. Check the PLANNING-BOARD for priorities
2. Pick the top unblocked item
3. Follow TDD workflow (test first, then implement)
4. Update progress in real-time
5. Move to done/ when complete

## System Architecture

### Repository Structure

```
.
├── .claude/skills/           # Reusable workflow skills
│   ├── report-issue/         # Bug/feature documentation
│   ├── start-working/        # Implementation workflow
│   ├── skill-creator/        # Skill creation guide
│   └── repo-help/            # System help guide
│
├── .github/
│   ├── agents/               # Specialized AI agents
│   │   ├── issue-reporter.agent.md
│   │   └── issue-tracking-expert.agent.md
│   │
│   └── prompts/              # Workflow templates
│       ├── start-working.prompt.md
│       ├── reprioritize.prompt.md
│       └── split-epic.prompt.md
│
├── issue-tracking/           # Issue management system
│   ├── AGENTS.md            # 📖 PRIMARY REFERENCE - Complete workflow documentation
│   ├── PLANNING-BOARD.md    # Current priorities (3-5 items)
│   ├── backlog/             # New issues
│   ├── in-progress/         # Active work
│   ├── done/                # Recently completed
│   └── archive/             # Historical completions
│
└── scripts/                 # PowerShell automation
    ├── issue-create.ps1
    ├── issue-start.ps1
    ├── issue-complete.ps1
    ├── backlog-view.ps1
    └── archive-old-issues.ps1
```

### Core Components

**Agents**: Specialized AI configurations for specific workflows
- `issue-reporter.agent.md` - Analyzes and documents issues (investigation only)
- `issue-tracking-expert.agent.md` - Expert on managing the system

**Skills**: Reusable workflows invoked with `/skill-name`
- `/report-issue` - Create comprehensive issue documentation
- `/start-working` - Pick up next priority and implement
- `/repo-help` - Get help understanding the system

**Scripts**: PowerShell automation for common operations
- `issue-create.ps1` - Create new issues
- `issue-start.ps1` - Start working on issues
- `issue-complete.ps1` - Mark issues complete
- `backlog-view.ps1` - View and filter backlog

## Issue Lifecycle

```
┌─────────────┐
│   backlog/  │  ← Issues created here
└──────┬──────┘
       │
       │ Start work (script or skill)
       │
┌──────▼──────┐
│ in-progress/│  ← Active implementation with TDD
└──────┬──────┘
       │
       │ Complete (all tests passing)
       │
┌──────▼──────┐
│    done/    │  ← Recently completed (~20 max)
└──────┬──────┘
       │
       │ Archive (>90 days old)
       │
┌──────▼──────┐
│  archive/   │  ← Historical completions
└─────────────┘
```

## Essential Documentation

### Start Here
- **[issue-tracking/AGENTS.md](issue-tracking/AGENTS.md)** - Complete system documentation (workflows, conventions, best practices)
- **[.claude/skills/repo-help/SKILL.md](.claude/skills/repo-help/SKILL.md)** - Comprehensive help guide

### For Specific Workflows
- [Report Issue Skill](.claude/skills/report-issue/SKILL.md) - Creating issues
- [Start Working Skill](.claude/skills/start-working/SKILL.md) - Implementation workflow
- [Issue Tracking Expert Agent](.github/agents/issue-tracking-expert.agent.md) - System management

## Common Workflows

### 1. View Current Priorities

```powershell
# Check what's next
cat issue-tracking/PLANNING-BOARD.md

# View full backlog with statistics
.\scripts\backlog-view.ps1 -ShowStats
```

### 2. Create a New Issue

**Using skill (recommended):**
```
/report-issue
```

**Using script:**
```powershell
# Interactive mode
.\scripts\issue-create.ps1

# Non-interactive
.\scripts\issue-create.ps1 -Type bug -Title "Timer not pausing" -Priority high -Effort 2h -NonInteractive
```

### 3. Start Working

**Using skill (recommended):**
```
/start-working
```

**Using scripts:**
```powershell
# Start specific issue
.\scripts\issue-start.ps1 FEATURE-issue-name

# [Implement following TDD workflow]

# Complete when done
.\scripts\issue-complete.ps1 FEATURE-issue-name
```

### 4. Filter and Sort Backlog

```powershell
# View high priority items
.\scripts\backlog-view.ps1 -FilterPriority high

# Find quick wins (sorted by effort)
.\scripts\backlog-view.ps1 -SortBy effort

# High priority bugs only
.\scripts\backlog-view.ps1 -FilterPriority high -FilterType bug
```

### 5. Archive Old Completed Items

```powershell
# Archive issues completed >90 days ago
.\scripts\archive-old-issues.ps1

# Preview without moving
.\scripts\archive-old-issues.ps1 -WhatIf
```

## Development Principles

### 1. Test-Driven Development (TDD)

Always follow the red-green workflow:
1. Check existing test coverage
2. Write failing test (RED)
3. Implement fix (GREEN)
4. Monitor tests continuously
5. Add integration/E2E tests

### 2. Real-Time Progress Tracking

Update issue Progress Log frequently:
```markdown
## Progress Log
- 2025-11-19 14:30 - Started, reviewed existing tests
- 2025-11-19 14:45 - Added failing test
- 2025-11-19 15:00 - Implemented fix
- 2025-11-19 15:15 - All tests passing
```

### 3. Analysis Before Action

Before creating issues:
- Research thoroughly using search tools
- Identify root cause with file paths and line numbers
- Understand affected components
- Check test coverage
- Ask clarifying questions

### 4. Keep PLANNING-BOARD Lean

- Maximum 3-5 items
- Most important at top
- Remove completed immediately
- Update status as work progresses

## Issue File Structure

All issues use YAML frontmatter:

```yaml
---
id: FEATURE-example              # From filename
type: feature                    # bug | feature | refactor | explore
priority: high                   # high | medium | low
effort: 4h                       # 2h, 4h, 1d, 3d, 1w
status: backlog                  # backlog | in-progress | done
labels: [frontend, api]          # Tags for filtering
depends_on: []                   # Dependencies
blocks: []                       # Blocks these issues
created: 2025-11-24             # YYYY-MM-DD
updated: 2025-11-24             # Last modified
started: null                    # Set when work starts
completed: null                  # Set when done
---

# [Type]: [Description]

## Problem Statement
## Acceptance Criteria
## Technical Context
## Implementation Plan (added during work)
## Progress Log (real-time updates)
## Verification
## Resolution (final outcome)
```

## File Naming Conventions

- **Bugs**: `BUG-timer-not-pausing.md`
- **Features**: `FEATURE-export-results.md`
- **Refactors**: `REFACTOR-consolidate-auth-logic.md`
- **Explorations**: `EXPLORE-database-options.md`

## PowerShell Scripts Reference

| Script | Purpose | Example |
|--------|---------|---------|
| `backlog-view.ps1` | View & filter issues | `.\scripts\backlog-view.ps1 -ShowStats` |
| `issue-create.ps1` | Create new issue | `.\scripts\issue-create.ps1 -Type bug -Title "..." -NonInteractive` |
| `issue-start.ps1` | Start working | `.\scripts\issue-start.ps1 FEATURE-name` |
| `issue-complete.ps1` | Mark complete | `.\scripts\issue-complete.ps1 FEATURE-name` |
| `archive-old-issues.ps1` | Archive old items | `.\scripts\archive-old-issues.ps1` |

## Risk Assessment for Production

High-risk issues include additional validation:

**Risk Categories:**
- `security` - Auth, data exposure
- `data-loss` - Could cause data deletion
- `performance` - Could degrade performance
- `breaking-change` - API/backward compatibility
- `integration` - Third-party dependencies
- `database` - Schema changes
- `compliance` - GDPR, legal requirements

**Risk Impact:**
- `high` - Data loss, security breach, downtime
- `medium` - Feature degradation, poor UX
- `low` - Minor bugs, easy to rollback

**High-risk issues require:**
- Security review
- Staging validation
- Rollback procedure
- Monitoring setup
- Load testing (if performance-critical)

## Best Practices

1. ✅ **Analysis first** - Research thoroughly with file paths and line numbers before creating issues
2. ✅ **TDD always** - Write test first (red), then implement (green)
3. ✅ **Real-time updates** - Timestamp every step in Progress Log
4. ✅ **One thing at a time** - Limit work in in-progress/ to 1-2 items
5. ✅ **Monitor tests continuously** - Keep test suite running
6. ✅ **Be specific** - Include file paths, line numbers, actionable descriptions
7. ✅ **Document decisions** - Record WHY in Progress Log, not just WHAT
8. ✅ **Complete fully** - All verification criteria met before moving to done/

## Getting Help

### Use the Help Skill

```
/repo-help
```

Provides comprehensive guidance on:
- System architecture and components
- Available workflows and scripts
- Best practices and troubleshooting
- Common operations and examples

### Read Core Documentation

- **[issue-tracking/AGENTS.md](issue-tracking/AGENTS.md)** - Complete workflow documentation
- **[.github/agents/issue-tracking-expert.agent.md](.github/agents/issue-tracking-expert.agent.md)** - System management expert
- **[.claude/skills/repo-help/SKILL.md](.claude/skills/repo-help/SKILL.md)** - Full help guide

## Extending the System

Want to add new skills or customize workflows?

```
/skill-creator
```

See [.claude/skills/skill-creator/SKILL.md](.claude/skills/skill-creator/SKILL.md) for guidance on creating effective skills.

## Why File-Based?

- ✅ **Transparent**: Everything is plain text, version-controlled
- ✅ **Portable**: No database, works anywhere
- ✅ **AI-friendly**: Markdown and YAML are easy for AI to parse
- ✅ **Flexible**: Customize workflows without complex tools
- ✅ **Auditable**: Full history in git
- ✅ **Simple**: No setup, no configuration

## Contributing

This is a generalized template repository. Adapt it to your project:
1. Fork/copy the repository structure
2. Customize agents for your architecture patterns
3. Adjust scripts for your tech stack
4. Modify issue templates for your workflow
5. Create project-specific skills

## License

See LICENSE.txt for complete terms.

---

**Need help?** Use `/repo-help` or read [issue-tracking/AGENTS.md](issue-tracking/AGENTS.md) for complete documentation.
