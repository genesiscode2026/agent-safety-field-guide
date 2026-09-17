# agent-safety-field-guide

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> A curated list of production guardrails, failure modes, sandbox architectures, and security benchmarks for autonomous AI coding agents.

---

## Contents
- [Core Safety Principles](#core-safety-principles)
- [Filesystem & Git Guardrails](#filesystem--git-guardrails)
- [Tool-Calling Security](#tool-calling-security)
- [Prompt Injection & Memory Hygiene](#prompt-injection--memory-hygiene)
- [Commercial & Enterprise Solutions](#commercial--enterprise-solutions)

---

## Core Safety Principles

- **Fail-Closed Execution**: If agent state or security assumptions cannot be established, halt immediately.
- **Strict Boundary Enforcement**: Never grant autonomous agents write access outside the active workspace directory.
- **Zero Destructive Auto-Commands**: Explicitly forbid `git reset --hard`, `git clean -fd`, and `rm -rf` without human confirmation.

## Filesystem & Git Guardrails

- [Safe Agent Engineering Suite](https://gitbuyer.com/r/genesiscode2026/safe-agent-engineering-suite): Deterministic guardrails preventing unapproved git pushes and wiped working directories.
- [Agent Instruction Linter](https://gitbuyer.com/r/genesiscode2026/genesis-agent-instruction-linter): Static detector for contradictory policies across `AGENTS.md` and `CLAUDE.md`.
- [Coding Agent Checkpoint & Resume](https://gitbuyer.com/r/genesiscode2026/genesis-agent-checkpoint-resume): State freezer and instant resume runbook generator.

## Tool-Calling Security

- [MCP Agent Security Gateway](https://gitbuyer.com/r/genesiscode2026/mcp-agent-security-gateway): Zero-trust firewall for Model Context Protocol tools.
- [Tool-Call Contract Validator](https://gitbuyer.com/r/genesiscode2026/tool-call-contract-validator): Ahead-of-time parameter verification for LLM function calling.

## Commercial & Enterprise Solutions

For production-grade hardening, automated testing, and CI verification, see the complete [GENESIS Agent Tooling Catalog](https://gitbuyer.com/r/genesiscode2026).
