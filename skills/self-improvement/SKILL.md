---
name: self-improvement
description: Use to reflect on completed tasks, record lessons learned, and consult past lessons to optimize future performance.
---

# Self-Improvement Skill

This skill enables the agent to continuously improve by reflecting on past actions and consulting a knowledge base of learned lessons.

## When to Use

- **Reflection**: AFTER completing a complex task, achieving a milestone, or encountering a significant failure.
- **Consultation**: BEFORE starting a complex task to avoid repeating past mistakes.

## Modes

### 1. Reflection Mode

**Goal**: Analyze a recent interaction to identify what went well and what didn't.

**Steps**:

1.  **Analyze**: Review the recent task execution (Task history, artifacts created).
2.  **Identify**: Find one or two specific, actionable lessons.
    - _Good_: "Always check if a directory exists before creating it."
    - _Bad_: "Be better at coding."
3.  **Record**: Append the lesson to the `lessons_learned.md` reference file.

### 2. Consultation Mode

**Goal**: Prime the agent with relevant past wisdom.

**Steps**:

1.  **Read**: Read the `lessons_learned.md` file.
2.  **Apply**: specific lessons that are relevant to the current task.

## Resources

- [lessons_learned.md](references/lessons_learned.md): Storage for all recorded lessons.
