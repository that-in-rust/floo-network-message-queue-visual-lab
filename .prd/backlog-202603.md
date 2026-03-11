# Backlog: Shreyas Doshi Level Insights

Document capturing product insights, user pain points, and strategic ideas for `floo-network-message-queue-visual-lab`.

---

## User Pain Points (from Apache Iggy Discord)

**Target: Engineers evaluating message queues for their organizations.**

| Use Case | Pain Point | Lab Opportunity |
|------|------------|-----------------|
| Rust trading terminal, backend→client streaming | "Still exploring" - discovery friction | Visual "does it fit?" decision in 30s |
| Audit trail for user CRUD actions | "CQRS is too complicated" - pattern complexity | Show data flow, not pattern names |
| Potential adopter | "Just discovered Iggy" - first touchpoint is blog | Interactive blog post (the lab itself) |
| Evaluating Iggy vs Kafka | "Kafka compatibility?" - wants migration story | Side-by-side interface comparison |

### Insight: The "Still Exploring" Problem
Users land on Iggy and spend days "exploring" before they can make a decision. A visual lab that shows ONE complete message journey in 30 seconds accelerates the "does this fit my use case?" decision by 100x.

### Insight: Pattern Fatigue
Developers don't want CQRS, event sourcing, or CDC as abstract concepts. They want to see data flow. The lab should never say "this demonstrates CQRS" — it should show data moving and let the pattern emerge from observation.

### Insight: The Kafka Question Is the FAQ
Kafka compatibility keeps coming up because users want migration safety.

The answer (no protocol compat, easy interface migration) is correct but invisible. A visual lab that shows "Same task: Iggy vs Kafka interface" answers the question in 30 seconds without docs.

### Insight: Blog Posts Are the Funnel
First touchpoint is content, not code. The visual lab is essentially an interactive blog post. It should feel like reading a great technical essay, but with "run it yourself" buttons.

---

## Strategic Insights

### Insight: Adopters First, Contributors Second
The primary user is the engineer evaluating Iggy for their use case. Contributors are a side benefit.

If the visualization helps someone decide "Iggy fits my use case", that's the win. If it happens to also help a contributor understand the codebase, that's bonus — not the goal.

**Shreyas Doshi principle:** Solve the user's problem, not the contributor's problem. Contributors are users of the codebase. Adopters are users of the product.

### Insight: Nobody Owns "Explainer" Position in Rust MQ Space
In Apache Iggy ecosystem:
- Core contributors understand internals deeply
- Users just want connectors working
- **Gap: No one makes internals accessible visually**

This is a defensible niche. Not "most PRs" but "best explainer."

### Insight: Visualization Forces Understanding
You cannot build a message journey tracer without understanding:
- Partition assignment code
- Segment storage format
- Index structure
- Consumer offset management
- Transport layers (TCP/QUIC)

The project is a learning vehicle disguised as a teaching tool.

---

## Product Ideas

### P1: Message Journey Tracer (Core Innovation)
A Rust tool that instruments Iggy to emit trace events:

```
t=0ms    Producer sends (2KB payload)
t=2ms    Server receives → stream:orders, topic:new
t=3ms    Assigned to partition 3
t=4ms    Appended to segment file (offset: 10,042)
t=4ms    Index updated
t=15ms   Consumer "checkout-service" polls
t=16ms   Offset committed to disk
```

**Why this matters:** You can't fake this. Building it forces deep codebase understanding.

### P2: Side-by-Side Broker Comparison
Same message, different brokers, rendered in parallel:

| Iggy | Kafka |
|------|-------|
| QUIC transport | TCP |
| io_uring I/O | epoll |
| Single binary | Zookeeper + brokers |

**Why this matters:** "Why Iggy over Kafka?" is the #1 question. Answer visually, not with docs.

### P3: Failure Mode Visualization
What happens when:
- Consumer dies mid-poll?
- Partition rebalance occurs?
- Backpressure builds?

**Why this matters:** Production debugging. Users don't understand failure modes until they see them.

### P4: Connector Journey Visualization
Postgres CDC → Iggy → Sink

Show the full connector path, not just broker internals.

**Why this matters:** Connectors are how real users interact with MQs. Pure broker visualization is academic; connector visualization is practical.

### P5: Kafka Migration Guide (Interactive)
Show the same task (produce, consume, offset commit) in Iggy vs Kafka side by side.

**Why this matters:** This is the #1 FAQ. Answer it visually. "Iggy doesn't support Kafka protocol, but here's what migration looks like."

---

## Content Ideas (Web Pages + Visualizations)

### Page: Message Journey
Interactive visualization of one message flowing through Iggy in slow motion — every step rendered, visible in your browser.

- Watch it flow through partition assignment, storage, consumer poll
- Every step shown as a badge with details like "partition", "offset", "index updated"

### Page: Side-by-Side Comparison
Compare Iggy vs Kafka on the same message, rendered in parallel.

- See what happens differently
- Decide "Iggy or Kafka?" faster than reading docs

### Page: Connector Journey
Postgres CDC → Iggy → Sink (animated)

- Show the full connector path, not just broker internals
- Connectors are how real users interact with MQs

### Page: Failure Modes Lab
Interactive scenarios: backpressure, replay, partition rebalance

- See what happens when things go wrong
- Build production confidence

### Page: Decision Tree
"When to use which" — visual guide for choosing between Iggy, Kafka, and other brokers

---

## Naming Insights

### Current: `floo-network-message-queue-visual-lab`

**Pros:** Harry Potter theme, "lab" suggests experimentation
**Cons:** Long, doesn't convey "fieldbook" or "guide" aspect

### Alternatives:
- **Message Queue Fieldbook** (like a naturalist's field guide)
- **MQ Observatory** (watching things happen)
- **Iggy Explorer** (tool-specific, narrower)

### Insight: Name Should Promise Transformation
Not "learn about message queues" but "see what you couldn't see before."

---

## What We're NOT Building (v0.1)

These are out of scope for v0.1:

- Contributor onboarding / codebase maps
- Interview prep mode
- Connector coverage gap analysis
- SDK documentation
- Architecture deep-dives (io_uring, compio migration)

---

## Open Questions for Future Insights

1. Should v0.1 trace Source→Iggy or Iggy→Sink? (Different learning stories)
2. CDC vs polling for Postgres connector? (Complexity tradeoff)
3. Connector-only events vs connector + storage events? (Scope boundary)
4. Should the lab be embeddable in Iggy docs? (Partnership opportunity)

---

## Meta: What Makes an Insight "Shreyas Doshi Level"?

1. **Counterintuitive** — goes against common wisdom
2. **Simply stated** — one sentence, no jargon
3. **Deeply true** — reveals something fundamental
4. **Actionable** — changes what you build or how

Add to this document when you find them.

---

*Last updated: 2026-03-10*
