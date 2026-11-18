# AI Agent Harness — Implementation & Evaluation

An independent implementation and evaluation project based on
Carnegie Mellon University's 11-768 AI Agents Assignment 1.

## Project Overview

This project explores the design and evaluation of LLM-powered
agents, including code-solving and chess-playing workflows.

The work focuses on agent orchestration, tool interaction,
prompt construction, execution feedback, and evaluation.

## My Contributions

I worked on six Python modules covering:

- Agent execution and control flow
- Code agent prompt construction and task handling
- Chess agent behavior and tool integration
- Tool definitions and execution
- Prompt management

A record of the code modifications is maintained separately
in `my-contributions.patch`.

## Technologies & Concepts

- Python
- Large Language Models (LLMs)
- ReAct-style agent workflows
- Tool Calling
- Agent Harnesses
- SWE-bench task evaluation
- GPT-OSS and Gemini experimentation

## Evaluation Results

| Evaluation | Verified Result |
|---|---|
| Chess terminal-move task (Part 1) | 10/10 tests passed |
| SWE-bench Django task (Part 2) | 30/30 tests passed |

These results apply to the specific evaluated tasks and
do not represent performance across the full SWE-bench benchmark.

## Experiments

Additional experiments explored chess-agent behavior using
different LLM configurations, including comparisons involving
legal-move information.

The observations are exploratory and should not be interpreted
as statistically conclusive benchmark results.

## Original Project & Attribution

This independent project is based on the starter materials
from Carnegie Mellon University's 11-768 AI Agents course.

Original repository:
https://github.com/cmu-agents/assignment-1

Original starter-code authors: Weiwei Sun and Saujas Vaduguru,
with feedback from the CMU 11-768 course staff.

This project is not an official CMU publication or certification.
