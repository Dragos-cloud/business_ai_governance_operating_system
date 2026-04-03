---
title: ORAND AI Governance Support Framework (BAI GOS)
version: 0.2
date: 2026-03-20
author: ORAND Advisors
status: Draft
internal-name: BAI GOS — Business-AI Governance Operating System
public-name: ORAND AI Governance Support Framework
---

<!-- SECTION:META
  Document: BAI_GOS_v02.md
  Version: 0.2
  Description: Full architecture specification — internal, contribution-ready, and client-facing
  Last-modified: 2026-03-20
  Sections: META, OVERVIEW, ARCHITECTURE, COMPONENTS, CONTEXT-MODEL, CROSSWALK, STATES, INTEGRATION, CLIENT
-->

---

# ORAND AI Governance Support Framework
## Architecture Specification v0.2

> **License:** © 2026 ORAND Advisors. This document is licensed under the [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0) License](https://creativecommons.org/licenses/by-nc-nd/4.0/). See `LICENSE.md` for details.

---

## SECTION A — Internal Reference

### A.1 Design Purpose

BAI GOS translates business intent and risk appetite into runtime-enforced agent behaviour, with evidence, rollback, and portfolio-level steerability.

Four governing principles apply without exception:

- No policy without enforcement
- No autonomy without evidence
- No change without rollback
- No runtime action without traceability

These principles make BAI GOS an executable governance architecture, not a documentation framework. The distinction is foundational: governance becomes real only when system permissions and controls enforce it technically.

### A.2 The Compliance-Governance Gap

BAI GOS as originally conceived was a compliance architecture. The gap between compliance and governance cannot be eliminated by better specification — it can only be made visible and managed through human normative practice.

Compliance asks whether an action conformed to the rules. Governance asks whether it served the purpose the rules were designed to achieve.

This reframe is foundational to everything that follows. BAI GOS provides the architecture that makes governance *possible*. Performed governance — governance that is enacted, not merely declared — requires humans operating within that architecture.

### A.3 Position Within the Four-Stage Business Operating Model

BAI GOS sits primarily within Stage 3 (GOVERN) of the ORAND Business Operating Model for Agentic AI, but its reach spans three of the four stages:

| Stage       | ORAND Instrument | BAI GOS Contribution |
|-------------|---|---|
| 1 — SCAN    | Agentic Opportunity Map | Portfolio Steering layer (Layer 8) feeds strategic alignment data into SCAN |
| 2 — DESIGN  | PAiD  | Policy Compiler and Canonicalization Gate enforce the process specifications PAiD produces |
| 3 — GOVERN  | RAEO                      | BAI GOS is the executable implementation layer for RAEO governance decisions |
| 4 — OPERATE | Agentic Operations Rhythm | Evidence & Assurance layer (Layer 7) and Portfolio Steering (Layer 8) supply the operational telemetry OPERATE consumes |

BAI GOS is the technical implementation of Stage 3 that makes Stages 2 and 4 governable at runtime.

---

### A.4 The Two Governance Planes

A holistic AI governance architecture requires two distinct but linked planes:

**Plane 1 — Business Agent Governance (ORAND / BAI GOS)**

Answers:
- Which Work Types are in scope and why they matter
- What tier of authority is allowed and what evidence supports expansion
- What decisions are delegated and under what conditions
- What boundaries, approvals, rollback, and evidence are required
- When autonomy can be promoted or demoted

**Plane 2 — IT AI Governance**

Answers:
- Which models, platforms, and tools are allowed
- How identities, secrets, and access are managed
- How prompts, agents, workflows, and tools are versioned and deployed
- What telemetry, logging, security, and incident controls exist
- How regulatory, security, and resilience requirements are enforced technically

BAI GOS governs the delegation of business authority through the IT platform. IT AI governance protects the platform through which that authority is exercised. Neither substitutes for the other. Integration is required at runtime and in change control.

---

### A.5 The 13-Layer Architecture

BAI GOS has 13 layers organised into two groups: 8 Core Layers (the operating system) and 5 Business Context Management Layers (the semantic middle).

#### The 8 Core Layers

Grouped into three functional zones:

**The Control Plane (Layers 1–3)**

| Layer | Name                  | Function                                                                                                                                                                               |
|-------|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1     | Strategic Control     | Captures business intent, Work Type portfolio, autonomy targets, and always-true constraints. The topmost governance source — never bypassed by local optimisations.                    
| 2     | Governance Repository | Git-like versioned source of governance truth. Stores AgentSpec, PolicyBundles, DMN decisions, BPMN enforcement points, canonical schemas, mapping sets, rollback plans, and evidence bundles. |
| 3     | Policy Compiler       | Translates business policy into machine-readable, runtime-enforceable constraints. Bridges the semantic gap between "business approved this policy" and "the runtime knows what to do." |

**The Execution Fabric (Layers 4–6)**

| Layer | Name             | Function                                                                                                                                                                                   |
|-------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 4     | Enforcement Gate | Enforces runtime permissions, tier boundaries, approval requirements, tool scopes, side-effect restrictions, and escalation rules. The only authorised path to consequential action.       |
| 5     | Data Trust Layer | Canonicalization Gate + Escrow. Validates inputs via schema checks, mapping currency verification, normalisation, and ambiguity handling. Returns PASS / PASS_WITH_WARNINGS / FAIL_ESCROW. |
| 6     | Orchestration    | Manages active workflows — agent invocation, state, tool calls, human handoffs, retries, escalation, and incident routing. Consumes policy; does not own it.                               |

**The Feedback Loop (Layers 7–8)**

| Layer | Name               | Function                                                                                                                                                                   |
|-------|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 7     | Evidence Layer     | Captures tamper-evident, immutable traces linking every runtime event to its governance version, business context version, and decision logic.                             |
| 8     | Portfolio Steering | Ensures the entire agent portfolio remains aligned to business intent. Detects drift, evaluates tier promotion/demotion evidence, flags strategic responsiveness failures. |

#### The 5 Business Context Management Layers

These layers form the *semantic middle* — the governed bridge between abstract policy and executable constraints. They determine under what conditions a policy, decision, or agent action is valid.

| Layer | Name                                             | Function                                                                                                                                                     |
|-------|--------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| C1    | Strategic Context                                | Defines high-level intent and always-true constraints. Connects Work Types to the business objectives they serve.                                            |
| C2    | Operating Context                                | Manages the specific environment in which a Work Type runs - region, business unit, legal entity, fiscal period.                                             |
| C3    | Decision Context                                 | Provides parameters for DMN logic - tolerance values, approval thresholds, duplicate windows. Prevents overgeneralised rules from applying outside their intended scope. |
| C4    | Data Translation Context (Interpretation Record) | Holds the assumptions needed for accurate data interpretation - locale, currency conventions, source system schema fingerprint, mapping set version. Feeds the Canonicalization Gate. |
| C5    | Exception & Escrow Context                       | Defines the posture and safety rules for suspended cases - SLA, resolver role, WIP limits, stop-the-line thresholds, timeout actions.                        |

#### Why the Semantic Middle Matters

Without explicit context lifecycle management, agent systems drift silently. The business conditions under which a decision rule is valid change over time — but if only the rule is versioned and not its context, the governance record is incomplete. Audit cannot reconstruct the decision. The three-agent cash scenario (P2P, O2C, Treasury) illustrates the portfolio-level version of this failure: each agent operating correctly within its local governance while collectively producing an outcome no individual governance layer reveals.

---

### A.6 The 9 Core Components

#### Component 1 — Work Type Registry
Authoritative registry of governed business units of deployment. No runtime execution without a valid, active Work Type. No Tier 3 Work Type without a certified rollback path.

**Key APIs:** `registerWorkType()`, `getWorkType()`, `updateTier()`, `setWorkTypeStatus()`

#### Component 2 — Business Context Registry *(new in v0.2)*
First-class governed object registry for business context. Each context object carries: context type, version, status lifecycle (DRAFT → UNDER_REVIEW → ACTIVE → RESTRICTED → DEPRECATED → RETIRED), validity window, scope dimensions (region, country, business unit, legal entity, vendor segment, currency), operating parameters, declared assumptions, and dependency references.

Context is not policy. Policy defines what is allowed. Context defines when, where, for whom, and under what assumptions that policy is valid.

**Key APIs:** `resolveContext()`, `createContext()`, `deprecateContext()`, `getContextDrift()`

#### Component 3 — Governance Artifact Registry
Version-controlled repository of all governed artifacts: AgentSpec, PolicyBundle, DMN artifacts, BPMN anchors, canonical schemas, mapping sets, tool permission matrices, escalation rules, and rollback plans. Only certified versions are eligible for production resolution.

**Key APIs:** `createArtifact()`, `resolveCertifiedBundle()`, `diffArtifacts()`

#### Component 4 — Change Control & Certification Service
Lifecycle from proposal to certification to rollback. Implements the Git-like change pattern: propose → diff → impact assess → test → approve → deploy → rollback. High-risk changes require stronger approval chains. All Tier 3 changes must declare rollback targets. Emergency rollback preserves the audit trace.

**Key APIs:** `submitChangeRequest()`, `attachTestEvidence()`, `certifyRelease()`, `rollbackToVersion()`, `freezeWorkType()`

#### Component 5 — Policy Compiler
Bridges business governance semantics to runtime constraints. Produces compiled policy manifests with: scope rules, side-effect permissions, approval requirements, escalation triggers, telemetry requirements, and enforcement instructions. Compilation must fail on missing dependencies. No natural-language-only policy reaches runtime.

**Key APIs:** `compilePolicyBundle()`, `getCompiledPolicy()`, `validateCompilation()`

#### Component 6 — Canonicalization & Escrow Service
Determines whether inbound data is trustworthy enough for downstream decisions and execution. Runs: schema signature checks, source version checks, normalisation, canonical mapping, ambiguity handling, and escrow routing. Output verdicts drive all downstream routing.

**Verdicts:**
- `PASS` — canonical payload proceeds
- `PASS_WITH_WARNINGS` — canonical payload proceeds in restricted mode; no external side effects
- `FAIL_ESCROW` — stops autonomous path; routes to human escrow queue

**Key APIs:** `normalizeAndValidate()`, `getGateVerdict()`, `createEscrowCase()`, `releaseEscrowCase()`

#### Component 7 — Decision Service
Executes governed decision logic using certified DMN artifacts. Evaluates only canonical payloads. Returns: outcome, reason codes, inputs used, decision trace ID. Only certified decision versions run in production.

**Key APIs:** `evaluateDecision()`, `getDecisionTrace()`

#### Component 8 — Enforcement Gateway
The only authorised runtime path to consequential action. Checks: actor identity, scope, permission, compiled policy version, tier, side-effect allowance, approval token, time window, and entity/region restrictions. No direct side effect without a gateway decision. Denied actions still produce evidence.

**Key APIs:** `authorizeAction()`, `validateApprovalToken()`, `checkToolScope()`

#### Component 9 — Evidence & Assurance Service
Captures governance-relevant runtime evidence and supports oversight. Maintains: audit traces, event ledger, evidence bundles, assurance tests, control health metrics, and promotion/demotion indicators. Evidence must link every runtime event to governance version, context version, and decision version. Assurance logic detects missing evidence — not just present evidence.

**Key APIs:** `emitEvidence()`, `getEvidenceBundle()`, `runAssuranceChecks()`, `getControlHealth()`

---

### A.7 Core Runtime Flow

1. Work instance arrives at a Work Type boundary
2. Canonicalization Gate validates data — escrows if not trustworthy
3. Context Resolver determines the active Business Context for this Work Type, region, and date
4. Orchestrator loads certified governance state — Work Type, tier, AgentSpec, PolicyBundle, DMN dependencies
5. Agent or DMN reasons within scope
6. Enforcement Gateway checks every consequential step before any external action
7. If action allowed, execute; if not, escalate, queue for approval, or freeze
8. Every meaningful event emits to the Evidence Ledger with policy version, context version, and trace IDs
9. Telemetry feeds Portfolio Steering — drift signals, promotion/demotion indicators, assurance findings

The enforcement order is invariant: validate data → resolve context → determine path → reason or orchestrate → check permission → only then act.

---

### A.8 Control States

Governed artifacts and Work Types move through a defined set of operational states:

`Draft` → `Tested` → `Certified` → `Heightened Monitoring` → `Restricted` → `Frozen` → `Demoted` → `Rolled Back` → `Retired`

These states make governance legible. A system that cannot declare its current control state cannot be governed.

---

### A.9 The 17-Domain Business-IT Governance Crosswalk

Each Work Type maps across both planes through 17 governance domains:

| Domain                      | Primary Owner          | BAI GOS Artifact                | IT Control                        |
|-----------------------------|------------------------|---------------------------------|-----------------------------------|
| Strategy & Portfolio        | Strategy + Architecture| Agentic Opportunity Map         | Enterprise architecture portfolio |
| Work Type                   | Business process owner | Work Type definition            | Application/service catalog       |
| Decision                    | Business + Risk        | DMN decision tables             | Decision service / rule engine    |
| Tiered Authority            | Risk + Security        | Tier model (1/2/3)              | RBAC / permission model           |
| Policy                      | Risk / Compliance      | Policy Bundle                   | Policy engine                     |
| Data                        | Data governance + IT   | Canonical schema + mapping sets | Data governance platform          |
| Data Quality & Escrow       | Operations             | Escrow rules                    | Data quality monitoring           |
| Agent                       | AI platform team       | AgentSpec                       | Agent registry                    |
| Model                       | AI platform governance | Model dependency declaration    | Model registry                    |
| Tool                        | IT platform            | Tool permission matrix          | API gateway / service mesh        |
| Identity                    | Security               | Actor definition                | IAM                               |
| Security                    | CISO                   | Security constraints            | Security architecture             |
| Change                      | DevOps                 | Governance repository           | CI/CD pipeline                    |
| Monitoring                  | Operations             | Monitoring policy               | Observability stack               |
| Incident                    | Security + Ops         | Incident playbooks              | SOC / incident response           |
| Assurance                   | Risk + Internal Audit  | Assurance tests                 | Testing frameworks                |
| Regulatory                  | Legal / Compliance     | Regulatory control mapping      | Compliance platform               |

---

## SECTION B

### B.1 What BAI GOS Is

The ORAND AI Governance Support Framework is the executable governance architecture that translates business intent into runtime-enforced agent behaviour.

Most organisations deploying AI agents face the same structural gap: governance is declared in policy documents but not enforced at runtime. Agents execute. Humans observe. The policy and the execution remain unconnected. BAI GOS closes that gap by making every governed decision traceable to the policy version, business context, and authority that authorised it.

This is what distinguishes BAI GOS from compliance frameworks. Compliance records whether rules were followed. BAI GOS enforces which rules apply, when, to which agents, with what evidence, and with clear rollback when the evidence degrades.

### B.2 The Five Deployment States

AI deployments exist on a spectrum from human augmentation to autonomous multi-agent systems. Each state carries distinct governance requirements. Applying the wrong governance model to a state creates blind spots — particularly at the transitions between states.

| State                  | Description                                                                                  | Governance Priority                                                                            |
|------------------------|----------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| 1 — Augmented Human    | AI as tool (e.g., Copilot). Human decides.                                                   | Shadow deployment risk. Establish usage boundaries.                                            |
| 2 — Assisted Workflow  | AI inserted into existing process steps.                                                     | Inherited process errors accelerate. Process quality precedes AI insertion.                    |
| 3 — Orchestrated Agent | Multi-step process purpose-built for AI. Workflow logic joins model reasoning at "The Join". | Governance gap at the join point. This is where BAI GOS enforcement begins.                    |
| 4 — Dynamic Agent      | AI plans its own execution sequence at runtime.                                              | Action chains become difficult to audit or reverse. Tier model and rollback become mandatory.  |
| 5 — Multi-Agent System | Multiple agents coordinate independently.                                                    | Errors launder and amplify across the agent chain without human detection. Portfolio Steering is the only defence. |

**The Transition Trigger:** Review governance whenever adding write access, external communications, or removing human oversight steps. Each of these moves the deployment toward a higher state.

### B.3 The Quick-Reference Governance Diagnostic

| Question                                      | If Yes                                    | If No                                 |
|-----------------------------------------------|-------------------------------------------|---------------------------------------|
| Does the AI take action without confirmation? | State 3 or above — enforce tier model     | State 1 or 2 — shadow deployment risk |
| Does the agent plan its own sequence?         | State 4 or 5 — enforce audit and rollback | State 1, 2, or 3                      |
| Are multiple agents coordinating?             | State 5 — enforce portfolio steering      | State 4 or below                      |

### B.4 What BAI GOS Enables

**For the board and C-suite:**
Clear sight of which agents hold what authority, at what tier, under what evidence. The conditions under which autonomy is expanded or revoked are explicit, not assumed.

**For risk and compliance:**
Every agent action traces to a certified governance version. The Canonicalization Gate prevents decisions on untrusted data. The Evidence Ledger supports audit reconstruction without relying on agent logs alone.

**For business process owners:**
Work Types are governed end-to-end — from strategic intent through to runtime enforcement and evidence capture. The Business Context Registry ensures governance remains valid as business conditions change.

**For operations:**
Portfolio Steering detects drift before it becomes a strategic problem. Promotion and demotion are evidence-driven, not schedule-driven.

### B.5 Strategic Responsiveness

Strategic Responsiveness — the organisation's capacity to keep its agentic architecture aligned with strategy — is the governing concept connecting BAI GOS to the ORAND Business Operating Model.

BAI GOS addresses SR across two failure modes:

**Internal coherence failure:** Agents produce collective outcomes that no individual governance layer reveals. The Portfolio Steering layer (Layer 8) is the only architectural response to this failure mode.

**External adaptability failure:** Strategic decisions cannot reach the autonomous execution layers. The Strategic Control Layer (Layer 1) and Business Context Registry (C1–C2) create the propagation path from strategic intent to runtime constraint.

---

## Appendix: Key Vocabulary

| Term                       | Definition                                                                                                                                     |
| Work Type                  | End-to-end business flow crossing functional boundaries — the primary unit of agentic deployment and governance                                |
| Tier 1                     | Machine recommends; human decides                                                                                                              |
| Tier 2                     | Machine drafts or executes; human approves before consequential action                                                                         |
| Tier 3                     | Machine executes autonomously within explicit boundaries, with rollback and monitoring                                                         |
| Canonicalization Gate      | The Data Trust Layer service that validates inbound data before any downstream decision or action                                              |
| Business Context           | A governed, time-bounded, scope-bounded set of business conditions under which a Work Type, decision, or policy remains valid                  |
| Performed Governance       | Governance that is enacted through actual practice — the standard BAI GOS holds human roles to, not declared governance                        |
| Strategic Responsiveness   | The organisation's capacity to keep its agentic architecture aligned with strategy at two levels: internal coherence and external adaptability |
| Compliance Drift Indicator | Portfolio Steering signal that measures the gap between declared governance posture and actual runtime behaviour                               |
| Interpretation Record      | The Data Translation Context layer — holds the assumptions needed for accurate data interpretation at the Canonicalization Gate                |
