PFC — Prime Flow Calculus Protocol
Version: 0.1
Status: Draft Release
Date: 2026-01-13

This document defines version 0.1 of the Prime Flow Calculus (PFC) Protocol.
This release establishes the initial public specification of the protocol.

---

# PFC v0.1 — Prime Flow Calculus Protocol

Draft Specification

---

## 1. Scope and Purpose

This document specifies the Prime Flow Calculus Protocol (PFC), a deterministic governance runtime and evidence-generation architecture for AI systems.

The scope of this specification is limited to:

- The definition of a system-boundary governance layer that operates at execution time
- The enforcement of externally defined constraints over AI system inputs, outputs, or execution context
- The generation of deterministic, machine-verifiable evidence artifacts
- The definition of conformance requirements for implementations of the protocol

This specification does not define:

- Any AI model architecture
- Any training procedure
- Any content generation mechanism
- Any provider-specific integration
- Any internal model instrumentation

The purpose of PFC is to provide a standardized, implementation-agnostic method for:

- Enforcing governance constraints at runtime
- Producing verifiable evidence of system behavior
- Enabling audit, oversight, and compliance evaluation
- Supporting provider-independent assurance and reproducibility

---

## 2. Terminology

The key words “MUST”, “MUST NOT”, “SHOULD”, “SHOULD NOT”, and “MAY” in this document are to be interpreted as described in RFC 2119.

For the purposes of this specification, the following terms apply:

**AI System**  
Any system that produces outputs using machine-learned or algorithmic models, including but not limited to large language models, multimodal models, or decision systems.

**Governance Runtime**  
A deterministic execution layer that mediates, constrains, or evaluates AI system execution according to externally defined rules.

**Constraint**  
An externally defined rule, policy, or condition that limits or shapes system behavior.

**Evidence Artifact**  
A machine-verifiable, deterministic record produced by the governance runtime that attests to the conditions, constraints, and outcomes of a governed execution.

**Execution Envelope**  
The bounded environment in which an AI system is executed under governance control.

**Policy Source**  
An external authority or definition system that provides constraints to the governance runtime.

**Conformance**  
The degree to which an implementation satisfies the mandatory requirements of this specification.

---

## 3. Problem Statement

Current approaches to AI governance rely predominantly on:

- Organizational policy and process
- Provider assertions
- Post-hoc analysis and logging
- Non-deterministic or non-reproducible audit trails

These approaches suffer from several structural limitations:

- They do not enforce constraints at execution time
- They do not produce independently verifiable evidence
- They rely on trust in providers, infrastructure, or internal instrumentation
- They do not support reproducible or adversarial audit

As a result, current governance methods are insufficient for:

- High-assurance compliance environments
- Independent oversight and regulation
- Forensic audit and investigation
- Cross-provider or cross-system comparability

PFC addresses this gap by specifying a deterministic governance runtime that:

- Enforces constraints at execution time
- Produces machine-verifiable evidence artifacts
- Operates independently of model internals and provider infrastructure
- Enables reproducible, third-party verification of governed executions
---

## 4. Design Goals and Non-Goals

### 4.1 Design Goals

The design goals of PFC are:

1. **Determinism**  
   Governed executions MUST produce deterministic, reproducible results with respect to governance decisions and evidence generation.

2. **Provider Independence**  
   The protocol MUST NOT require access to model internals, training data, or provider-controlled infrastructure.

3. **Execution-Time Enforcement**  
   Constraints MUST be enforced at execution time, not solely through post-hoc analysis.

4. **Machine-Verifiable Evidence**  
   The system MUST produce evidence artifacts that can be independently verified without reliance on provider assertions.

5. **Implementation Agnosticism**  
   The specification MUST NOT prescribe any specific model architecture, vendor, or deployment topology.

6. **Auditability and Reproducibility**  
   Governed executions MUST support third-party audit and reproducible verification.

---

### 4.2 Non-Goals

PFC explicitly does not attempt to:

- Define AI model behavior or correctness
- Replace organizational governance, legal, or policy processes
- Perform content moderation or classification
- Guarantee semantic correctness of model outputs
- Perform training-time alignment or optimization
- Provide real-time safety guarantees beyond constraint enforcement

PFC is a governance and evidence protocol, not a safety oracle or behavioral correctness system.

---

## 5. System Overview

At a high level, PFC defines a governance execution envelope that sits at the boundary between an AI system and its operating environment.

Conceptually, the system consists of:

