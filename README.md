# ai-code-prompts

A curated collection of AI prompts designed to enhance collaboration with AI coding assistants. This repository contains structured prompts that guide AI agents to follow best practices in software development.

## Overview

This repository provides reusable prompts that help AI coding assistants work more effectively by:
- **Memory Continuity**: Maintaining project context across sessions through structured documentation
- **Clarifying Requirements**: Ensuring AI agents identify ambiguities and ask relevant questions before starting work
- **Strategic Planning**: Guiding AI to create thoughtful implementation plans with multiple alternatives and clear steps
- **Structured Development**: Promoting a methodical, step-by-step approach to coding tasks
- **Quality Assurance**: Establishing systematic code review and testing standards
- **Sustainable Practices**: Managing dependencies, maintaining compatibility, and following commit conventions

## Table of Contents

### Memory & Context
- [Memory Bank System](./memory-bank/memorybank-rule.md) - Maintain project context across AI sessions
- [Memory Bank Initialization Example](./memory-bank/memorybank-init-prompt.md) - Sample initialization for a project

### Development Workflow
- [Clarification Questions](./clarification/clarification-questions.md)
- [Planning Phase](./planning/planning-phase.md)

### Code Quality
- [Code Review Checklist](./code-review/code-review-checklist.md)
- [Testing Strategy](./testing/testing-strategy.md)

### Project Management
- [Dependency Management](./dependencies/dependency-management.md)
- [Git Commit Conventions](./git/git-commit-conventions.md)
- [Backwards Compatibility](./compatibility/backwards-compatibility.md)

### Agents
Specialized AI agents with defined roles for structured team-based development:
- [Architect](./agents/architect.md) - Requirements gathering, design, and implementation planning
- [Worker](./agents/worker.md) - Code implementation following the architect's plan
- [Code Reviewer](./agents/code-reviewer.md) - Code review against target branch

### Skills
Reusable orchestration prompts that coordinate agents and workflows:
- [Feature Team Orchestration](./skills/feature-team-orchestration/SKILL.md) - End-to-end feature delivery using the architect → worker → code-reviewer pipeline

## Usage

Each prompt file can be used as a rule for AI tool of you choice (Cursor, Claude Code, Github Copilot etc.) or directly shared with your AI coding assistant to establish consistent behavior patterns across your development sessions.
