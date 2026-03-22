---
id: "GUARD-001"
type: "guardrail"
title: "No software — skills and templates only"
status: "active"
date: "2026-03-22"
---

## Rule
Same as foss-forge: demo-forge is skills + templates, not installable software.

## Why
Consistency across the forge ecosystem. Skills evolve with the agent. Software requires maintenance.

## Violation Examples
- Adding pyproject.toml with a build system
- Writing a CLI that needs to be installed
- Publishing to PyPI
