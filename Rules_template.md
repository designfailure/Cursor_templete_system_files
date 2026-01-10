# Rules_template.md — Unified Cursor Rules Framework (non-duplicative)

## Purpose

This file is a **single source of truth** for designing and maintaining **Cursor Rules** that guide AI behavior and enforce project standards. Use it to create and curate rule files under `.cursor/rules/`.

## Core Concept

**Rules are persistent prompts**: structured, versionable instructions that are automatically included in the AI’s context during editing and generation, so standards remain consistent without repeating them in every chat.

## Rule System Model

### Directory layout (rule hierarchy by application trigger)

```
.cursor/rules/
├── always/              # Universal standards; applied to every interaction
├── auto-attached/       # Applied by file globs/patterns
├── agent-requested/     # Optional, specialized; AI may apply when relevant
└── manual/              # Only when explicitly referenced via @
```

### Precedence (conflict resolution)

When two rules conflict, prefer the most specific, most intentionally applied rule:

1. **Manual** (explicit `@rule-name`)
2. **Auto-attached** (path matches glob)
3. **Always** (universal baseline)

(`agent-requested` is intentionally situational and should not override explicit/manual intent.)

## Rule File Format (`.mdc`)

Rules are Markdown files with YAML frontmatter metadata plus a body containing actionable guidance.

### Canonical frontmatter fields

- **`description`**: one-sentence purpose (used for discovery/selection)
- **`alwaysApply`**: `true` or `false`
- **`globs`**: list of patterns (only for auto-attached rules)

### Recommended rule body structure

Use this consistent outline so rules remain scannable and maintainable:

1. **Purpose**: what the rule governs and why it exists
2. **Do / Don’t**: specific, testable standards (not vague advice)
3. **Examples**: at least one ✅ good and one ❌ bad example when relevant
4. **Notes**: edge cases, exceptions, interaction with tooling
5. **References**: links/docs/ADRs that anchor the rule

## Rule Templates (copy/paste)

### Template: Always Rule (universal baseline)

```md
---
description: <Brief description>
alwaysApply: true
---

# <Rule name>

## Purpose
<Why this rule exists; what it protects/standardizes>

## Standards
### Do
- <Actionable requirement>

### Don't
- <Prohibited pattern>

## Examples
### ✅ Good
<Example>

### ❌ Bad
<Example>

## References
- <Link or doc path>
```

### Template: Auto-Attached Rule (path-based)

```md
---
description: <Brief description>
alwaysApply: false
globs: ["<pattern1>", "<pattern2>"]
---

# <Rule name>

## Purpose
<Why these files need different standards>

## Standards
### Do
- <File-type specific standard>

### Don't
- <Anti-pattern for these files>

## Examples
### ✅ Good
<Example>

### ❌ Bad
<Example>
```

### Template: Agent-Requested Rule (situational expertise)

Use for specialized guidance that is not always relevant (e.g., performance optimization, legacy refactoring).

```md
---
description: <Brief description>
alwaysApply: false
---

# <Rule name>

## When to use
- <Signals that make this rule relevant>

## Standards
- <Actionable, situation-specific guidance>
```

### Template: Manual Rule (explicit invocation)

Use when you want a rule applied only intentionally (e.g., migrations, temporary constraints).

```md
---
description: <Brief description>
alwaysApply: false
---

# <Rule name>

## When to apply
Only when explicitly referenced, for example:
`@<rule-name> "<short instruction>"`

## Standards
- <Actionable guidance>
```

## Baseline Rule Set (recommended minimum)

Start projects with these domains as separate rule files, then extend as needed:

- **Security** (almost always `always/`): secrets handling, input validation, safe logging, dependency hygiene
- **Code style** (`always/`): formatting, naming, language constraints (e.g., TypeScript strict mode)
- **Architecture** (`always/` + selective `auto-attached/`): layering, boundaries, where business logic lives
- **Testing** (`auto-attached/` for test globs + `always/` for expectations): structure, critical paths, error scenarios
- **Documentation** (`manual/` or `always/` depending on team): public APIs, “explain WHY”, examples for utilities

## Writing Rules That Work (quality bar)

- **Specific and actionable**: replace “write clean code” with measurable constraints and patterns.
- **One topic per file**: keep scope narrow; split by concern rather than dumping everything into one rule.
- **Include the rationale**: explain *why* when it prevents misunderstandings (especially for architecture/security).
- **Prefer examples over prose**: show canonical patterns and anti-patterns.
- **Avoid contradictions**: rules should not fight each other or the project’s tooling (linters/formatters).
- **Keep them current**: review periodically; remove obsolete constraints.

## Bootstrapping Rules (optional workflow)

- **Generate initial rules from the codebase**: use Cursor’s rule generation, then curate the output.
- **Update from chat learnings**: when a new decision emerges (e.g., “we always use X”), capture it in the appropriate rule file so it becomes persistent.

## Testing and Maintenance Checklist

- [ ] Rule frontmatter is correct (`alwaysApply`, `globs` when needed)
- [ ] Instructions are unambiguous and testable
- [ ] Examples compile / match the project’s stack
- [ ] No overlaps that cause duplicate or conflicting guidance
- [ ] New rules are validated by running a realistic prompt on a matching file
- [ ] Rules are versioned alongside code (and reviewed on schedule)

## References (source documents merged into this template)

- `Cursor RULES.md`
- `rule.md`
- `Cursor Rules and System Prompting_ A Framework for AI Governance.md`

