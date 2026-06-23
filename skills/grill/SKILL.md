---
name: grill
description: Interview the user relentlesly until aching shared understanding, resolving each branch of the decision tree. Use when user wants to stress-test the plan, get grilled on eir design or mentions "grill".
disable-model-invocation: true
---

# Grill

Interview the user relentlessly about every aspect of the plan until you reach shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one by one.

## Instructions

1. Identify the current plan, proposal, design, or decision being stress-tested.
2. Map the major decision branches and dependencies between them.
3. Ask one focused question at a time, prioritizing the decision that blocks the most downstream choices.
4. If the question can be answered by exploring the codebase, explore the codebase instead.
5. Continue until the design tree is resolved, the assumptions are explicit, and both the user and agent share the same understanding.

## Asking Questions

Use the AskQuestion tool to simplify the process for the user.

For each question:
- Add 2-3 concrete answer options.
- Mark one option as recommended.
- Always include an "Other" option so the user can specify a custom answer.
- Keep the question narrow enough that the answer resolves a real branch of the decision tree.

## Question Style

Be relentless but useful:
- Challenge vague goals, hidden assumptions, missing constraints, risks, ownership boundaries, rollout strategy, test coverage, and failure modes.
- Prefer questions that collapse uncertainty over questions that merely collect preferences.
- Stop only when the remaining decisions are either resolved, explicitly deferred, or no longer relevant.