- An AI System (unmodified, opaque)
- A Governance Runtime (deterministic, external)
- One or more Policy Sources (external)
- An Evidence Generation subsystem
- An Execution Envelope that mediates all governed interactions

All interactions between the AI system and the external environment that are subject to governance MUST pass through the governance runtime.

The governance runtime:

- Receives execution requests
- Applies externally defined constraints
- Determines whether and how execution may proceed
- Records the governance decision process
- Emits deterministic evidence artifacts describing the governed execution

The AI system itself is treated as an opaque component and is not required to expose any internal state or instrumentation.

---

## 6. Architecture Model

### 6.1 Conceptual Components

A conforming PFC implementation consists of the following logical components:

- **Execution Request Interface**
- **Governance Runtime**
- **Constraint Evaluation Engine**
- **Policy Source Interface**
- **Evidence Generator**
- **Evidence Store (logical)**

### 6.2 Control Flow

At a minimum, the following control flow MUST occur for each governed execution:

1. An execution request is submitted to the governance runtime.
2. The governance runtime retrieves or is provided applicable constraints from one or more policy sources.
3. The constraint evaluation engine evaluates the request against the constraints.
4. A governance decision is produced (e.g., allow, deny, modify, require conditions).
5. If permitted, the execution proceeds within the execution envelope.
6. The evidence generator produces a deterministic evidence artifact describing:
   - The request
   - The applicable constraints
   - The evaluation result
   - The governance decision
   - The execution outcome (if applicable)
7. The evidence artifact is made available for audit and verification.

### 6.3 Trust Boundaries

The governance runtime and evidence generator form the trust boundary of the PFC system.

The AI system itself is explicitly outside the trust boundary.

Conformance to this specification MUST NOT depend on:

- The correctness of the AI system
- The honesty of the AI provider
- The integrity of provider-controlled infrastructure

---

## 7. Execution Envelope

The execution envelope is the controlled environment in which governed executions occur.

A conforming implementation MUST ensure that:

- All governed inputs and outputs pass through the governance runtime
- Constraints are enforced prior to and/or during execution
- Evidence generation is not bypassable by the AI system
- The AI system cannot suppress or alter evidence artifacts

The precise implementation of the execution envelope is left to implementers, provided the above properties are satisfied.

---
---

## 8. Constraint Model

### 8.1 General

PFC defines a constraint as any externally defined rule, policy, or condition that governs whether and how an execution may proceed.

Constraints:

- MUST be defined outside the AI system
- MUST be interpretable by the governance runtime
- MUST be evaluated deterministically
- MUST NOT depend on AI model internal state

Constraints MAY:

- Reference request metadata
- Reference execution context
- Reference identity, jurisdiction, or classification information
- Reference prior evidence artifacts

### 8.2 Constraint Evaluation

A conforming implementation MUST ensure that:

- All applicable constraints are evaluated prior to or during execution
- Constraint evaluation produces a deterministic result
- The result of constraint evaluation is included in the evidence artifact

Constraint evaluation MUST result in one of the following abstract outcomes:

- Permit
- Deny
- Permit with modification
- Permit with conditions

The precise semantics of these outcomes are implementation-defined, but the outcome MUST be recorded in evidence.

---

## 9. Evidence Model

### 9.1 General

For each governed execution, the system MUST produce an evidence artifact.

An evidence artifact is a deterministic, machine-verifiable record describing:

- The execution request
- The applicable constraints
- The constraint evaluation result
- The governance decision
- The execution outcome (if any)

### 9.2 Required Properties

Evidence artifacts MUST be:

- Deterministic
- Tamper-evident
- Independently verifiable
- Stable under re-evaluation
- Unforgeable by the AI system

### 9.3 Evidence Content

At a minimum, an evidence artifact MUST include:

- A unique identifier
- A timestamp or logical time marker
- A representation or hash of the execution request
- A representation or hash of the constraints applied
- The evaluation result
- The governance decision
- The execution outcome or disposition
- Integrity protection data (e.g., signature, hash chain, or equivalent)

The specific encoding format is implementation-defined.

---

## 10. Determinism Requirements

A conforming implementation MUST ensure that:

- Given the same execution request, constraints, and context, the governance decision is identical
- Evidence artifact generation is deterministic
- Verification of an evidence artifact yields a deterministic result

Non-determinism originating from the AI system itself does not invalidate conformance, provided that:

- The governance decision process is deterministic
- The evidence artifact accurately reflects what occurred

The governance runtime MUST NOT rely on:

- Randomness
- Time-dependent external state (unless explicitly included in evidence)
- Non-reproducible external services

