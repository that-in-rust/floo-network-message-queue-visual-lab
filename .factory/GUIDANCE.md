# Factory Guidance: floo-network-message-queue-visual-lab

Project context for AI assistants working on this repository.

---

## Project Purpose

A visual lab for understanding message queue internals, starting with Apache Iggy.

**Core thesis:** Message queues are invisible by default. This lab makes them visible.

**v0.1 scope:** One broker (Iggy), one message, one trace, one visualization.

---

## Target User

**PRIMARY:** Engineers evaluating or adopting Apache Iggy — they need to understand what happens when they send a message.

**SECONDARY:** Contributors — they benefit from the visualization but are NOT the primary audience.

The backlog and product decisions should optimize for the adopter, not the contributor. If a feature helps contributors but doesn't help adopters understand Iggy, it's out of scope.

---

## Key Constraints

1. **Rust backend only** - Backend services must be implemented in Rust
2. **Popular connector first** - First connector story should be production-relevant (PostgreSQL, not demo connectors)
3. **Narrow scope** - Resist scope creep. v0.1 is intentionally minimal.

---

## Related Files

| File | Purpose |
|------|---------|
| `PRD/PRD-v001.md` | Product requirements and executable specifications |
| `backlog-202603.md` | Shreyas Doshi level product insights |

---

## Background Context

This project serves dual purposes:
1. **Public:** Educational resource for understanding message queue internals
2. **Private:** Learning vehicle for understanding distributed systems deeply

The visualizer cannot be built without understanding the internals. This is the design constraint that forces deep learning.

---

## Repository Naming

`floo-network` references Harry Potter's magical transportation network - invisible infrastructure that wizards use daily without understanding how it works. The metaphor: message queues are the floo network of distributed systems.

---

*Last updated: 2026-03-10*
