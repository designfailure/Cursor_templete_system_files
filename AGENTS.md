# AGENTS.md

## Cursor Cloud specific instructions

This is a **documentation-only repository** containing Markdown templates and guides for AI-assisted development with Cursor IDE. There is no source code, no dependencies, no build system, and no runnable services.

### Repository structure

All files are Markdown documents at the repository root:
- `README.md` -- Main guide on using Cursor (written in Slovenian)
- `CONTEXT_ENGINEERING_COMPREHENSIVE_PLAN.md` -- Comprehensive context engineering plan and ontology
- `CLAW_AGENTIC_WORKFLOW_PLAN.md` -- Plan for using Cursor+AGENTS as an OpenClaw alternative
- `PRD_template.md` -- Product Requirements Document template
- `WEB_template.md` -- AI-assisted web development workflow template
- `DataSkills_template.md` -- AI-assisted database design template
- `Rules_template.md` -- Framework for creating Cursor rules
- `LICENSE` -- CC0 1.0 Universal (public domain)

### Development environment

- No package manager, no dependencies, no build step.
- Linting: `markdownlint '*.md'` (requires `markdownlint-cli` installed globally via npm). Existing files have stylistic warnings (line length, blank lines) which are intentional for readability.
- The "application" is the documentation itself -- view Markdown files with any Markdown-capable editor or renderer.

### What future agents should know

- Do not attempt to install project dependencies or start services -- there are none.
- Contributions to this repo are new or edited Markdown files.
- The ontology in `CONTEXT_ENGINEERING_COMPREHENSIVE_PLAN.md` Section 5 is the canonical entity model referenced by other documents.
