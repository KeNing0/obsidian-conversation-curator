# Example review-mode preview before write

This is an example of what the agent should show in the default review mode. It must not perform the write at this stage.

## Proposed operation

- Conversation scope: From the discussion of conversation capture through the final privacy checklist.
- Category: Knowledge management
- Target: `01_knowledge/Knowledge management.md`
- Operation: Update existing document
- Insertion point: After `## Local Markdown vaults`
- Sensitive data removed: One local username and one private vault path were replaced with generic placeholders.
- Needs verification: None

## Complete text to write

### Human-approved conversation deposits

A conversation-deposit workflow is different from automatic memory. It processes only material the user deliberately selects, prepares directly readable knowledge, and waits for approval before changing the knowledge base.

The preview must include the target document, insertion point, and complete proposed text. If the user changes the category or wording, the agent must generate a new complete preview and obtain confirmation again.

Long-lived category documents reduce note fragmentation. New material should be merged into an existing section when possible, while preserving conditions, reasoning, examples, and conflicts needed for later reading.

## Confirmation request

Do you confirm writing the complete preview above to `01_knowledge/Knowledge management.md`?
