## WEB_template.md — Unified template for AI-assisted web development (Cursor)

### Purpose
Use this as the **single, reusable session template** to turn a design + requirements into a **production-quality frontend** via AI, using **structured context**, **phase-based execution**, and **fast iteration**.

### Core principles (execution style)
- **Momentum > perfection**: ship runnable increments; iterate later.
- **Working artifacts > explanations**: prefer generating real files/components over theory.
- **Explicit context**: always attach the most relevant files via `@...` references.
- **Granular iteration**: build component-by-component; assemble pages after components are stable.

---

## How to use this template in a Cursor session

### 1) Pin essential context (recommended)
Pin the files that define “truth” for the session:
- `PRD.md` (requirements/spec)
- `RULES.md` (coding standards)
- Design references (screenshots, Figma links, notes)
- Any existing architecture / component plan docs

### 2) Start session (copy/paste)
```markdown
Follow pinned context. Vibe mode ON.

Goal: Implement [PAGE/FEATURE] from design + requirements.
Stack: [e.g., Next.js 14 App Router + TypeScript + Tailwind CSS]
Non-negotiables: pixel-perfect, 60fps performance, WCAG AA accessibility.
```

### 3) Choose analysis/implementation mode (workflow hint)
- **Ask Mode**: requirements clarification, design analysis, component breakdown.
- **Agent Mode**: scaffold, implement, refactor, test, iterate.

---

## Inputs you should provide (minimum viable context)

### Design reference (at least one)
- Screenshot/mockup image(s)
- Figma link
- Detailed written description / wireframe

### Product + UX
- Page/component purpose
- Key interactions (hover, active, empty states, loading, errors)
- Responsive expectations (mobile/tablet/desktop)

### Technical constraints (if any)
- Framework/runtime (e.g., Next.js App Router)
- Styling approach (e.g., Tailwind CSS)
- Data sources (API endpoints), auth, feature flags
- Accessibility targets (e.g., WCAG 2.1 AA)

---

## End-to-end workflow (phases)

### Phase 0 — One-line framing (fast alignment)
```markdown
Make me a [TYPE OF WEB APP]
for [WHO IT'S FOR]
that helps [GOAL / PROBLEM]
by doing [WHAT IT DOES]
```

### Phase 1 — Requirements clarification (Ask Mode)
Goal: turn “vague idea” into an implementable spec (or confirm PRD completeness).

Prompt:
```markdown
I need to build [project/page/feature]. Help me create/validate a detailed PRD
by asking clarifying questions. Focus on scope, edge cases, and success criteria.
```

### Phase 2 — Design analysis + component breakdown (Ask Mode)
Goal: extract a reusable component hierarchy and responsibilities before coding.

Prompt:
```markdown
@design/[mockup-or-screenshot].png
Analyze this design and break it down into a hierarchy of reusable React components
(Atoms/Molecules/Organisms/Templates/Pages). For each component list:
- Name
- Responsibilities
- Props (TypeScript)
- State (if any)
- Accessibility considerations
```

Output artifact to generate (recommended): `docs/component-plan.md`

### Phase 3 — Component implementation (Agent Mode, component-by-component)
Goal: implement one component at a time for quality and debuggability.

Prompt:
```markdown
@docs/component-plan.md
Create the `[ComponentName]` component using TypeScript and Tailwind CSS.
Requirements:
- Match the design (spacing/typography/colors)
- Mobile-first responsive behavior
- WCAG AA accessibility (semantic HTML + ARIA where needed)
Return:
- Component code
- Props types/interfaces
```

### Phase 4 — Page assembly + integration (Agent Mode)
Goal: assemble stable components into pages/views and add data loading, errors.

Prompt:
```markdown
@components/[...relevant components...]
Assemble the `[PageName]` page to match the mockup.
Include:
- Responsive layout
- Data fetching from `[API endpoint]`
- Loading state
- Error state
```

### Phase 5 — Quality passes (Agent Mode)
Goal: enforce the three non-negotiables: fidelity, performance, accessibility.

#### Pixel-perfect refinement
```markdown
Review the UI against the design and fix mismatches.
Be specific: padding, font sizes, line height, colors, border radius, spacing.
```

#### 60fps performance pass
```markdown
Review `[Component/Page]` for unnecessary re-renders and improve performance.
Apply memoization where appropriate (e.g., React.memo, useCallback) and reduce work per render.
```

#### Accessibility pass (WCAG AA)
```markdown
Audit `[Component/Page]` for accessibility.
Ensure: keyboard navigation, focus states, semantic landmarks, ARIA only when needed,
alt text for images, and adequate color contrast (WCAG AA).
```

### Phase 6 — Testing + checkpoints (Agent Mode)
Goal: lock in behavior and prevent regressions as you iterate fast.

Prompts:
```markdown
Write unit tests for `[ComponentName]` using Jest + React Testing Library.
Cover: key interactions, states, and accessibility-related expectations.
```

```markdown
Create checkpoint: [milestone description]
```

```markdown
Rollback to checkpoint: [name]
```

---

## Quality bar (non-negotiables)

### Pixel-perfect implementation
- Match layout, spacing, typography, and visual hierarchy to the design.
- Iterate using concrete feedback (e.g., “padding should be 16px not 20px”).

### 60fps performance
- Avoid unnecessary re-renders.
- Keep animations cheap; minimize layout thrash and heavy effects.

### Accessibility (WCAG AA)
- Semantic HTML first; ARIA when semantics aren’t sufficient.
- Keyboard navigation and visible focus.
- Meaningful alt text; correct labels; sufficient contrast.

---

## Prompt templates (quick reference)

### Create a new component
```markdown
Create a new React component named `[ComponentName]` that [does what].
Use TypeScript and Tailwind CSS. Include props types, responsive behavior,
and WCAG AA accessibility considerations.
```

### Style a component to match design
```markdown
Style `[ComponentName]` to match the design.
Key styles: [colors], [typography], [spacing], [layout rules], [states].
```

### Implement an API call (hook)
```markdown
Create a custom hook `useFetch[DataName]` that fetches from `[API endpoint]`.
Handle loading, success, and error states.
```

### Responsive adjustments
```markdown
Make `[ComponentName]` responsive (mobile-first).
Define changes for mobile, tablet, desktop and implement using Tailwind responsive utilities.
```

---

## Context management (keep the agent effective)

### What to reference explicitly
- The exact design asset(s) being implemented (`@design/...`)
- The component plan / PRD (`@docs/...`)
- The specific component/page file(s) being modified (`@...`)
- Any rules/standards file(s) that must be followed

### How to iterate
- Prefer small, testable increments.
- If the session becomes messy, checkpoint and refactor rather than restarting from scratch.

---

## Success criteria (definition of “done”)
- The UI matches the design with high fidelity.
- Responsive behavior works across defined breakpoints.
- Accessibility meets WCAG AA expectations.
- Performance is smooth (no obvious jank; avoid expensive re-renders).
- Tests exist for critical components/interactions (where applicable).

