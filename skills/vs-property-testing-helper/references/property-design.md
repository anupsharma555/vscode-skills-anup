# Choosing and checking properties

| Property | Example relationship | Important limitation |
| --- | --- | --- |
| Round trip | decode(encode(x)) equals x | Lossy codecs need normalized equivalence, not exact equality. |
| Idempotence | normalize(normalize(x)) equals normalize(x) | Does not prove the first result is correct; pair with meaningful invariants. |
| Independent oracle | result agrees with a simpler reference model | A copy of the production algorithm shares its bugs. |
| Invariant | Membership, totals, or valid-state constraints hold after operations | State must satisfy stated preconditions; invalid states need their own contract. |
| Metamorphic relation | A controlled input change implies a known output relationship | Only use relationships promised by the domain. |
| Ordering | Output is ordered and preserves the input multiset | Sortedness alone allows an empty output to pass. |

## A stateful example

For a generic voting contract in which each participant chooses one direction, a simple map from participant to last selected direction can act as an oracle. Generate a sequence of participant/direction choices, update the map, apply the real operation, and compare membership and score. Repeating the same direction should not duplicate a participant if that is the established contract. Switching direction should remove only that participant from the opposite group.

Do not assume that choosing the same direction toggles a vote off. Do not treat a mocked `save` as proof of persisted state. Concurrent request behavior needs its own concurrency contract and integration evidence. Avoid inventing response fields that only exist on an in-memory object.

## Avoid false confidence

- Build valid generators directly, rather than discarding most inputs with assumptions.
- Include empty and boundary cases without making all generated inputs empty or identical.
- Give each case fresh state; shared fixtures can create both false failures and false passes.
- Check independent outcomes, not a second spelling of the same computation.
- Distinguish genuine determinism checks from reflexive equality that cannot fail.
- Keep asynchronous failures observable and await the actual operation.
- Record a failure's seed, minimized input, library/runtime version, and command when available; do not fabricate replay metadata for a static proposal.

Official library references (select only the project's actual language/library):

- [fast-check](https://fast-check.dev/docs/introduction/)
- [Hypothesis](https://hypothesis.readthedocs.io/en/latest/)
- [Proptest](https://proptest-rs.github.io/proptest/intro.html)
- [jqwik](https://jqwik.net/docs/current/user-guide.html)

Design reference: [Trail of Bits property-based testing](https://github.com/trailofbits/skills/blob/main/plugins/property-based-testing/skills/property-based-testing/SKILL.md). This is an independently authored adaptation; no upstream scripts or testing framework are bundled.
