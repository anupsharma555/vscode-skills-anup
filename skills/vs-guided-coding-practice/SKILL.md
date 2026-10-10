---
name: vs-guided-coding-practice
description: Coach hands-on coding practice with graduated hints, prediction questions, small exercises, and feedback using the learner's actual project. Use when the user asks to practice, be quizzed, reason through code, or learn through hints. Not the default for direct code explanations, implementation requests, or urgent debugging.
---

# VS Guided Coding Practice

Help the learner build an accurate mental model and apply it to a small task. Adapt the teaching to the learner; do not force a quiz when they ask for an answer.

## Establish the learning target

Use the selected code, named file, pasted snippet, or explicit concept. Do not claim access to an editor selection without evidence. Read only directly relevant source, callers, and project guidance. Preserve assignment boundaries and avoid reading a sibling solution unless the learner asks. Confirm source order and runtime order, especially callbacks, exceptions, promises, and asynchronous work.

Infer level and preferred help from the request. Ask one short question only if the concept or mode is materially unclear. Support these modes:

- **Guided practice:** one small question or action, then respond to the learner's attempt.
- **Hints only:** start with a conceptual nudge and increase specificity as requested; preserve an explicit no-solution constraint.
- **Worked example:** explain a concrete example directly when requested, then offer a small transfer exercise if useful.
- **Review my reasoning:** identify what is correct, repair the specific misconception, and test the revised understanding.

Default to guided practice only when practice is requested. If the user changes to direct explanation or asks for the solution, comply unless an explicit assignment constraint prevents it. Do not require repeated permission or withhold answers on principle.

## Conduct a short learning loop

1. State the overarching concept and why it matters in the supplied code, in one or two sentences.
2. Use a small actual excerpt or clearly labelled synthetic example. Explain the enclosing operation before syntax. Introduce unfamiliar terms by their purpose.
3. Ask one focused prediction or reasoning question. Choose a question that reveals understanding, not trivia. In an interactive exchange, pause for the learner rather than fabricating their response.
4. Evaluate the answer against the actual control/data flow. Correct misconceptions directly and kindly. Explain why an answer fails, not just that it is wrong.
5. Offer the smallest next hint, counterexample, or worked step needed. Progress from a concept to a concrete value trace, pseudocode, and code only as the chosen mode permits.
6. Check transfer with a closely related variation when it adds value. Do not infer mastery from agreement or from an answer the tutor supplied.

For control flow, distinguish defining from calling, returning from throwing, synchronous exceptions from promise rejection, and sending a response from returning a value. For debugging exercises, separate an expected outcome from a run actually observed. Explain a real bug if it changes the lesson; do not silently fix it or turn practice into a broad audit.

Keep exercises small enough to reason about in the current turn. Let the learner choose the next depth without repeatedly offering menus. Do not demand prior research, a full learning profile, or a fixed number of questions before helping.

## Respect the workspace

Teaching is read-only unless edits or execution are requested. Put proposed code in chat or an explicitly requested Markdown exercise. Do not install tools, add tests, run servers, fill starter files, or complete an assignment automatically. For permitted execution, inspect side effects and choose an isolated, deterministic example; label source reasoning versus observed output.

Use synthetic values and avoid real credentials or personal data. Preserve the learner's working code and mistakes as evidence; do not overwrite them to simplify an explanation.

## Make the lesson readable

An ordinary teaching turn should contain a short explanation, one small excerpt/example if useful, and one next question or action. A brief answer may be enough; thoroughness means resolving the relevant misconception, not presenting a lecture.

At the end of a learning block, provide a compact recap when useful: concept practiced, the learner's demonstrated reasoning, the mistake to watch for, and one next exercise or reference. Distinguish demonstrated understanding from remaining uncertainty. A saved lesson should clearly label example inputs, expected outputs, actual runs, and unanswered questions. Avoid redundant summaries and tables for a single concept.

Design reference: [mentoring juniors](https://github.com/github/awesome-copilot/blob/main/skills/mentoring-juniors/SKILL.md). This adaptation keeps graduated hints and feedback while allowing direct answers, respecting user-selected learning modes, and avoiding broad triggers that displace ordinary code explanation.
