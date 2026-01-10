# DataSkills Template — AI-Assisted Database Design & Data Engineering

> **Goal**: A single, non-duplicative reference template for AI-assisted database design and data pipeline work (Cursor Ask/Agent workflow), unified from:
> - **Document A**: `Data Skills_ AI-Assisted Database Design and Engineering.md`
> - **Document B**: `data_skills.md`

---

## 0) Comparison (to justify the unified notion)

### Summary (5–10 bullets)
- **Both documents align on a phase-based, AI-assisted workflow** starting with requirements clarification and then schema implementation.
- **Document A is a compact methodology/template** focused on “guided conversation” and a small set of prompt templates.
- **Document B is an expanded guide** with schema patterns (Prisma), tool snippets (TypeORM), pipeline patterns (batch/stream), and best practices (performance/security).
- **Overlap is high** around requirements → schema → migrations/seed; the unified template removes repeated prompt templates and keeps one canonical workflow.
- **New in B (relative to A)**: schema design patterns/examples, more explicit context engineering steps, best practices sections, and pipeline transformation patterns.
- **New in A (relative to B)**: a compact skills comparison table framing “Traditional vs AI-Assisted” tasks and explicit “AI for data quality tests with dbt”.
- **Impact level**: **MEDIUM** (B adds operational detail; A adds framing and advanced prompts). The unified template keeps both without duplicating steps.

### Key Differences (grouped by type)

#### Structure/Sections Changed
- **A is short and phase-driven**:
  - A: “## 2. The AI-Assisted Data Design Workflow” and “### Phase 1: Requirements Analysis (Ask Mode)” (A)
- **B is a full guide with many sections**:
  - B: “## Table of Contents … 2. Database Design Methodology … 7. Context Engineering Workflow …” (B)

#### Added Content (present in B but not A)
- **Concrete Prisma patterns and relationship examples**:
  - B: “### Prisma Schema Pattern” with `model User`/`model Board` example (B)
- **Broader best practices** (performance/security):
  - B: “### Performance … Optimize queries with proper indexes … Cache frequently accessed data” (B)
  - B: “### Security … Validate all input data … Implement row-level security when needed” (B)
- **Pipeline transformation patterns** (batch vs stream, queues):
  - B: “**Stream Processing** … Message queues (Kafka, RabbitMQ)” (B)

#### Added Content (present in A but not B)
- **Skills framing table (Traditional vs AI-Assisted)**:
  - A: “| Skill Area | Traditional Task | AI-Assisted Task | Key AI Benefit |” (A)
- **Explicit dbt test prompt example**:
  - A: “Generate data quality tests … using `dbt` … id unique/not null … email valid/unique” (A)

#### Modified Content (same idea, different wording/coverage)
- **Requirements prompt** is conceptually the same but B is more “context-engineering” explicit:
  - A: “Start by asking me questions to clarify the core entities…” (A)
  - B: “Analysis. Define Data Requirements. Start with Ask mode to clarify data needs…” (B)

#### Functional Changes (meaning changes)
- **No conflicting recommendations detected**; B extends breadth, A adds concise framing and a couple advanced prompts.

### Risk / Breaking Changes
- **LOW**: This is documentation/template consolidation; the main risk is losing a useful prompt or example. The unified template preserves all distinct concepts and keeps one canonical prompt per task type.

---

## 1) Overview

### Purpose
- Provide a repeatable **AI-assisted workflow** for database design and data pipeline work.
- Keep a single “source of truth” for **prompts, patterns, and best practices**.

### Core concepts (unified)
- **Data requirements analysis** via guided Q&A (Ask mode).
- **Schema design** in an ORM (Prisma/TypeORM) (Agent mode).
- **Migrations + seed data** generation (Agent mode).
- **Data pipelines (ETL)** and **data quality validation** (Agent mode with review/verification).

---

## 2) AI-Assisted Workflow (canonical)

### Phase 1 — Requirements Analysis (Ask mode)

#### Objective
Clarify entities, relationships, constraints, data volume, and query patterns before producing schemas.

#### Canonical prompt
```markdown
"Analysis. Help me design a database for [PROJECT].

Start in Ask mode: ask me questions to clarify:
- core entities and their attributes
- relationships
- constraints/business rules
- expected data volume and key query patterns
- scalability targets (e.g., up to 1 million users)"
```

#### Question checklist (merge of A + B)
- Who are the primary users and what data will they generate?
- What are the main entities?
- What attributes does each entity need?
- How are the entities related (cardinality, ownership, join entities)?
- What constraints apply (required fields, uniqueness, value rules)?
- What indexes are needed (foreign keys, frequently queried fields)?
- What data volume is expected?
- Any requirements for real-time processing/analytics?

---

### Phase 2 — Schema Design (Agent mode)

#### Objective
Translate the clarified domain model into an ORM schema with relationships, constraints, and indexes.

