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
