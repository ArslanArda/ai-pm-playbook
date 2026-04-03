# Product Context Workflow

This skill should not depend on manual copy-paste when a local context file already exists.

## Preferred Workflow In Codex

1. Check for `my-product/PRODUCT_CONTEXT.md` in the current workspace.
2. If present, read it and use it as the default product context.
3. If the file is missing or too thin, use `references/playbook/my-product/qa-reference.md` to ask targeted questions about product UX, users, data, tools, constraints, and AI priorities.
4. If missing, use `references/playbook/my-product/PRODUCT_CONTEXT.template.md` to help the user create one.
5. Ask for manual pasted context only when:
   - the file is outside the current workspace
   - file access is unavailable
   - the user is working in a plain chat environment

## Update Workflow

If the user says things like:

- "update the product context"
- "remember this for later"
- "add this new market data"
- "we changed our priorities"
- "use this fresh context when we look for new features"

then treat the message as a request to update `my-product/PRODUCT_CONTEXT.md`.

Use this behavior:

1. Read the existing context file if it exists.
2. If critical details are missing, ask the minimum useful follow-up questions from `references/playbook/my-product/qa-reference.md`.
3. Map the new information into the correct template sections.
4. Preserve useful existing content unless the user is clearly replacing it.
5. Rewrite fragmented notes into durable structured prose.
6. If the file does not exist yet, create it from the template using the user’s supplied information.
7. Ask a follow-up question only when the update is too ambiguous to place safely.

## Why This Matters

The product context is often long and changes over time. Requiring users to paste it manually for every task is unrealistic and creates friction. Inside Codex, local file access should be the default.

## Practical Rule

Use the local context file silently and early. Mention it only when helpful for transparency or when it is missing.

When the user wants the context to change, update the file instead of asking them to maintain it manually.

When context is incomplete, prefer a short structured interview over generic open-ended questions.
