# Product Context Workflow

This skill should not depend on manual copy-paste when a local context file already exists.

## Preferred Workflow In Codex

1. Check for `my-product/PRODUCT_CONTEXT.md` in the current workspace.
2. If present, read it and use it as the default product context.
3. If missing, use `references/playbook/my-product/PRODUCT_CONTEXT.template.md` to help the user create one.
4. Ask for manual pasted context only when:
   - the file is outside the current workspace
   - file access is unavailable
   - the user is working in a plain chat environment

## Why This Matters

The product context is often long and changes over time. Requiring users to paste it manually for every task is unrealistic and creates friction. Inside Codex, local file access should be the default.

## Practical Rule

Use the local context file silently and early. Mention it only when helpful for transparency or when it is missing.
