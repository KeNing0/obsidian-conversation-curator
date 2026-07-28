# Example explicit direct-write request

## User request

```text
Use $obsidian-conversation-curator. For this request, do not show a preview
or ask for confirmation. Directly deposit the current conversation into my
Obsidian personal knowledge base. Infer the category if needed. After writing,
tell me the exact file and show me the complete content that was added.
```

## Example receipt after verification

- Mode: Direct write
- Conversation scope: From the explanation of local Markdown through the final backup recommendation.
- Category: Knowledge management
- Target: `01_knowledge/Knowledge management.md`
- Operation: Updated existing document
- Insertion point: After `## Local Markdown vaults`
- Sensitive data removed: One fictional local path was replaced with `/path/to/my-vault`.
- Verification: The target location was re-read successfully.

## Complete content added

### Maintaining a personal knowledge base from conversations

Conversation deposits should add durable conclusions to long-lived category documents instead of creating a separate note for every chat. When the source already contains a clear conclusion, preserve its wording and useful detail. When the source is exploratory, retain the resulting method together with the conditions, reasoning, exceptions, examples, commands, numbers, and links needed for later use.

Direct-write mode is appropriate when the conversation scope is trusted and the user explicitly asks to skip preview or confirmation for the current request. That authorization is not a permanent preference. Later deposits return to review mode unless the user opts into direct writing again.
