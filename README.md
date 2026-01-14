⚠️ IMPORTANT LICENSE NOTICE
This repository publishes the PFC specification for review and evaluation only.
Any implementation or production use requires a commercial license from the author.

This repository contains the official specification of the Prime Flow Calculus (PFC) Protocol — a deterministic governance runtime and evidence-generation architecture for AI systems.

Read the full specification

The full specification can be found here:

[Read the full specification](SPEC/PFC-v0.1.md)

Prime Flow Calculus (PFC) is a deterministic governance runtime and evidence-generation architecture for AI systems.

It is designed to control how AI systems operate, change state, and affect the real world.

PFC does not attempt to improve model intelligence, generate content, or make task-level decisions.

Instead, it governs whether an AI system is allowed to perform a given action and whether a proposed state transition is permitted.

PFC operates as a form of meta-intelligence.

Ordinary AI systems answer questions such as what diagnosis to give, what trade to place, or what route to take.

PFC governs higher-order questions such as whether the system has the authority to perform that action, whether the transition is allowed under current conditions, and whether the system remains inside its certified operational envelope.

In this way, PFC controls operational authority and system behavior rather than content.

At the core of PFC is the Stability Kernel, a continuously operating closed-loop control system.

The Stability Kernel monitors the operational state of the system, evaluates proposed state transitions against stability and constraint criteria, and controls which transitions may be committed.

Because this process runs continuously at runtime, unsafe regions of the system’s state space become dynamically unreachable rather than merely detected after the fact.

PFC operates outside the AI model itself and does not rely on training, prompting, or fine-tuning to enforce safety.

Traditional AI safety approaches primarily focus on filtering outputs or moderating responses.

PFC takes a different approach by governing the operational states the system can enter and the real-world actions it is allowed to perform.

Instead of inspecting what the system says, PFC controls what the system can do.

This makes PFC suitable for domains where AI systems have direct real-world impact, such as medical systems, financial systems, autonomous systems, industrial control, and other safety-critical or compliance-sensitive environments.

The PFC architecture is control-theoretic in nature and is designed to generate audit-grade, machine-verifiable evidence of system behavior by construction.

This makes it possible to support regulated deployment scenarios where continuous assurance, traceability, and post-incident analysis are required.

PFC is model-agnostic and domain-agnostic, and is intended to be deployed as a governance layer around existing AI systems rather than as a replacement for them.

The full specification can be found here:

[Read the full specification](SPEC/PFC-v0.1.md)

Prime Flow Calculus (PFC) Protocol, Version 0.1 (Draft), 2026.
