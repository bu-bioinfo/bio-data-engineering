# Biological Data Engineering — Course Outline, Assignment Scaffolding & Assessment Strategy

This document expands the course into its structural components: the topic units, the artifact sequence that constitutes assessment, and a concrete strategy for running portfolio assessment at scale (50–60 students, limited TA support) consistently, transparently, and with deliberate LLM involvement.

---

## Part 1 — Topic units

The course is organized into seven units. Units are sized unequally on purpose: modeling and ETL are the heaviest because they are where the craft lives. Each unit is framed as an answer to the course's driving question — *how do we make biological data findable, trustworthy, and reusable?*

### Unit 0 — Orientation: the data-engineering mindset (≈1 week)

Why infrastructure is the bottleneck. The data lifecycle in a biological project. The course's recurring dataset, introduced in its raw, messy state. The studio workflow and the Git-based mechanics of the course. First framing of LLMs as toolchain: the *specify → generate → verify → document* loop, and why biological data is precisely the domain where "plausible but wrong" is dangerous.

### Unit 1 — Data modeling (≈3 weeks, the conceptual spine)

The discipline of describing data formally before storing it. Entities, attributes, relationships, types, and constraints. LinkML as the vehicle: classes, slots, ranges, enums, inheritance, and the distinction between a model and its serializations. Modeling *biological* domains specifically — where the semantics are subtle and the failure modes (silent unit errors, conflated identifiers) are costly. Schema evolution and versioning. Generating artifacts from a model (JSON Schema, SQL DDL, documentation) — the "model once, project many" payoff.

### Unit 2 — Identifiers, ontologies, and semantics (≈1.5 weeks, bio-distinctive)

Why biological data engineering is not generic data engineering. Persistent identifiers, CURIEs/IRIs, namespaces. Controlled vocabularies and ontologies (OBO Foundry, the role of GO, Uberon, MONDO, etc.). Binding schema slots to ontology terms. Semantic versus syntactic correctness. This is where LinkML's enum/ontology features become concrete and where LLM output most needs verification (hallucinated terms, wrong namespaces).

### Unit 3 — Database technologies (≈2.5 weeks)

Matching data shape and access pattern to storage. Relational (normalization, joins, when the relational model fits biological data and when it fights it). Document stores (semi-structured biological metadata, nested records). Graph databases (networks, pathways, ontology relationships, provenance graphs). The deliberate comparison: the same recurring dataset modeled and queried three ways, with tradeoffs made explicit. When *no* database is the right answer and a columnar file (Parquet/Arrow) wins.

### Unit 4 — FAIR principles and data stewardship (≈1.5 weeks)

Findable, Accessible, Interoperable, Reusable — operationalized, not recited. Metadata and data catalogs (the "findable" problem at institutional scale). Accessibility and access protocols. Interoperability through shared vocabularies (ties back to Unit 2). Reusability, licensing, and provenance (ties forward to Unit 5). Assessing real resources against FAIR and proposing remediation.

### Unit 5 — ETL, pipelines, and provenance (≈2.5 weeks)

Moving and transforming data without losing trust in it. Extract/transform/load patterns. Pipelines as DAGs (Snakemake/Nextflow framed as ETL-with-a-graph). Validation as a pipeline stage — syntactic and semantic checks, failing loudly. Idempotency and reproducibility. Data provenance and lineage: recording where data came from and what transformed it, and why that is inseparable from reproducibility.

### Unit 6 — Formats, scale, and access (≈1 week)

The biological format zoo (FASTQ, BAM, VCF, AnnData/h5ad, OME-Zarr) versus general-purpose formats (Parquet, Arrow, HDF5), and why the field fragmented. Storage economics and tiering (object storage, cloud vs. HPC, hot/warm/cold). Serving data: REST/GraphQL basics and consuming public resources (Ensembl, UniProt, GDC) as an engineering rather than analysis task.

### Capstone (runs in parallel, final ≈1 week dedicated)

A self-chosen domain taken end to end: schema → storage → FAIR assessment → validated ETL with provenance → documentation → AI disclosure. The portfolio's centerpiece.

---

## Part 2 — The artifact sequence (assignment scaffolding)

Assessment is a chain of artifacts, not a set of disconnected homeworks. Each builds on the last, and most operate on the **recurring course dataset** so that effort compounds. Every artifact has the same three-part structure, which is what makes grading tractable at scale:

1. **The deliverable** — working code/schema/config (machine-checkable).
2. **The rationale** — a short design-decision document (ADR-style): what you chose, what you rejected, why.
3. **The AI disclosure** — what tools you used, for what, where they were wrong, and how you verified.

### The artifacts

