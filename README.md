# agent-safety-field-guide

[![Awesome](https://awesome.re/badge.svg)](https://awesome.re)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Payout Rail](https://img.shields.io/badge/payout-USDC%20on%20Base-blue)](https://basescan.org)
[![Commercial Catalog](https://img.shields.io/badge/catalog-45%20Verified%20Tools-success)](https://github.com/genesiscode2026/genesis-software-catalog)

> **Curated operational checklist, failure mode taxonomy, and sandbox architectural patterns for autonomous AI coding agents.**

---

## Executive Summary

Autonomous coding agents (Claude Code, Antigravity, OpenDevin, Cursor) possess execution agency: reading files, editing source code, executing shell commands, and driving Git workflows. Without rigid boundaries, agents cause workspace contamination, accidental secret exposure, and unapproved repository mutations.

This guide provides open, production-tested guardrail specifications and reference checklists for engineering teams deploying agentic software workflows.

---

## 1. Core Safety Principles

- **Fail-Closed Execution**: If environmental state, auth boundaries, or tool invariants cannot be established, halt execution immediately.
- **Strict Boundary Enforcement**: Enforce mandatory path scoping to the designated workspace root (`Cwd`). Reject paths outside workspace.
- **Zero Destructive Auto-Commands**: Explicitly forbid automated execution of `git reset --hard`, `git clean -fd`, `rm -rf`, `sudo`, or history rewrites without explicit interactive confirmation.
- **Credential Hygiene**: Prevent agents from accessing system keychains, reading `.env` secrets, or exporting sensitive auth material.

---

## 2. Guardrail Checklist & Failure Modes

| ID | Failure Mode | Severity | Recommended Guardrail |
|---|---|---|---|
| **SAF-01** | Destructive Git Wipe (`git reset --hard`) | CRITICAL | Git wrapper interceptor rejecting destructive subcommands |
| **SAF-02** | Workspace Boundary Escape (`../../`) | CRITICAL | Filesystem chroot / canonical path validator |
| **SAF-03** | Secret Exfiltration via Tool Returns | HIGH | Regex scrubber for API keys, private keys, seed phrases |
| **SAF-04** | Contradictory Instruction Drift | HIGH | Static cross-linter for `AGENTS.md` and `CLAUDE.md` |
| **SAF-05** | Cascading Autonomous Loops | MEDIUM | Max-step circuit breakers and rate limiters |

---

## 3. Sample Verification Output

Below is an authentic execution trace from a preflight guardrail run verifying agent workspace isolation:

```text
============================================================
   AGENT WORKSPACE PREFLIGHT & INTEGRITY CHECK (v1.0.0)
============================================================
[AUDIT] Target Workspace: /workspace/project-alpha
[CHECK 01] Path traversal attempt (../../etc/passwd) ...... [BLOCKED]
[CHECK 02] Shell injection probe (; rm -rf /) ............. [BLOCKED]
[CHECK 03] Git branch protection (main lock) .............. [ENFORCED]
[CHECK 04] Secret exposure scan (0 unmasked tokens) ....... [PASS]
[CHECK 05] Destructive command blacklist (5/5 active) ...... [PASS]
------------------------------------------------------------
RESULT: PASS (Workspace isolation verified. Execution safe.)
============================================================
```

---

## 4. Production Tooling & Commercial Catalog

For engineering teams seeking automated CI/CD integration, deterministic pre-commit hooks, and enterprise hardening:

### Low-Friction Entry Tools ($19)
- **[Agent Workspace Preflight](https://gitbuyer.com/r/genesiscode2026/genesis-agent-workspace-preflight)** ($19) — [GitBuyer](https://gitbuyer.com/r/genesiscode2026/genesis-agent-workspace-preflight) | [X402 Git](https://x402git.com/genesiscode2026/genesis-agent-workspace-preflight)
- **[Agent Instruction Linter](https://gitbuyer.com/r/genesiscode2026/genesis-agent-instruction-linter)** ($19) — [GitBuyer](https://gitbuyer.com/r/genesiscode2026/genesis-agent-instruction-linter) | [X402 Git](https://x402git.com/genesiscode2026/genesis-agent-instruction-linter)
- **[Agent Checkpoint & Resume](https://gitbuyer.com/r/genesiscode2026/genesis-agent-checkpoint-resume)** ($19) — [GitBuyer](https://gitbuyer.com/r/genesiscode2026/genesis-agent-checkpoint-resume) | [X402 Git](https://x402git.com/genesiscode2026/genesis-agent-checkpoint-resume)

### Enterprise Core Suites
- **[Safe Agent Engineering Suite](https://gitbuyer.com/r/genesiscode2026/safe-agent-engineering-suite)** ($199) — [GitBuyer Checkout](https://gitbuyer.com/r/genesiscode2026/safe-agent-engineering-suite) | [X402 Git Checkout](https://x402git.com/genesiscode2026/safe-agent-engineering-suite)
- **[Agent Operations Control Room SDK](https://gitbuyer.com/r/genesiscode2026/agent-operations-control-room-sdk)** ($149) — [GitBuyer Checkout](https://gitbuyer.com/r/genesiscode2026/agent-operations-control-room-sdk) | [X402 Git Checkout](https://x402git.com/genesiscode2026/agent-operations-control-room-sdk)
- **[MCP Agent Security Gateway](https://gitbuyer.com/r/genesiscode2026/mcp-agent-security-gateway)** ($149) — [GitBuyer Checkout](https://gitbuyer.com/r/genesiscode2026/mcp-agent-security-gateway) | [X402 Git Checkout](https://x402git.com/genesiscode2026/mcp-agent-security-gateway)

Browse the full [GENESIS Multi-Channel Software Catalog](https://github.com/genesiscode2026/genesis-software-catalog) for 45 verified agent engineering and quant tools.
