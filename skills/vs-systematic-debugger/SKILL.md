---
name: vs-systematic-debugger
description: Diagnose a concrete error, failed test, or unexpected behavior through reproduction, source tracing, and hypothesis testing. Present the diagnosis and suggested fix for user confirmation before applying corrections. Use across languages and VS Code projects. Not for broad speculative audits, feature implementation, or a beginner line-by-line explanation.
---

# VS Systematic Debugger

Explain what failed, why the evidence supports a cause, and what would establish a correction. Do not confuse an error message, a hypothesis, a patch, and a verified outcome.

## Frame the incident

Capture the expected behavior, observed behavior, exact trigger or error, relevant revision/environment, and requested scope. Use supplied logs and files first. Ask for a missing reproduction only when current evidence cannot advance the diagnosis. State the requested scope and keep the initial pass diagnostic: gather evidence, explain the cause, and suggest a fix. Present the diagnosis for review before applying corrections.

Read applicable project guidance, relevant command wrappers, manifests, the affected entry point, and nearby tests. Use the named subsystem, not the entire parent repository. Preserve dirty work. For coursework, establish whether the failing code is an intentional exercise gap; do not silently substitute a solution or complete unrelated lessons.

## Investigate before changing behavior

1. **Read the full relevant error.** Identify the first actionable failure and separate downstream symptoms. Distinguish syntax/import/setup failures from assertions, HTTP failures, and external-service failures.
2. **Reproduce at the smallest safe boundary.** Inspect the command and imports for side effects first. Prefer a pure-function call, focused test, or isolated request over starting the full application. If reproduction requires prohibited writes, credentials, installation, paid calls, or a real database, stop that path and continue source analysis; identify the smallest missing proof.
3. **Trace the failing flow.** Follow the input, transformations, calls, and relevant storage/external boundaries until the divergence is explained. Compare one working example or recent change when useful. Do not infer recent causation without revision evidence.
4. **Form a specific hypothesis.** State cause, supporting evidence, and the observation that would disprove it. Test one variable at a time. Avoid stacking speculative changes.
5. **Update from results.** A failed experiment rejects or narrows the hypothesis. Repeated unexplained failures call for a fresh look at assumptions or a narrower reproduction; do not impose an arbitrary retry count or claim an external cause without measuring it.

Use logs proportionally. Capture output once, redact sensitive values, and log state/presence rather than dumping environments, tokens, request bodies, or database records. Distinguish supplied logs from commands run in this session, and synthetic reproductions from production behavior.

## Diagnose and suggest a fix first

Present the diagnosis, supporting evidence, confidence, and remaining uncertainty before making corrections. Suggest the smallest fix, identify the affected files or behavior, explain why it addresses the cause, and describe how it would be verified. If the cause is not established, propose the next diagnostic check instead of presenting a speculative fix as certain.

Wait for the user to review the diagnosis and confirm the proposed fix before changing application code, configuration, or tests to correct the problem. An initial debugging or fix request does not skip this review step. Safe, non-mutating diagnostic checks may proceed within the requested scope; do not apply a speculative patch as part of the initial diagnosis.

After confirmation, implement only the agreed correction. Preserve public contracts, user work, and unrelated behavior. Do not weaken assertions, suppress errors broadly, remove checks, or add retries to hide a defect. Explain a necessary compatibility change before proceeding beyond the confirmed scope.

Use a regression test or minimal reproduction that demonstrates the original failure when practical. Do not add a permanent test for a trivial reversible edit merely to satisfy a ritual. Re-run the relevant failing behavior after the fix, then the repository's smallest appropriate checks. Broaden only when the impact or new evidence justifies it.

If edits or execution are disallowed, provide a concrete correction plan and a verification command grounded in the actual project; do not claim the fix is implemented. If the apparent issue is expected behavior, explain the contract and demonstrate it when safe rather than manufacturing a bug.

## Explain the result

Lead with the diagnosis and confidence. Use short sections when helpful:

- **Observed:** symptom, trigger, and affected scope.
- **Cause:** the evidence chain with precise source references; label unresolved hypotheses.
- **Suggested fix:** the proposed correction, affected files or behavior, rationale, and verification plan; state that it awaits confirmation. After an approved fix, report what was actually changed separately.
- **Verification:** commands and outcomes, what they prove, what was not run, and remaining limits.

Use a small hypothesis table only when multiple explanations remain plausible. Define technical terms by their role, show a short input-to-outcome example when it clarifies the failure, and avoid dumping entire logs. Deliver in chat unless a report is requested. Do not say an application works because an isolated module imports successfully.

Design reference: [systematic debugging](https://github.com/obra/superpowers/blob/main/skills/systematic-debugging/SKILL.md). This adaptation keeps the evidence-led method without requiring its companion skills, secret-bearing diagnostics, rigid ceremony, or unrelated architecture changes.
