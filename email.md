# Email as Infrastructure: Taxonomy, Planes, and Strategy

This document treats email as infrastructure rather than correspondence. It assumes an environment with many domains, heavy use of shared and operational addresses, system-generated mail, and customer-facing project domains. The purpose is to describe the problem space precisely, derive the architectural decomposition that the problem forces, enumerate the solution classes that exist in practice, and arrive at a recommendation that follows mechanically from those premises.

The claim is not that email is complicated. The claim is that once email is used beyond person-to-person communication, its behavior becomes structured, enumerable, and constrained. When those constraints are made explicit, the architecture stops being a matter of taste.

## Taxonomy of Email Use Cases

In a domain-rich environment, email behavior is enumerable. The following taxonomy describes the **complete and closed** set of routing and lifecycle behaviors the system must support. These are problem descriptions only, independent of implementation. Any real-world email behavior can be expressed as one or more of these use cases, possibly composed with temporal or conditional routing.

1. [One-to-one correspondence](#one-to-one-correspondence)
2. [One-to-many distribution](#one-to-many-distribution)
3. [Many-to-one aggregation](#many-to-one-aggregation)
4. [Many-to-many routing](#many-to-many-routing)
5. [Zero-consumer acceptance](#zero-consumer-acceptance)
6. [Zero-sender validity](#zero-sender-validity)
7. [Temporal routing](#temporal-routing)
8. [Conditional routing](#conditional-routing)
9. [Journaling and shadow consumption](#journaling-and-shadow-consumption)
10. [Address-as-capability](#address-as-capability)

### One-to-one correspondence

A single human sender communicates directly with a single human recipient. Both addresses are treated as identities, and the message is conversational in nature.

alice@domain.com → bob@domain.com

### One-to-many distribution

A single sender writes to an address that intentionally fans out to multiple recipients. The address represents a role or audience rather than an individual, and recipient membership is expected to change over time.

alice@domain.com → ops@domain.com → bob@domain.com, joe@domain.com

### Many-to-one aggregation

Multiple senders converge on a single address that exists to collect signals rather than to represent ownership. The value of the address lies in consolidation.

alice@domain.com → support@project.domain  
bob@external.com → support@project.domain  
monitor@system.domain → support@project.domain

### Many-to-many routing

Multiple senders emit mail to an address that fans out to multiple consumers. Neither side of the routing relationship is stable, and both may include humans and systems.

alice@domain.com → ops@project.domain → bob@domain.com, joe@domain.com  
deploy@system.domain → ops@project.domain → bob@domain.com, incident-log@system.domain

### Zero-consumer acceptance

Mail is accepted and authenticated but not delivered to any active consumer. Acceptance itself is the signal.

probe@external.domain → sink@domain.com → ∅  
verification@partner.domain → trap@domain.com → ∅

### Zero-sender validity

An address is valid as a sender identity but must never accept inbound mail. Any attempt to deliver to it is invalid by definition.

noreply@domain.com → alice@external.com  
alice@external.com → noreply@domain.com → rejected

### Temporal routing

The address is stable, but the recipient set changes over time according to schedules or phases.

alice@domain.com → oncall@infra.domain → bob@domain.com   (week 1)  
alice@domain.com → oncall@infra.domain → joe@domain.com   (week 2)

### Conditional routing

Delivery depends on message attributes rather than address alone.

monitor@system.domain → alerts@infra.domain → log@system.domain  
monitor@system.domain → alerts@infra.domain → bob@domain.com, pager@system.domain

### Journaling and shadow consumption

Messages are delivered to their primary recipients while also being copied to secondary consumers for audit or analysis.

alice@domain.com → bob@domain.com  
alice@domain.com → audit@system.domain

### Address-as-capability

Sending to the address triggers an action rather than a conversation.

alice@domain.com → create-ticket@project.domain → ticketing-system  
deploy@system.domain → promote@env.domain → release-pipeline

## Architectural Decomposition

Once the taxonomy is stated, a separation of responsibilities follows inevitably. The use cases differ not just in frequency, but in how they scale and what constitutes failure. Collapsing these concerns into a single system forces incompatible assumptions to coexist.

From the taxonomy, email responsibilities separate into three planes.

The **Human Consumption Plane** exists to serve people. It optimizes for continuity, state, search, threading, and low cognitive overhead. Its scale factor is headcount, not domain count.

The **Routing and Distribution Plane** exists to move messages between senders and consumers without implying identity. It optimizes for fan-in, fan-out, and cheap change. Its scale factor is the number of domains and addresses.

The **Sending Authority Plane** exists to assert identity outward. It optimizes for authentication correctness, reputation isolation, and explicit control over which domains may emit mail.

These planes are orthogonal. A single tool can approximate more than one plane, but cannot optimize for all three without accumulating coupling.

## Potential Solutions

This section describes the major classes of email solutions commonly used in practice. Each solution type is evaluated only in terms of which planes it natively covers.

Before mapping solution types to planes, it is useful to describe what each solution class is actually designed to do. These categories reflect the dominant abstraction each class optimizes for. They are not mutually exclusive in implementation, but they are mutually exclusive in intent.

A **user-centric email solution** is designed around people as the primary abstraction. An email address is an attribute of a user, and the inbox is the organizing surface. Most functionality assumes long-lived identities, relatively stable domains, and primarily conversational traffic. Distribution lists and shared inboxes are typically layered on top of the user model as administrative constructs. This class is optimized for organizational communication where email closely tracks the org chart.

An **inbox-centric email solution** is still focused on human consumption, but it decouples the inbox experience from broader collaboration and directory concerns. The inbox remains the core abstraction, but users may operate across many domains and aliases. These systems emphasize fast, reliable mail delivery, strong filtering, and flexible aliasing, while remaining opinionated about inboxes as the natural sinks for mail. They assume that most important messages ultimately terminate in a human inbox.

An **alias-centric routing solution** treats email addresses and domains as routing nodes rather than identities. The core abstraction is the mapping between addresses and destinations, with fan-in, fan-out, and indirection treated as first-class operations. Many addresses are expected to be shared, disposable, or non-human. These systems are designed for address lifecycle management and routing correctness, not for inbox ergonomics or user identity.

A **transactional email solution** is designed for outbound mail emitted by systems rather than people. Its core responsibility is to assert sending authority correctly and reliably on behalf of a domain. These systems focus on authentication, deliverability, reputation isolation, and volume handling. They do not attempt to model inboxes or inbound routing and treat email purely as a transport for system-generated messages.

The table below maps these solution classes to the responsibility planes they natively cover.

### Solution Space by Plane Coverage

| Solution Type                                                  | Consumption | Distribution | Authority |
|----------------------------------------------------------------|:-----------:|:------------:|:---------:|
| User-centric email suites<br>(Google Workspace, Microsoft 365) |      Y      |      N       |     N     |
| Inbox-centric hosted email<br>(Fastmail)                       |      Y      |      N       |     N     |
| Alias-centric routing services<br>(ForwardEmail)               |      N      |      Y       |     N     |
| Transactional email services<br>(AWS SES, SendGrid, Postmark)  |      N      |      N       |     Y     |
| Self-hosted mail infrastructure<br>                            |      Y      |      Y       |     Y     |

## Reduction of the Solution Space

Once plane coverage is explicit, the space of viable architectures collapses. A complete architecture must cover all three planes. Any combination that leaves a plane uncovered is incomplete. Any combination that covers a plane more than once introduces overlap and coupling.

Self-hosted infrastructure covers all planes but does so by collapsing them into a single operational domain, increasing cost, risk, and ongoing effort. All other solution types cover exactly one plane.

| Solution Type                                                  | Consumption | Distribution | Authority |
|----------------------------------------------------------------|:-----------:|:------------:|:---------:|
| Self-hosted mail infrastructure<br>                            |      Y      |      Y       |     Y     |

After reduction, only three classes of architectures remain viable in principle: a single system that covers all planes at high operational cost; two systems where one is overloaded to cover two planes; or three systems, each covering exactly one plane.

| Solution Type                                                  | Consumption | Distribution | Authority |
|----------------------------------------------------------------|:-----------:|:------------:|:---------:|
| Inbox-centric hosted email<br>(Fastmail)                       |      Y      |      N       |     N     |
| Alias-centric routing services<br>(ForwardEmail)               |      N      |      Y       |     N     |
| Transactional email services<br>(AWS SES, SendGrid, Postmark)  |      N      |      N       |     Y     |

## Recommendation

The minimal complete architecture assigns exactly one system to each plane, as shown by the plane coverage table above.

Human inboxes are handled by a system optimized for the Human Consumption Plane. Routing and distribution are handled by an alias-centric system that treats domains and addresses as routing primitives. Sending authority is handled by a system optimized for authenticated, domain-native outbound mail.

This composition covers the full taxonomy without special casing. Domains can be added and retired cheaply. Distribution and aggregation are explicit. Human inboxes remain stable. System mail does not impersonate people. Administrative effort and cost scale with people rather than with domains or addresses.

The recommendation is not about feature richness. It is the consequence of aligning abstractions with the shape of the problem so that the system remains understandable as it grows.
