# ORAND AI Governance Support Framework (BAI GOS)

## Overview

The **Business-AI Governance Operating System (BAI GOS)** is an executable governance architecture designed by ORAND Advisors. It translates business intent and risk appetite into runtime-enforced AI agent behavior. Unlike traditional compliance frameworks that merely document rules, BAI GOS ensures that governance is enacted at runtime with verifiable evidence, rollback capabilities, and portfolio-level steerability.

This repository features the UI simulation for the BAI GOS platform, bridging abstract business policy with executable constraints across various tiers of autonomous agents.

## Core Features and Architecture

The platform translates the **Four Governing Principles** of BAI GOS into an interactive pipeline:
1. No policy without enforcement
2. No autonomy without evidence
3. No change without rollback
4. No runtime action without traceability

### The 13-Layer Architecture
BAI GOS operates across 13 layers divided into **8 Core Layers** (Control Plane, Execution Fabric, and Feedback Loop) and **5 Business Context Management Layers** (the Semantic Middle), ensuring that decisions happen within an active, versioned business context.

### Governed Execution Tiers
The simulation explores actions handled across the three BAI GOS execution tiers:
- **Tier 3 (Auto-Approve):** Machines execute autonomously within explicit boundaries, monitored by the Evidence Ledger.
- **Tier 2 (Warning):** Intercepts consequential actions for required single-use human authorization tokens.
- **Tier 1 (Escrow Hard-Stop):** Immediate workflow halt demanding manual review or redirection when data trust gates or canonicalization fails.

## Project Structure

- **[`bai-gos-full-sim.html`](./bai-gos-full-sim.html)**: The interactive simulation UI demonstrating the Enforcement Gate, Canonicalization Gate, Context Resolution, and Evidence generation. Open directly in a modern browser.
- **[`BAI_GOS_v02.md`](./BAI_GOS_v02.md)**: The v0.2 Architecture Specification detailing the core components, business crosswalk, generative AI integration points, and control states.
- **[`ARCHITECTURE.md`](./ARCHITECTURE.md)**: A developer-focused markdown document bridging the technical simulation logic back to the business domain components.

## Getting Started

1. Clone or download this repository locally.
2. Open `bai-gos-full-sim.html` in an updated web browser (Google Chrome, Edge, Safari, Firefox). No external server is required.
3. Utilize the top-navigation buttons to simulate Fast-Track, Warning, and Hard Stop lifecycle scenarios, and use the Control Plane to visualize context and rule modifications.

## License

This repository uses a dual-license structure to protect the underlying framework while leaving the UI code open. Please see the \[`LICENSE.md`\](./LICENSE.md) file for full details:
- **Software/Code (`.html`, `.js`, etc.)**: [MIT License](https://opensource.org/licenses/MIT)
- **Documentation/Architecture (`.md`, `.docx`)**: [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)

---
**Maintained By**
@ORAND Advisors | Business Consulting - Process Improvement - AI Training
