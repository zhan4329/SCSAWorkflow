---
name: plan-update-bojohn
description: Update existing plan.md files safely and consistently. Use when users ask to revise tasks, decisions, checkboxes, Issues sections, or policy/governance text in project plans while preserving unrelated history.
author: Boqian Zhang
version: 2026.4.15
---

# Plan Update Policy

Apply this skill when editing an existing plan document so updates stay minimal, traceable, and status-accurate.

## Core Rules

- Edit only sections touched by the user request.
- Preserve unrelated content and historical checked items.
- Removing an item from Issues requires a recorded outcome: promote to a task, explicitly abandon, or convert to a rule/policy.
- Keep checkbox truth strict: mark done only after implementation/tests are completed.
- Keep tasks scoped: split a task if it mixes independent workstreams.
- Keep action items executable and outcome-focused.
- Avoid passive action items such as "keep ..." as standalone tasks.
- Keep action wording concise and positive; avoid unnecessary negative caveats in task bullets.

## Update Workflow

1. Read only the relevant sections first:
   - Immediate Next Step
   - Progress (Addressed/Ongoing/Remaining)
   - Issues
   - Development Details for affected tasks
   - Decision Log
   - Notes/Policies sections
2. Classify each requested change:
   - Decision update
   - Task status update
   - Task scope/structure update
   - Policy update
3. Apply minimal edits:
   - Remove resolved Issues items (or resolved sub-parts only)
   - Record where each removed Issues item went (task, abandon, or rule/policy).
   - Mirror final decisions in both Decision Log and affected task action items
   - Keep numbering coherent after inserts/removals
4. Validate consistency:
   - No task says Done while implementation action items remain unchecked
   - Immediate Next Step references existing task numbers
   - Action items reflect task title scope

## Preferred Patterns

- If a decision affects multiple concerns, keep one concise decision-log entry and update task action items where execution happens.
- If one task title no longer matches its actions, rename or split the task.
- If a policy is requested, add a dedicated policy section rather than scattering one-off lines.
- If guidance is a general recurring rule (not PR-specific), document it in Notes/Policies, not as a standalone Decision Log entry.

## Anti-Patterns

- Deleting checked historical records without factual correction
- Converting decisions into vague action items
- Duplicating the same requirement in many sections
- Expanding plan scope beyond the active PR focus

## Output Standard

When summarizing your update, report:

1. Sections changed
2. Why each change was necessary
3. What was intentionally left untouched
