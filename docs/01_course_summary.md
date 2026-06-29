# Biological Data Engineering

**Proposed graduate course — BU Bioinformatics MS Program**
*4 credit hours · 13 weeks · MS and PhD students*

---

## One-line description

The infrastructure half of bioinformatics: how to model, store, validate, move, and steward biological data so that downstream analysis is reproducible, trustworthy, and reusable at scale.

## Rationale

Most bioinformatics training emphasizes *analysis* — statistics, algorithms, methods — and treats the data itself as a given. In practice, the dominant bottleneck in modern biology is not the analysis but the data infrastructure underneath it: schemas that drift, identifiers that don't resolve, pipelines that can't be rerun, and metadata that makes datasets impossible to find or reuse. This course addresses that gap directly. It treats data engineering as a first-class discipline and equips students to build the systems that make biological data scientifically dependable.

A second motivation is professional. Infrastructure- and software-oriented roles in biological research — data architects, pipeline engineers, schema and standards developers, research-software engineers — are growing and chronically undertrained for. This course is explicitly designed to produce a portfolio that demonstrates those competencies.

## Central thesis

*The credibility of a biological result is inherited from the engineering of the data it rests on.* Every topic in the course is framed as an answer to a single question: **how do we make biological data findable, trustworthy, and reusable?**

## What makes this course distinctive

- **Bio-specific, not generic data engineering.** The course centers the things that make biological data unique and hard: ontologies and controlled vocabularies, persistent identifiers, the format zoo (FASTQ/BAM/VCF/AnnData), provenance, and domain semantics — not just "here is SQL."
- **Studio model.** Given an audience that already programs, class time is spent building, not lecturing. Students produce working artifacts every week.
- **LLM usage as a transparent, assessed core skill.** Large language models are now part of the engineering toolchain. Rather than ignore or prohibit them, the course teaches the professional workflow — *specify, generate, verify, document* — and treats critical evaluation of model output as the central assessable competency.
- **Portfolio assessment.** There is no terminal exam. Students are assessed on a sequence of engineering artifacts that accumulate into a coherent, employer-facing portfolio.

## Audience and prerequisites

MS and PhD students in Bioinformatics with at least some programming experience (comfortable writing scripts, using the command line, and reading code). No prior database or data-engineering coursework assumed. The course blends theory and practice so that it serves both degree tracks; differentiation is handled through assessment depth (see below), not separate sections.

## Format

- **Studio-centered.** Each unit pairs a short conceptual segment (concepts, readings, discussion) with an extended hands-on build segment.
- **One recurring dataset.** A single messy, real (de-identified) biological dataset threads through the whole semester — students model it, store it, assess its FAIRness, and build ETL for it across successive weeks, so principles compound rather than reset.
- **Everything in version control.** Course materials and student work all live in Git, so the mechanics of the course model the practices being taught.

## Assessment philosophy

Assessment is **by artifact**, accumulating into a portfolio. Each artifact bundles a working deliverable, a short design-rationale document, and an AI-use disclosure. Because the course is large (50–60 students) with limited TA support, assessment is engineered for scalability: rubric-driven, automatable where possible, peer- and self-assessment for formative feedback, and LLM-assisted for consistent first-pass evaluation under instructor oversight (detailed in the outline document). The disclosure and critical-evaluation components are themselves graded — students are rewarded for using AI tools well and transparently, not penalized for using them.

## Degree-track differentiation

The same lectures and labs serve both tracks. MS students are assessed on building correctly; PhD students take on an additional critique/justification layer per unit — evaluating competing standards, engaging the primary literature, and arguing about what "correct" means in an under-modeled domain. The capstone scales accordingly.

## Learning objectives

By the end of the course, a student can:

1. Model a biological domain as a formal schema, justifying class, slot, and type decisions and binding to appropriate ontologies and identifier systems.
2. Select an appropriate database technology (relational, document, graph) for a given biological data shape and access pattern, and articulate the tradeoffs.
3. Evaluate a dataset or resource against the FAIR principles and propose concrete, prioritized remediations.
4. Design and implement an ETL pipeline that ingests messy real-world biological data into a validated, queryable store.
5. Reason about data provenance and implement lineage tracking for a transformation workflow.
6. Use LLM-based tools to accelerate engineering work while critically evaluating and verifying their output, and document that use transparently and professionally.
7. Communicate data-engineering design decisions through architecture documentation (ADRs, schema docs, READMEs).

PhD-track objective (additional): critically evaluate competing data-modeling standards within a biological subfield and propose a defensible schema for an under-modeled domain.

## Deliverables produced (student portfolio)

By semester's end each student holds a version-controlled portfolio containing: a domain schema with ontology bindings; a comparative storage analysis with working implementations; a FAIR assessment and remediation plan; a complete, validated ETL pipeline with provenance tracking; an AI-use disclosure log and failure log; and a capstone project integrating all of the above for a domain of their choice.
