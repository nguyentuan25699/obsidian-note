
## 1. [[Claude Platform 101]]
- The Claude Platform is Anthropic's infrastructure for building with Claude programmatically: a REST API, SDKs, CLIs, and a console for keys, usage, managed agents, and prompt testing.
- Think of it as three layers: **primitives** (Messages API, tool use, files, web search, code execution, MCP servers, skills), **infrastructure** (managed agents, retries, queues, observability), and **controls** (dashboards, evals).
- The shorthand: build with primitives, scale on infrastructure, run with control.
- A single `messages.create` call gives you full control over the model, response length, system prompt, and user input — enough to wire Claude into an existing feature like drafting help desk replies.
- The platform takes you from asking Claude questions to making Claude part of your product — and with managed agents, it can run your agents for you.