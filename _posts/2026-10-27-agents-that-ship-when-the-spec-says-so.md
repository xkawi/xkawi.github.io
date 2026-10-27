---
title: "A hands-on course: agents that ship when the spec says so"
description: "Write the spec, prove the evals can fail, then hand-build the agent pipeline around them."
tags: [AI Agent, Evals, Spec-Driven Development]
---

I put together an interactive course on building AI agents the outcome-based way: [Agents that ship when the spec says so](/lessons/spec-driven-agent-pipeline/).

I've read countless online articles about agentic coding and development workflows, full of buzzwords like "spec-driven development", "loop engineering", "harness" and "eval". I'm new to all this, and it took me a while to grasp what they actually meant. So, together with Claude, I built this interactive course, structured the way I learn best. I hope it helps others pick these ideas up faster too.

The course follows one small project, a Task Tracker API, through five layers:

1. **Spec**: turn a feature request into acceptance criteria a machine can check.
2. **Evals**: write a test per criterion, then prove each one can fail by planting bugs.
3. **Harness**: hand-build the agent loop, tools and a plan, generate, evaluate, decide state machine in Python with the raw Anthropic API.
4. **Observability**: trace every model call, tool call and score in Langfuse.
5. **Feedback**: measure variance across runs, add an LLM judge for what tests cannot see, and change one thing at a time.

By the end the pipeline ships a web UI for the app, guarded by regression evals, and you can open it in your browser.

Everything runs offline with a scripted fake model, so you can work through the whole course without an API key. If you just want to poke at the finished pipeline, the course's Appendix A rebuilds the whole project in one script, with a README listing every command.
