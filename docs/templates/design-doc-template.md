<!--
Template guidance: Problem, Requirements and Success Criteria are core.
Keep every other section only when it earns its place for this document;
delete sections that don't apply rather than leaving them empty.
-->

# <Document Title>

**Author:** <name>

**Created:** <YYYY-MM-DD>

**Last updated:** <YYYY-MM-DD>

**Status:** Draft | In review | Accepted

## Overview
What is the purpose of this document and who is it for? Should the reader know
anything before diving in? Is there a targeted audience (technical vs
non-technical)? This section scopes the document itself, not the project.

## Problem
Explain the problem that needs solving. Keep background out of this section
(put it in an appendix). Assume the reader has no prior knowledge and avoid
abbreviations. Link to any supporting material the reader may want.

## Tenets
Principles or beliefs that align everyone on the critical questions, used to go
back to first principles when making a design decision.

## Requirements
All the requirements the problem imposes, written from the end user's
perspective where possible. What do they expect from this solution?

Use cases help:
- As a <role>, I want <capability>.

## Out of Scope
What is deliberately not in scope. Explaining this helps the reader understand
the decision-making framework and avoids unnecessary questions.

## Success Criteria
Imagine the solution is already in production. How will you judge whether it
succeeded? What data proves it?

## Architecture
Describe the solution with explanatory text, a few key diagrams, and some
lists. Balance explanation with diagrams. Say why this is the recommended
design.

### High-Level Overview (HLD)
List the logical components of the system, not specific technologies. A diagram
helps here.

### API Design
The APIs through which users and services interact: payloads, verbs, versions.
How might the API evolve? This section can evolve during implementation.

### Data Storage and Model
What data model and which database? Estimate data volume and forecast growth.
Show the solution scales to the needs of the next 3-5 years. Consider pipelines,
ingestion, pre-processing, and the storage layer.

### Application / Component-Level Design (LLD)
Go deeper on each component. Add component, data-flow, and control-flow diagrams
as applicable.

## Dependencies
Be explicit about other systems you interact with, internal or external.
External ones carry risk you don't control. State your assumptions about them.

## Design Alternatives Considered
The different alternatives you considered (infrastructure platforms, databases,
service frameworks, logical approaches) and which one you recommend and why. A
pros/cons table with columns like cost, scalability, ease of use, latency,
maintainability, and community support helps compare options.

## Cost Analysis
How much infrastructure cost the solution will generate. Plan for
future growth.

## Failure Modes
What can go wrong: dependency failure, traffic overflow, performance
degradation, business-logic bugs. Know how the system can fail.

## Non-Functional Requirements
Scalability, availability, maintainability, reliability, latency, security.

### Scalability
How many users, transactions, queries, how much data?

### Latency and Availability
P99, P50 targets. Define an SLA with your customers.

### Maintainability
How much maintenance per component, and who owns it long term?

### Security
What level of security is required and how is it achieved? Depends on what the
system stores and handles.

## Testing and Observability
### Testing
Unit, integration, A/B, stress tests, and the tools used.

### Metrics and Alarms
Key metrics, dashboards, and the alarms tracking the SLAs.

## Concerns / Risks
Main risks and concerns: external dependencies, resource shortage, and so on.

## Future Improvements
Features users can expect in future releases, and what the timeline might look
like.

## FAQs
Questions people ask regularly, or that you anticipate. Fine to leave blank
until questions appear.

## Appendix A: <subtitle>
Deep technical analysis, data, or investigation detail. Useful background not
required reading for a review.

## Glossary
- <term>: <definition>

## References
- <Service / document>: <link>
