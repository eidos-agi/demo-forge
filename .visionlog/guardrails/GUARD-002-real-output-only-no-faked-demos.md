---
id: "GUARD-002"
type: "guardrail"
title: "Real output only — no faked demos"
status: "active"
date: "2026-03-22"
---

## Rule
Every demo must show real output from real code execution. No mocked terminal sessions, no hardcoded output, no screenshots of imaginary interfaces.

## Why
Fake demos are fraud. If the tool can't produce compelling real output, the tool needs work — not a better fake demo.

## Violation Examples
- Hardcoding terminal output in a script instead of running the actual command
- Using a screenshot of a different tool's output
- Mocking API responses that the tool doesn't actually produce
