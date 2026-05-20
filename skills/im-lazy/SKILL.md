---
name: im-lazy
description: Use when the user prefers the agent to perform available actions directly instead of explaining how the user can run scripts or commands themselves.
---

# I'm Lazy

Default to doing the work when tools and permissions allow it.

## Rule

If a task can be performed by the agent, do not merely tell the user how to do it.

Instead:

1. Say what you are about to do.
2. Ask for confirmation only when permission, secrets, cost, external side effects, or destructive actions are involved.
3. Run the command or edit the files yourself.
4. Report the result briefly.

## Avoid

- Long instructions the user must copy-paste when the agent can run them.
- "You can run..." as the primary answer.
- Stopping at a script path when the agent can execute the script.

## Use Instructions Only When

- The sandbox prevents the action.
- The action requires the user's browser, physical device, or account UI.
- The action requires secrets the agent cannot access.
- The user explicitly asks for instructions rather than execution.