---

## 11. Conformance Requirements

### 11.1 General

An implementation conforms to this specification if and only if it satisfies all requirements labeled as MUST or MUST NOT.

### 11.2 Mandatory Capabilities

A conforming implementation MUST:

- Enforce externally defined constraints at execution time
- Produce evidence artifacts for all governed executions
- Ensure evidence artifacts are deterministic and verifiable
- Treat the AI system as outside the trust boundary
- Prevent the AI system from bypassing governance or evidence generation

### 11.3 Optional Capabilities

An implementation MAY:

- Support multiple policy sources
- Support multiple evidence storage backends
- Support streaming or batch execution modes
- Support hierarchical or compositional constraints

Such features MUST NOT weaken any mandatory requirement.

---

## 12. Security Considerations

PFC assumes that the AI system is not trustworthy.

A conforming implementation SHOULD consider threats including:

- Bypass of the governance runtime
- Suppression or tampering of evidence artifacts
- Forged policy inputs
- Replay or substitution of execution requests
- Confused-deputy and privilege escalation scenarios

Mitigations are implementation-defined, but the architecture MUST preserve:

- Integrity of governance decisions
- Integrity of evidence artifacts
- Independence from AI system behavior

---

## 13. Out of Scope

This specification does not define:

- Cryptographic algorithms
- Policy languages
- Evidence serialization formats
- Deployment architectures
- Regulatory processes
- Legal interpretations

These are left to profiles, companion standards, or implementations.

---
---

Appendix A — Example Governed Execution (Informative)

This appendix is informative and not normative.

The following illustrates a simplified example of a governed execution under PFC.

A.1 Scenario

An external application submits a request to an AI system to generate a response.

The environment requires that:
	•	The request be classified by jurisdiction
	•	Certain categories of requests are disallowed
	•	All executions must produce auditable evidence

A.2 Inputs

Execution Request:
	•	Request ID: R-12345
	•	Payload: “Generate a response to user query X”
	•	Context:
	•	Jurisdiction: US
	•	Requester Role: Public User

Policy Source provides constraints:
	•	C1: Requests from Public User MUST NOT access restricted capabilities
	•	C2: Requests in Jurisdiction US MUST be logged
	•	C3: Requests classified as Category Z MUST be denied

A.3 Governance Flow
	1.	The execution request is submitted to the governance runtime.
	2.	The governance runtime retrieves applicable constraints from the policy source.
	3.	The constraint evaluation engine evaluates:
	•	C1: PASS
	•	C2: PASS
	•	C3: PASS
	4.	The governance decision is: PERMIT
	5.	The execution proceeds within the execution envelope.
	6.	The evidence generator produces an evidence artifact describing the execution.

⸻

Appendix B — Example Evidence Artifact (Informative)

This appendix is informative and not normative.

The following is an illustrative example of an evidence artifact in a JSON-like form.

Example evidence artifact:

{
“evidence_id”: “E-98765”,
“timestamp”: “2026-01-13T12:00:00Z”,
“request”: {
“request_id”: “R-12345”,
“request_hash”: “0xABC123…”
},
“constraints”: [
{ “id”: “C1”, “result”: “PASS” },
{ “id”: “C2”, “result”: “PASS” },
{ “id”: “C3”, “result”: “PASS” }
],
“governance_decision”: “PERMIT”,
“execution_outcome”: {
“status”: “COMPLETED”,
“output_hash”: “0xDEF456…”
},
“integrity”: {
“artifact_hash”: “0x999999…”,
“signature”: “0xSIG…”
}
}

This example is illustrative only. The actual encoding, hashing, and signing mechanisms are implementation-defined.

⸻

Appendix C — Example Constraint Evaluation (Informative)

This appendix is informative and not normative.

An example constraint evaluation process:

Input:
	•	Request metadata
	•	Execution context
	•	Policy constraints

Evaluation:
	•	Evaluate each constraint deterministically
	•	Record result for each constraint
	•	Produce a final governance decision

Output:
	•	Decision: PERMIT / DENY / MODIFY / CONDITIONAL
	•	Evidence record including:
	•	All evaluated constraints
	•	Their results
	•	The final decision

⸻

Appendix D — Profiles and Extensions (Informative)

This specification defines a core protocol.

Future documents or standards MAY define:
	•	Standard policy languages
	•	Standard evidence formats
	•	Standard cryptographic profiles
	•	Domain-specific governance profiles (e.g., healthcare, finance, government)

Such profiles MUST NOT weaken the core requirements of this specification.
