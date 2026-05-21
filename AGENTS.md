# Personal Agent Rules

These rules are global working agreements for Peter's repositories.

## Default Behaviour

- Keep the working tree clean. Check `git status -sb` before implementation.
- Prefer doing the work directly when tools and permissions allow it.
- Treat `im-lazy` behaviour as the default: act instead of giving instructions when the agent can safely do the task.
- Ask for confirmation before destructive actions, spending money, exposing secrets, or changing external services.
- Use clean code over backwards compatibility while a project is explicitly in MVP mode.
- Preserve user data. Silent user data loss is a serious bug.
- Prefer local Markdown issues unless the repo explicitly uses GitHub Issues.
- Commit and push completed repo changes when the user asks for implementation work.
- When ideas, terms, or instructions overlap, prefer the one with the most recent documented provenance. Current user instructions, safety rules, and explicit repo instructions still take precedence.

## Communication

- Be concise by default.
- Use caveman-style brevity unless clarity or safety needs fuller prose.
- End every response with a suggested next step.
- When giving setup/dashboard instructions, treat Peter like he is five:
  - include direct links
  - give exact values
  - one clear path
  - do not say "go to the dashboard" without a link
- For reusable workflows, prefer local skills over ad hoc repeated instructions.

## Grilling Sessions

When Peter asks to be grilled:

- Ask one question at a time.
- Provide the recommended answer with each question.
- Wait for Peter's answer before continuing.
- If code/docs can answer the question, inspect them instead of asking.
- Capture resolved decisions in docs or issues when useful.

## Implementation Notes

- Use `rg`/`rg --files` for search.
- Use `apply_patch` for manual file edits.
- Do not revert user changes unless explicitly asked.
- Do not leave needed dev servers running unmanaged without saying so.
- For frontend-visible changes, build and restart the local server when practical.
