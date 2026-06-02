---
title: OpenAI Codex Python SDK
created: 2026-06-02
updated: 2026-06-02
type: entity
tags: [agent, tool-use, automation, api, devtools, ai-engineering]
sources: [raw/articles/openai-codex-python-sdk-2026-06-02.md]
confidence: low
---

# OpenAI Codex Python SDK

The forwarded source claims OpenAI released a Python SDK for Codex, installable as `openai-codex`, that lets developers embed Codex directly inside Python applications. Because this is a fast-moving release claim captured from a forwarded post rather than an official source page, the current confidence is `low` until verified against OpenAI documentation or the package repository.

## Capabilities mentioned in the source

The post says the SDK can:

- start new Codex sessions;
- run individual agent steps;
- stream progress updates;
- resume previously created sessions;
- pass images into sessions;
- manage access to the sandbox environment;
- use already configured Codex authorization.

## Example pattern

The screenshot shows a `Codex` context manager and a writable workspace sandbox:

```python
from openai_codex import Codex, Sandbox

with Codex() as codex:
    thread = codex.thread_start(sandbox=Sandbox.workspace_write)
    result = thread.run("Find the failing tests, explain the root cause, and propose a fix.")
    print(result.final_response)
```

This suggests a workflow where [[agentic-coding-workflows]] can be embedded as Python functions or services rather than invoked through CLI wrappers.

## Why it matters

If verified, the SDK would make Codex easier to compose into internal developer tools, CI assistants, local automation, review bots, and other [[ai-engineering]] systems. The important shift is from "call a coding agent as an external tool" to "orchestrate a coding agent as an application component".

## Source image

The forwarded post included a screenshot of a minimal SDK example: `raw/assets/openai-codex-python-sdk-example-2026-06-02.jpg`.

## Open questions

- What official documentation, package repository, and changelog confirm the release?
- What sandbox permissions are available beyond `Sandbox.workspace_write`?
- How are streaming events represented in the API?
- How does the SDK authenticate and resume sessions across processes?

## Related

- [[agentic-coding-workflows]]
- [[ai-engineering]]
