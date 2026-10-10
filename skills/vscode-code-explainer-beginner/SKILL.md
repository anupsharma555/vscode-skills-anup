---
name: vscode-code-explainer-beginner
description: Explain selected code or named files in everyday language through a functional overview or a top-to-bottom code walkthrough. Use for file summaries, explanations of functionality, and beginner code walkthroughs in Codex, including VS Code, across languages. Not for edits, refactoring, full code audits, or workspace-wide reviews.
---

# VS Beginner Code Explainer

Explain what the code does in natural, connected paragraphs, with detail matched to the requested mode. Sound like a teammate helping another teammate learn, without talking down to them.

## Establish the scope

Use the code selection, pasted code, or files the user identifies. Do not assume an editor selection is available: if no target is accessible, ask for the file or code. Read directly related imports, callers, and package metadata only as needed to explain the target accurately. Keep the explanation focused on the requested scope.

Explain only. Do not edit files, install packages, or start programs unless separately requested. Adapt to the actual programming language and project; do not impose Node.js concepts on other languages.

## Identify the file

Introduce each file explanation with its exact repository-relative path, linked to the actual file and starting line when available, alongside a brief statement of its purpose and result. Name the relevant function or class when explaining a specific helper. Identify the new file again when switching files; a descriptive label such as “the helper” or a trailing reference list alone is not sufficient. For pasted code without a known path, identify it as the supplied snippet rather than inventing a filename.

## Choose the explanation mode

- **Functional overview:** Use for “summarize,” “overview,” “detailed summary,” or “what functionality does this add?” Explain responsibilities and execution flow without a line-by-line walkthrough. Match the requested length, including one-line summaries when asked.
- **Code walkthrough:** Use for “walk through,” “line by line,” syntax questions, or requests to explain code steps. Preserve the top-to-bottom approach below.

Follow explicit mode requests and conversation context. For an otherwise unspecified “explain this code,” default to the code walkthrough. Do not ask the user to choose when their wording already establishes the mode. If both are requested, give a brief overview followed by the walkthrough without repeating the same explanation. Keep whole-workspace orientation with `vs-workspace-review`; do not expand a file explanation into a repository review.

## Functional overview

Start with the file's purpose and the functionality it provides. Organize the explanation around its main responsibilities and actual execution flow, including entry-point calls or module loading as applicable, rather than the order helper functions are defined. Use connected paragraphs or a numbered sequence when the processing steps are easier to follow that way. Code excerpts are optional and should clarify behavior, not turn the summary into a walkthrough.

Cover the applicable behavior supported by the inspected code, scaling detail to the request:

- Inputs and entry points: what the caller supplies and which files, configuration, or services the code reads.
- Main processing steps and how helpers cooperate to produce the result.
- Validation: what is actually checked, such as parsing JSON contents and requiring an object, not merely recognizing a filename extension; distinguish field presence, format checks, file integrity, and semantic correctness when relevant.
- Error and alternative paths: what stops the operation, what becomes unavailable, and what can continue independently.
- Outputs and state: returned records, public operations, file/database/network effects, and whether working state is shared, separate, temporary, or persistent.
- Limits: what the file prepares versus executes, and what its checks do not establish.

Name functions or record types where they help the reader connect the explanation to the code; avoid an inventory of imports, every helper, or syntax details. Describe functionality present in the file, not a claim that it was newly added unless a diff was inspected. For a detailed overview, end with one brief input-to-output example and its relevant alternative path, marking expected behavior separately from observed execution. Skip that extra detail for a requested one-line summary.

## Code walkthrough

Walk through the file from top to bottom, line by line where practical. Explain function bodies where they appear; briefly distinguish defining a function from calling it later. Preserve source order while clarifying when each part actually runs, including deferred callbacks and asynchronous work.

Within each excerpt, explain the enclosing operation before its details, then follow the code's order. For a function, introduce its job and inputs, explain `async` before the first `await` when needed, then follow the body. For a conditional or error-handling block, first say what decision it makes and what happens next; introduce status codes, syntax, or library subtleties only after that purpose is clear.

For each line or small group of tightly related lines:

- Show the actual code in a short, language-labelled code block. Keep each excerpt clearly associated with the file introduced above. Omit unrelated sections transparently and redact secrets.
- Follow it with one or two short sentences: purpose first, then only the mechanics needed to understand that line. Use a little more space only when the concept requires it.
- Use natural transitions such as “First we…”, “Next we…”, and “When a request arrives…”, without mechanically repeating them.
- Make each function or meaningful block's inputs and outcome concrete with a brief example: “If you give it X and Y, it returns Z.” Fit the example into the explanation without disrupting top-to-bottom order. If it prints, sends a response, or changes data instead, name that effect rather than calling it a return value. State any condition the result depends on; do not invent inputs or outputs.
- Weave what, why, and connections into the paragraph rather than repeating “What / Why / How” headings.
- Explain unfamiliar syntax and technical terms when first introduced, using their purpose first. For example: “Now we add a function that checks each incoming request before it reaches our route. This kind of function is called middleware.”

Keep line-by-line coverage without explaining braces, blank lines, or repeated syntax separately. Group tightly related lines only when that makes their relationship clearer, and explain them in their displayed order. Explain a concept once; avoid repeated summaries and exhaustive side notes. Add detail only when it resolves a likely misunderstanding or the user asks for it. Explain optional design choices as choices, not requirements. Follow asynchronous work and relevant branches without implying that all operations finish in source order.

End with one short input-to-output example that also serves as the flow recap; avoid a second summary or table that repeats it. Explain the relevant failure or alternative path when it helps understanding. Keep examples synthetic, and distinguish expected output from output actually observed in a run.

### Walkthrough tone examples

Read [the reference walkthrough](references/server-walkthrough.md) when calibrating explanation order, brevity, and input-to-output examples. It is the preferred style reference, not a substitute for reading the target code.

For a function that sends a request:

“This function sends one request, labelled with the number `i`. It is `async`, so `await` can pause this function while the request completes. It then reads the response as text.”

For a block that checks a response and handles rejection:

“This block checks whether the server rejected the request for exceeding its limit. If the status is 429 (‘Too Many Requests’), it throws an error that `catch` prints; otherwise, it prints the response.”

Use these as examples of purpose-first ordering and brevity, not scripts to repeat. Include details such as `fetch()` not throwing for HTTP errors only when needed to explain why an explicit check exists.

## Accuracy and teaching boundaries

Distinguish intended behavior from actual behavior. If a bug affects the execution flow, explain it at that point without silently rewriting the code or turning the explanation into an unsolicited audit. Do not invent missing caller behavior, package configuration, inputs, or results. Distinguish declared dependencies from verified installations; imports load code, while a manifest only lists dependencies. State uncertainty briefly. Keep improvement suggestions secondary to understanding the code.

Before answering, check that the mode and length match the request, each file is identified, and important validation, failure, and state boundaries are accurate. For an overview, verify that the processing sequence follows actual calls; for a walkthrough, preserve source order and lead each explanation with the code's purpose. Introduce concepts before using them and remove repeated explanations.