| # | Artifact | Built on | Primary objective |
|---|----------|----------|-------------------|
| A0 | Environment + repo + "hello dataset" exploration | — | Onboarding; studio/Git mechanics; first AI-disclosure practice |
| A1 | Domain schema (LinkML) for the recurring dataset | A0 | LO 1 |
| A2 | Ontology/identifier binding + semantic validation of A1 | A1 | LO 1, partial LO 4 |
| A3 | Three-way storage implementation + comparative analysis | A1 | LO 2 |
| A4 | FAIR assessment + remediation plan for a real resource | — | LO 3 |
| A5 | Validated ETL pipeline (raw → schema-conformant store) | A1–A3 | LO 4 |
| A6 | Provenance/lineage layer over the A5 pipeline | A5 | LO 5 |
| Cap | Capstone: full stack for a self-chosen domain | all | all LOs |

Two recurring meta-artifacts span the whole term and are graded at midpoint and end:

- **AI-use disclosure log** — cumulative, professional-grade documentation of tool use across all artifacts.
- **Failure log** — a running record of where LLMs led the student astray and how it was caught. This is the single most pedagogically valuable artifact for LO 6, and it generates honest data on the tools' real limits.

### Degree-track scaling

Each artifact has a base specification (MS) and a **+critique extension** (PhD). Examples: A1 PhD students additionally evaluate two competing real-world schemas for the domain and justify divergence; A3 PhD students add a literature-grounded argument about storage choices in a published resource; the capstone PhD track requires an under-modeled domain and a defensible novel schema. Same lectures, differentiated depth.

---

## Part 3 — Assessment at scale (50–60 students, limited TA support)

This is the operational crux. The strategy is to make each artifact's three parts graded by the *cheapest reliable mechanism* for that part, reserving scarce human attention for where judgment genuinely matters.

### Principle: tier the grading by what each part needs

**Tier 1 — Automated (the deliverable).** Schemas, validation, ETL outputs, and storage implementations are machine-checkable. Provide an autograder harness in the course repo: schema linting (LinkML's own validators), conformance tests against a held-out slice of the recurring dataset, pipeline smoke tests, and structural checks. Students run it themselves before submitting (formative); CI runs it on submission (summative). This removes the largest, most mechanical grading burden entirely and gives students instant feedback.

**Tier 2 — LLM-assisted first pass (the rationale + disclosure).** The prose components — rationale docs, disclosures — are where an LLM grader, used carefully, scales human judgment rather than replacing it. The approach:

- A **fixed, published rubric** per artifact, the same one given to students.
- An LLM scores each submission against that rubric and produces structured output: a score per criterion *plus a specific justification quoting the student's text*. The justification is non-negotiable — it is what makes the pass auditable.
- The instructor/TA reviews the LLM's output, not the raw submissions, spot-checking and overriding. Reviewing structured, justified assessments is several times faster than grading from scratch.
- **Transparency to students:** they are told exactly that an LLM produces the first-pass score against the shared rubric, that a human reviews it, and that they may contest. This models the same honesty the course demands of them.
- **Consistency safeguards:** same model, same prompt, same rubric, temperature low; calibrate on a handful of instructor-graded exemplars at the start; periodically re-score a sample to check drift.

**Tier 3 — Human (judgment-heavy moments only).** Reserve TA/instructor time for: capstone evaluation, contested grades, the midpoint portfolio review (a single substantive human touchpoint), and flagged edge cases the automated/LLM tiers surface as low-confidence.

### Peer and self-assessment for formative load

Use structured peer review for formative feedback on the rationale docs — students assess two peers against the shared rubric before submission. This is pedagogically valuable (reading others' design decisions teaches design) and offloads formative feedback from staff. Self-assessment against the rubric is a required, graded-for-completion part of each submission.

### Why this is defensible

The arrangement is internally consistent with the course's thesis: it uses automation where output is verifiable, uses LLMs transparently with human oversight and auditable justifications, and concentrates human expertise where genuine judgment is required. It is the same *specify → generate → verify → document* loop the course teaches, applied to grading. And it is honest with students about all of it.

### Operational checklist

- One course repo template, forked per student; CI autograder wired in from A0.
- Rubrics written *before* the semester, published with each assignment, reused by autograder, LLM grader, peer review, and self-assessment alike (write once, use five ways).
- An LLM-grading harness with logged prompts/outputs for auditability and a calibration set of instructor-graded exemplars.
- A defined contest/appeal path.
- The recurring dataset prepared in raw and held-out forms before week 1.

---

## Part 4 — Materials organization strategy

- **Spiral around the recurring dataset.** Each unit revisits it at a higher level (model it → store it → assess it → move it), so abstractions become concrete and artifacts compound.
- **Theory/practice split per unit** is the MS/PhD blend mechanism: shared conceptual segment, shared lab, differentiated assessment depth.
- **Studio over lecture.** In-class building with staff circulating; watching a validation error get debugged beats slides about validation.
- **Capstone as portfolio piece** — the employer-facing artifact, aligned with the course's professional rationale.
- **Version everything in Git** — the course mechanics model the engineering practices being taught.
