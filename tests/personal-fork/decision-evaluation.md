# Personal fork decision evaluation

Baseline: upstream `22f0b463e7a5e579904dd6211a520321035526f7` (7.0.2).
Evaluation: independent agents read the relevant skills and chose actions
for the requests below. These are decision simulations, not executed coding
sessions or a claim of lower measured cost. Run these scenarios in fresh
sessions after future upstream updates; judge actual choices, not wording.

| Request | Baseline decision | Revised decision |
|---|---|---|
| Add a data-only enum value; generic consumer already covered | No enum assertion, but seek failing consumer test or ask for exception | Existing consumer checks, no duplicate test or permission pause |
| Fix retry off-by-one without regression | One real retry regression with outcome and attempt assertions | Same regression, red then green retained |
| Typo and config default with integration coverage | No prose test; configuration exception if no new red test | Existing integration/validation, update behavior expectation if needed |
| Mechanical rename | Cheap implementation | Cheap implementation |
| Authorization race | Most capable | Premium justified by risk |
| Final review of two-line typo | Mandatory most capable | Cheap reviewer |
| Changed wire enum value | Not simulated | Boundary compatibility regression; data-only exception does not apply |
| Obvious assignment vs external service cap | Not simulated | No narration; brief non-obvious reason for cap |

The first forward pass found three inconsistencies: automatic model
escalation in fix-loop guidance, review calibration outside copied prompt
fences, and a test-only completion contract for documentation. Corrected
all three in the skills and templates; an independent follow-up static pass
confirmed those corrections.

Upstream already forbids tautological constant and enum tests in its test
quality reference. This patch removes conflicting incentives rather than
claiming that reference was missing. No blanket reduction in security,
compatibility, boundary, or regression coverage is intended.

## Independent Claude review

Claude Sonnet 5.5 (Medium), through the local Claude Code GUI, reviewed the
uncommitted diff and surrounding instructions. Its review found missing
contract safeguards in worker prompts, insufficient reused-coverage reporting,
and stale red-green wording in the flowchart and execution/template prose.
These were corrected and rechecked. The final verdict was ready for a draft
PR; Claude also reran `git diff --check` successfully.

This is static review, not a live coding benchmark. Removal of the TDD
rationalization/red-flag tables has not been pressure-tested in executing
agent sessions. Cheap reviewers on larger review prompts remain unmeasured.


## Fable 5.2 review and bounded live checks

Fable 5.2 (Medium), in a fresh local Claude Code GUI session, independently
reviewed the diff and intended behavior. It identified reused-coverage
verification, worker-reference delivery, conditional exemptions, stale comment
handling, and deterministic-test guidance gaps. The resulting patch also
resolves the reference's contradictory ban on boundary-spy assertions and
its requirement for unrelated fixture fields.

Not all proposed restrictions were accepted: unchanged tests can already
reproduce a bug; redundant assertions are not automatically merge blockers;
a premium executor does not require a premium typo reviewer. Fable agreed
with these corrections. Review severity follows the actual protection gap.

Two fresh OpenAI coding-subagent sessions used the revised testing skill and
reference on isolated local Python fixtures. They used the inherited model;
this run did not expose an exact model ID or measure cost.

- **Retry bug (live):** request counted the first call in max_attempts and
  explained the external gateway's three-attempt default. The worker added
  two focused tests beside the existing success test: table-driven exhaustion
  and last-attempt success. The exhaustion cases failed before the fix
  (4 vs 3, 2 vs 1, 6 vs 5 attempts); all three test methods passed after it.
  Assertions checked real outcome, attempts, and pauses without sleeping.
  One short comment explained the external limit; no constant-value test.
- **Independent mutation check (executed):** ran those same tests with the
  current function, the old off-by-one implementation, and a harmless
  one-based-loop refactor injected in memory. Results respectively: 0, 3,
  and 0 failures; no errors. Source files were not mutated.
- **Internal enum addition (live):** worker added only PAUSED = 'Paused',
  inspected existing generic rendering/escaping coverage, ran both tests
  successfully, and exercised the new value. No new test or permission pause.

These are bounded smoke checks, not representative benchmarks or proof of
routing on real high-risk projects. Model routing remains statically reviewed.

Fable's final verdict on the amended diff: ready for the updated draft PR.
It independently reran both fixtures and the in-memory old-bug/refactor
checks, then introduced missing-pause and swallowed-final-error mutants;
both produced three failures. It also reran size/layout/whitespace checks
and parsed the graphs. The GUI showed Fable 5.2 Medium; the reviewer itself
could not introspect that effort label.

The live smoke workers consumed testing guidance directly, not the complete
SDD workflow. Worker-path resolution, reviewer reuse inspection/severity,
and risk-based model routing are therefore statically reviewed, not exercised
end-to-end. The reviewer saw resulting artifacts rather than worker transcripts;
independent reruns establish failure sensitivity, not the workers' chronology.
