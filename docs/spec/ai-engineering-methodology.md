# AI‑Orchestrated Engineering Methodology

Version 1.0

## Purpose

This methodology defines a development model where artificial
intelligence participates actively in the generation of technical
knowledge, while the human engineer directs the thinking, architectural
decisions, and validation.

The objective is to reduce manual documentation work and allow engineers
to focus on: - architecture - analysis - technical decisions - system
supervision

In this model: - AI produces documentation and structured artifacts -
the engineer directs and validates the process

------------------------------------------------------------------------

## Core Principles

### Documentation as the system core

All knowledge about the project lives in:

docs/

This includes architecture, specifications, workflows, prompts and
decisions.

Code is considered a consequence of the documentation.

------------------------------------------------------------------------

### Separation of internal thinking and public documentation

Two levels of documentation exist:

SPEC --- complete technical thinking PUBLIC --- simplified documentation
for developers and stakeholders

SPEC contains: - architecture - analysis - design reasoning -
decisions - feature specifications

PUBLIC contains: - architecture overview - API documentation -
onboarding guides

------------------------------------------------------------------------

### AI as a documentation engine

AI is responsible for:

-   generating documentation
-   structuring specifications
-   maintaining consistency
-   expanding technical descriptions

The engineer focuses on:

-   directing analysis
-   validating outputs
-   making decisions

------------------------------------------------------------------------

### Minimal repository structure

Projects begin with a minimal structure:

project/ docs/ README.md

This avoids premature complexity.

------------------------------------------------------------------------

### Organic repository evolution

Code folders appear only when implementation actually begins.

Example:

Early phase:

project/ docs/

Implementation phase:

project/ docs/ backend/ frontend/

------------------------------------------------------------------------

## Knowledge Structure

docs/

ai/ spec/ public/ lab/

ai -- AI workflows and prompts spec -- full technical specifications
public -- simplified documentation lab -- experiments and research

------------------------------------------------------------------------

## Role of the Engineer

The engineer acts as an orchestra director:

Responsibilities: - guide analysis - validate architecture - approve
decisions - supervise system evolution

AI performs documentation and structural work.

------------------------------------------------------------------------

## Expected Benefits

-   living documentation
-   architectural clarity
-   traceable decisions
-   reduced documentation workload
-   repositories prepared for AI‑assisted development
