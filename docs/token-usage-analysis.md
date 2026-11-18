# Token Usage Analysis — Part 2

> **Reading guide:** The initial comparison table documents earlier unsuccessful experiments. The verified November 9 run, described below, is the successful final result. These runs are not a controlled model-matched comparison.

## Status and scope

This report analyzes context compaction and token usage for
`django__django-15368`. The final successful agent run used
`gemini-3.1-flash-lite`, performed four compactions, and generated a patch
that passed the public SWE-bench evaluation.

Earlier unsuccessful runs are retained as comparative evidence.
Because their models and execution conditions differ from the successful
run, their token totals do not establish a controlled causal comparison.

## Runs

| Metric | Baseline | Compaction v3 |
| --- | ---: | ---: |
| Compaction threshold | Disabled (`0` at CLI) | 6,000 estimated tokens |
| Configured action-step limit | 30 | 30 |
| Recorded successful action responses | 22 | 30 |
| Recorded compaction responses | 0 | 11 |
| Action-request input tokens | 503,730 | 128,334 |
| Compaction-request input tokens | 0 | 67,997 |
| Total recorded input tokens | 503,730 | 196,331 |
| Action-response output tokens | 632 | 861 |
| Compaction-response output tokens | 0 | 4,387 |
| Total recorded output tokens | 632 | 5,248 |
| Final successful action-request input tokens | 40,622 | 2,744 |
| Termination | Input-token-per-minute rate limit at request 23 | Step limit after action 30 |
| Verified task resolution | Not established | Not established |

Source files: `artifacts/django-baseline-trajectory.json` and
`artifacts/django-compact-v3-trajectory.json`. Token totals are sums of the
provider-reported `usage.prompt_tokens` and `usage.completion_tokens` fields
in `responses` and, separately, `compactions[].compaction_response`.
Failed requests without recorded usage are excluded. These are token counts,
not monetary charges; cached-token billing is not analyzed.

## Observations

The baseline accumulated a large prompt. Compaction kept the final action
prompt substantially smaller, despite the compacted attempt completing more
action steps. Summary generation added 67,997 input tokens and 4,387 output
tokens; these costs must not be omitted from the comparison.

One logged compaction reduced the rough active-prompt estimate from 7,856 to
2,610 tokens (approximately 66.8%). These event estimates use the harness's
rough estimator and must not be confused with provider-reported usage.

The summaries retained the task, relevant code locations, existing test
results, and a proposed next action. Nevertheless, the agent repeatedly
inspected source files instead of creating a regression test and implementing
the fix. Existing tests passing without a code change does not establish
resolution of the reported bug.

## Limitations

The runs have different completed step counts, action sequences, and system
prompts. Therefore, the difference in total tokens is descriptive; it is not
a controlled causal estimate of savings attributable only to compaction.
Neither attempt produced a submitted patch that passed `check-swebench`.
Context reduction was demonstrated, but successful end-to-end task completion
was not.

## Completion status

The original remaining tasks were completed in the verified November 9 run.
The agent generated a patch after four compactions, and the submitted patch
passed `check-swebench` (FAIL_TO_PASS 1/1, PASS_TO_PASS 29/29,
RESOLVED: yes).

The earlier unsuccessful runs remain documented as historical comparisons.
Because the baseline and successful run used different models and execution
conditions, their token totals should not be interpreted as a controlled
causal estimate of compaction savings.

## Additional compaction run — November 7

In `django-gemini-focused-trajectory.json`, the agent recorded six
compaction events. At step 10, the estimated active context dropped from
5,923 to 1,727 tokens (about 71%). These are context estimates, not billed
token counts. The run reached the 30-step limit without submitting a
patch, so it demonstrates context reduction but not task completion.
## Verified Django repair — November 9

The agent ran `django__django-15368` with `gemini-3.1-flash-lite`
and a 6,000-token compaction threshold. It submitted the patch at
step 53 after four compactions. At step 13, estimated active context
fell from 6,066 to 1,613 tokens (about 73%).

| Provider-reported usage | Input tokens | Output tokens |
| --- | ---: | ---: |
| 53 action responses | 223,926 | 3,261 |
| 4 compaction responses | 36,733 | 1,435 |
| Total | 260,659 | 4,696 |

The submitted patch passed `check-swebench`: FAIL_TO_PASS 1/1,
PASS_TO_PASS 29/29, RESOLVED: yes. The earlier no-compaction
baseline used a different model and ended early, so it is not a
controlled comparison with this successful run. The before/after
estimates above show context reduction within the successful run.