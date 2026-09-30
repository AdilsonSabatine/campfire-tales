# Architecture Decision Records

This directory contains records of significant architectural and technical decisions made during the development of Campfire Tales.

Each decision should document the context, the alternatives considered, and the rationale behind the chosen approach.

## Purpose

Architecture Decision Records (ADRs) provide a historical record of why important decisions were made.

They should help contributors understand:

* The context in which a decision was made.
* The problem the decision addressed.
* The alternatives that were considered.
* The consequences of the decision.
* Whether the decision is still valid.

## Format

Each decision should be stored in a separate Markdown file using the following naming convention:

```text
NNNN-short-description.md
```

Where `NNNN` is a sequential number.

For example:

```text
0001-example-decision.md
0002-another-decision.md
```

## Status

An ADR may have one of the following statuses:

* **Proposed** — the decision is being discussed and has not been finalized.
* **Accepted** — the decision has been approved and is currently applicable.
* **Superseded** — the decision was replaced by a later decision.
* **Deprecated** — the decision is no longer applicable.

## Guidelines

Create an ADR when a decision:

* Has meaningful architectural consequences.
* Is difficult or costly to reverse.
* Involves significant trade-offs.
* Establishes a convention that affects future development.

Avoid creating ADRs for routine implementation details or decisions that are trivial to change.

ADRs should describe the decision and its context rather than prescribe every implementation detail.
