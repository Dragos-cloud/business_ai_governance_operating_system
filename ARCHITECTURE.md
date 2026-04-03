# BAI-GOS Architecture

The Business AI Governance Operating System (BAI-GOS) is divided into two primary conceptual domains: the **Control Plane** (Governance Layer) and the **Execution Pipeline** (Workflow Layer). This document outlines the technical architecture simulated in the current UI and serves as a blueprint for extracting the simulation into a full-stack application.

---

## 1. The Control Plane (Governance Layer)
The Control Plane is responsible for defining the overarching rules, business context, and acceptable thresholds for autonomous agent operation. It dictates the deterministic rules that the Execution Pipeline must follow.

### Components
*   **Business Context Registry (Semantic Layer)**
    *   Maintains the active operating context (e.g., Geographic Region, Risk Profile).
    *   Dynamically adjusts overarching governance strictness based on context changes (e.g., switching from "US Standard" to "EMEA Restricted").
*   **Policy Compiler (Rules & Thresholds)**
    *   Acts as the central authority for setting quality and confidence thresholds for incoming workflows.
    *   Compiles *Draft Policies* into *Certified Active Policies* that are strictly enforced by the execution layer.

---

## 2. The Execution Pipeline (Workflow Layer)
The Execution Pipeline is the literal sequence of operations that real-time data artifacts (such as proposals or invoices) pass through. It represents the "How" compared to the Control Plane's "What".

### The Pipeline Nodes
1.  **Context Resolver (`[🔍]`)**
    *   Attaches the certified business context (from the Control Plane) to the incoming data packet.
2.  **Canonicalization Gate (`[⚖️]`)**
    *   Normalizes the incoming data and performs an initial Data Quality and Confidence Check.
    *   This node maps the packet's quality score against the thresholds defined in the Policy Compiler.
3.  **Decision Engine (`[🧠]`)**
    *   Applies deterministic DMN (Decision Model and Notation) routing rules to evaluate if the packet can proceed autonomously, requires a human, or must be halted.
4.  **Approval Service (`[👤]`)**
    *   The interception point where the workflow pauses to await human intervention if the Decision Engine determines ambiguity or risk (Tier 2).
5.  **Enforcement Gateway (`[🔒]`)**
    *   Cryptographically verifies any human authorization tokens or automated approvals before allowing the final action.
6.  **Mock ERP Adapter (`[💾]`)**
    *   The final destination. Simulates the write-back of the transaction or data into the organization's system of record.

---

## 3. Governance Tiers & Outcomes
Depending on the Data Quality Score and the Active Policy Thresholds, the payload will fall into one of three execution paths:

### Tier 3: Auto-Approve (Fast-Track)
*   **Condition:** The data quality/confidence score exceeds the Control Plane's *Auto-Approve Threshold*.
*   **Outcome:** The packet bypasses the Approval Service entirely and is written directly to the ERP via the Enforcement Gateway. True autonomous operation.

### Tier 2: Human Approval (Warning/Interaction)
*   **Condition:** The data quality score falls below the Auto-Approve Threshold but stays above the Escrow Hard-Stop Threshold.
*   **Outcome:** A consequential action is halted. The system requests a human to evaluate the payload and requires them to cryptographically sign a single-use authorization token (valid for a limited duration) before the pipeline can resume.

### Tier 1: Escrow Airlock (Hard Stop)
*   **Condition:** The data quality score falls below the *Escrow Hard-Stop Threshold*, indicating high risk or a critical failure in canonicalization.
*   **Outcome:** The pipeline stops entirely. The payload enters an "Escrow Airlock" for manual remediation, where it must be explicitly corrected or rejected, creating an immutable audit log of the failure.

---

## 4. Immutable Evidence Service
Every state transition within the Execution Pipeline, as well as policy adjustments in the Control Plane, are logged into an append-only audit trail. This ensures that every automated action and human intervention leaves cryptographic, undeniable evidence of _why_ a deterministic decision was made.