#### Canonical prompt
```markdown
@docs/requirements/database-prd.md
"Based on our requirements and the database PRD, create the Prisma (or TypeORM) schema for the domain model.

Include:
- all entities + fields
- relationships (1:1, 1:N, N:M)
- required fields and constraints (unique, not null)
- indexes for foreign keys and frequently queried fields
- timestamps (createdAt, updatedAt)"
```

#### Prisma schema pattern (example from B)
```prisma
model User {
  id        String   @id @default(uuid())
  email     String   @unique
  name      String
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt
  
  boards    Board[]
  
  @@map("users")
}
```

#### Relationship patterns (from B)
- **One-to-many**: parent has `children[]`; child has `parentId` + `@relation(...)`.
- **Many-to-many**: either implicit relation arrays or explicit join model (e.g., `TaskTag`).

---

### Phase 3 — Migrations + Seeding (Agent mode)

#### Objective
Generate safe schema migrations and seed scripts for development/testing.

#### Canonical prompt
```markdown
"Generate the database migration scripts for the schema.

Additionally, create a seed script that populates:
- [Entity1]: [count]
- [Entity2]: [count]
- realistic relationships between entities"
```

---

### Phase 4 — Testing + Validation (Agent mode)

#### Objective
Validate CRUD operations, relationships, and performance assumptions; add data quality checks.

#### Canonical prompts
```markdown
"Create tests for:
- CRUD operations for each core entity
- relationship operations (joins, cascades)
- expected query patterns (pagination, filtering, sorting)"
```

```markdown
"Generate data quality tests for our [table/model] using dbt. Ensure:
- primary keys are unique and not null
- [email/identifier] format is valid and unique
- timestamps like createdAt are always in the past"
```

---

## 3) Skill Areas (Traditional vs AI-Assisted framing)

| Skill Area | Traditional Task | AI-Assisted Task | Key AI Benefit |
|---|---|---|---|
| **Data Modeling** | Manually creating ERDs and conceptual schemas. | Generating schemas from natural language descriptions. | Speed, consistency. |
| **Schema Design** | Writing SQL DDL or ORM schema files by hand. | Generating Prisma/TypeORM schemas from a list of entities/fields. | Error reduction, best practice enforcement. |
| **Indexing Strategy** | Analyzing query logs and manually adding indexes. | Recommending indexes based on described query patterns. | Performance optimization. |
| **Migration Planning** | Writing and managing migration scripts manually. | Generating migration scripts from schema changes. | Reliability, safety. |
| **ETL Pipelines** | Writing extraction/transformation/loading scripts by hand. | Generating Python/SQL/TypeScript ETL scaffolds from source/target schema descriptions. | Development acceleration. |
| **Query Optimization** | Manual rewriting + execution plan analysis. | Suggesting rewrites/indexes based on slow query + context. | Expertise on demand. |

---

## 4) Tools + Patterns (unified)

### ORM and database tools
- **Prisma (recommended in B)**: schema, migrations, client generation, seed scripts.
- **TypeORM (shown in B)**: entity class definitions as an alternative ORM.

### Data pipeline patterns (from B)
- **Batch processing**: chunking, retries, error handling.
- **Stream processing**: real-time/event-driven; message queues like Kafka/RabbitMQ.

---

## 5) Advanced AI-Assisted Tasks (from A)

### Data pipeline orchestration (Airflow/Dagster)
```markdown
"Create an Airflow DAG that performs a daily ETL job:
1. Extract user data from a PostgreSQL database.
2. Anonymize sensitive fields (e.g., email, password).
3. Load the anonymized data into a BigQuery data warehouse for analytics."
```

---

## 6) Prompt Library (minimal, non-duplicative)

### A) Requirements discovery (Ask mode)
```markdown
"What data do we need to store for [PROJECT]?"
```

### B) Schema generation (Agent mode)
```markdown
"Based on our discussion, create the Prisma schema for:
- [Entity1] (attributes...)
- [Entity2] (attributes...)
- relationships between them

Include comments, constraints, and indexes."
```

### C) Migration creation
```markdown
"@prisma/schema.prisma Create migration for [changes].

Migration should:
- add/remove fields
- create/update indexes
- update relationships safely"
```

### D) Seed data
```markdown
"Create a seed script with realistic sample data for [entities] and their relationships."
```

---

## 7) Best Practices (from B; concise)

### Schema design
- Use UUIDs for primary keys.
- Add timestamps (`createdAt`, `updatedAt`) to all tables.
- Use enums for fixed value sets.
- Add indexes for frequently queried fields.
- Prefer soft deletes (`deletedAt`) instead of hard deletes when appropriate.

### Performance
- Optimize queries with proper indexes.
- Use connection pooling.
- Implement pagination for large datasets.
- Cache frequently accessed data.

### Security
- Use parameterized queries (ORM helps).
- Validate all input data.
- Implement row-level security when needed.

---

## 8) Usage Notes

- Start every project by running **Phase 1** until requirements are stable.
- Treat AI outputs as drafts: **review constraints, indexes, and relations** before shipping.
- Keep your PRD / requirements doc referenced in prompts (e.g., `@docs/requirements/database-prd.md`) to anchor context.

