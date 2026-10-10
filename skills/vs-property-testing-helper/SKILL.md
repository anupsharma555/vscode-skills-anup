---
name: vs-property-testing-helper
description: Assess, design, write, review, or debug property-based tests for project behavior across generated inputs. Use for invariants, state transitions, serializers, parsers, normalization, and mathematical relationships. Not for routine example tests, UI testing, unrestricted fuzzing, or adding a testing dependency without a concrete benefit.
---

# VS Property Testing Helper

Find meaningful rules that should hold across many inputs, then test those rules without merely repeating the implementation. Explain the property, valid input domain, and what a failure would mean.

## Establish fit and scope

Read the requested code, its requirements/callers, relevant tests, and project guidance. Identify language, existing test runner and property-testing library, command wrappers, and execution constraints. Preserve the project's conventions; do not assume JavaScript, Python, or a particular library. Limit exploration to the requested behavior and its relevant boundaries.

Identify the desired mode: assess suitability, design properties, implement tests, review existing properties, or diagnose a generated counterexample. If the user asks for a proposal, do not edit code or add dependencies. If a property-testing library is absent, state the specific benefit and dependency decision; do not install one merely because this skill was invoked. Existing example tests or a bounded deterministic input loop may be sufficient.

Use [property design](references/property-design.md) for examples, stateful testing, and failure interpretation. Check the selected library's official version-appropriate documentation before writing unfamiliar APIs. If unavailable, provide clearly labelled pseudocode rather than pretending it is runnable.

## Define a meaningful property

1. Describe the user-visible behavior and contract separately from current implementation. Establish valid and invalid inputs and any unresolved requirements.
2. Choose a rule supported by that contract: round trip, idempotence, invariant, ordering, symmetry, equivalence to an independent model, or a relation between multiple executions. Not every function has a useful algebraic property; saying example tests are better is a valid result.
3. Explain why the rule should hold, its preconditions, and a plausible defect it catches. Reject properties that only duplicate the algorithm or check that an object exists.
4. Design generators that produce meaningful inputs directly. Include boundary sizes, empty values, repeated values, encoding/range cases, or command sequences when relevant. Avoid filtering away almost every generated case or accidentally generating only trivial cases.
5. Define the expected observable result and comparison semantics. Account for ordering, identity, floating-point tolerances, nondeterminism, and invalid-domain behavior. Do not assert a stronger contract than the product promises.

For stateful behavior, begin with a valid initial state, apply a generated sequence of operations, and compare with a simpler independent state model after each relevant step. A function can be idempotent for repeating the same action without being reversible. Do not assume toggling, commutativity, or concurrency safety without evidence.

## Implement or review carefully

When authorized, use the installed framework, keep fixtures independent, and bound runtime and input size. Isolate randomness, time, network, and storage. Reset model state for each generated case and await asynchronous checks. Use synthetic data and disposable fixtures; never target a developer or production database. Inspect runners and setup for caches, downloads, and service startup before execution.

Mock a boundary only when the property is about behavior outside that boundary. An in-memory document or mock model can test transition logic but does not prove schema persistence, transactions, HTTP middleware, or concurrency. Report those limits and propose a separate integration check only when valuable.

When a shared helper serves multiple models or response types, inspect each relevant schema and wrapper before sharing assertions. A field present on a mock or one model may not exist in another model's persisted or serialized output.

Run the focused property when allowed, record the seed/replay information, and preserve the minimal counterexample. Check a representative known-bad case when safe to establish that assertions can fail; do not alter production code just to manufacture this proof. Do not claim exhaustive correctness from a finite passing run.

When a property fails, diagnose before fixing. Reproduce the minimized case and identify whether the discrepancy comes from the implementation, property, generated inputs, expected-result model, or environment. Present a readable diagnosis with the expected rule, observed result, failing input or sequence, supporting evidence, uncertainty, and smallest recommended correction. Distinguish observed failures from predictions based only on source inspection.

Let the user review that diagnosis and confirm the proposed correction before applying fixes to any of those layers. Authorization to create or run tests does not by itself authorize fixing discovered discrepancies. After confirmation, apply only the agreed correction and re-run the relevant property when permitted. Do not hide a real counterexample by weakening the generator or increasing retries. Preserve the failing example in the diagnosis; retain it as a regression test when test changes are authorized and it communicates the defect better than a seed alone.

## Present the reasoning and result

For design work, use a compact table: property in plain language, input domain, expected relationship, defect caught, and suitable test layer. Add short code or pseudocode only where requested or needed for clarity. Explain unfamiliar terms such as a generated input (generator), independent expected-result model (oracle), and simplified failing example (shrinking) when used.

For implementation or debugging, report files changed, command and results, seed/counterexample if relevant, assumptions, and checks not run. Distinguish a draft in Markdown from an installed executable test, and a bounded deterministic trial from a library's randomized/shrinking run. Deliver in chat unless a saved artifact is requested. Prefer a few strong properties to a catalog of weak assertions.
