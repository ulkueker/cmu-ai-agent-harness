# AI Usage

I used ChatGPT/Codex as an assistant to understand the assignment
requirements, review and debug agent implementations, interpret
terminal output and test results, and prepare experiment reports.

I used the following AI models and services:

- ChatGPT/Codex: Assisted with understanding the ReAct agent harness,
  reviewing Python code, troubleshooting errors, interpreting
  evaluation results, and drafting technical documentation.

- Google Gemini: Used for coding-agent experiments, including the
  successful Django SWE-bench repair with gemini-3.1-flash-lite.
  The successful run performed four context compactions and
  submitted a patch that passed check-swebench
  (FAIL_TO_PASS 1/1, PASS_TO_PASS 29/29, RESOLVED: yes).

- GPT-OSS 120B via Groq: Used for the Part 3 chess observation
  experiment. Both runs, with and without legal moves shown,
  reached game_over: true.

- Particle-1 via OpenRouter: Tested for chess-agent compatibility.
  The chess experiment was interrupted by a provider rate limit.

- NVIDIA Nemotron 3 Ultra via OpenRouter: Successfully tested
  function calling and ran a partial chess experiment.
  The experiment stopped when the daily free API quota was reached.

- Inkling-2 Small via OpenRouter: Tested API access, but the
  request was rejected because of agentic-harness restrictions.

For Part 3, Gemini 3.5 Flash Lite was used instead of DeepSeek
with the instructor's permission. Both Gemini observation experiments
(legal moves hidden and legal moves shown) were completed successfully.

All four observation experiments, including the two GPT-OSS 120B runs,
reached game_over: true. The results and error-rate comparisons are
documented in docs/observation-experiment.md.

I executed the commands locally, reviewed the generated logs,
and distinguished verified outcomes from incomplete experiments.

## Model Substitution and API Clarification

With the instructor's permission, Google Gemini 3.5 Flash Lite
was used instead of DeepSeek for the Part 3 observation A/B experiment.
The corresponding output filenames use "gemini" instead of "deepseek"
to accurately identify the model used.

Both GPT-OSS experiments were completed using openai/gpt-oss-120b
through the Groq API.
