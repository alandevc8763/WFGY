<!--
AI_NOTE_START

Document role:
This file defines the stable routing and output field conventions used across the official flagship demo pack.

How to use this file:
1. Read this file before creating a new official demo notebook or editing an existing one.
2. Use this file to keep field names, route summaries, and replay outputs aligned across demos.
3. Treat this file as the shared schema guide for the official flagship demo pack.
4. Read together with:
   - [Flagship Runnable Demo Pack](../README.md)
   - [Shared Demo Helpers](./README.md)

What this file is:
- The schema guide for official demo JSON files
- The naming guide for common route fields
- The alignment layer for replay-first notebook outputs

What this file is not:
- Not a strict production API contract
- Not the atlas core ontology
- Not a replacement for per-demo README explanations
- Not a promise that every field will be identical across every future community demo

Reading discipline for AI:
- Preserve the difference between stable shared fields and demo-specific extensions.
- Do not over-normalize away the teaching purpose of each demo.
- Keep route fields consistent, but allow case-specific content where needed.

AI_NOTE_END
-->

# Routing Schema v1

## Problem Map 3.0 Troubleshooting Atlas
## Shared field conventions for official flagship demos

This document defines the stable routing and output field conventions used across the **official flagship demo pack**.

Its purpose is simple:

> keep the demo notebooks aligned  
> keep JSON fixtures readable  
> keep replay outputs comparable across demos

This is not meant to be a giant formal spec.
It is a practical schema guide for the first official MVP demo pack.

---

## 1. Scope

This schema applies to the official flagship demos under:

- `demo-f1-grounding-anchor`
- `demo-f5-observability-first`
- `demo-f4-execution-closure`
- `demo-f7-container-fidelity`

It focuses on the three common JSON files used across those demos:

- `input_case.json`
- `replay_outputs.json`
- `expected_output.json`

It also defines the shared route-summary fields that may be rendered in notebooks or README explanations.

---

## 2. Design rule

The official demos are **aligned**, but not artificially flattened.

That means:

- the same core route fields should stay stable
- the same file roles should stay stable
- replay outputs should look structurally familiar across demos

But also:

- each demo may include case-specific fields
- each demo may have its own teaching emphasis
- not every replay output must use identical secondary keys

In short:

> keep the shared spine stable  
> allow the teaching layer to stay local

---

## 3. Common file roles

### `input_case.json`

Purpose:

- define the case
- define the target route
- define the main teaching context
- provide the notebook with the minimum case bundle

### `replay_outputs.json`

Purpose:

- define the baseline state
- define the repaired or improved state
- define the before / after teaching contrast
- support replay-first inspection

### `expected_output.json`

Purpose:

- define the clean target structure
- define the expected routing result
- define the minimum success contract for the demo

---

## 4. Stable shared fields in `input_case.json`

The following fields are recommended as the stable shared layer.

### Required top-level fields

- `demo_id`
- `demo_version`
- `case_id`
- `title`
- `task_type`
- `family_target`
- `user_question`

### Required shared sub-object

#### `family_target`

Recommended stable fields:

- `primary_family`
- `secondary_family`
- `best_current_fit`
- `broken_invariant`

These four fields form the official shared route spine.

### Example shared structure

```json
{
  "demo_id": "demo_f5_observability_first",
  "demo_version": "v1",
  "case_id": "f5_observability_case_001",
  "title": "Workflow failure with too little visibility for safe diagnosis",
  "task_type": "workflow_debugging",
  "family_target": {
    "primary_family": "F5",
    "secondary_family": "F4",
    "best_current_fit": "F5_N01 Failure Path Opacity",
    "broken_invariant": "failure_path_visibility_broken"
  },
  "user_question": "Why is the workflow returning irrelevant answers, and what should be fixed first?"
}
