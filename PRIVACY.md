# Privacy model

Obsidian Conversation Curator is an instruction-only Agent Skill. It contains no service, telemetry, analytics, API client, database, bundled executable, or background process.

## Data processed

When invoked, the host agent may process:

- The conversation scope selected by the user.
- Filenames and headings in the configured knowledge directory.
- The minimum relevant Markdown content needed to select a category and merge the new knowledge.
- The complete target document immediately before preparing an update.

The Skill instructs the agent not to inspect unrelated vault folders, hidden directories, attachments, Obsidian workspace state, Git metadata, environment files, or credentials.

## Data written

The host agent may write only:

- In review mode, the exact Markdown content and target identified in the latest approved complete preview.
- In direct-write mode, only the conversation scope and write operation explicitly authorized by the current request.
- An existing category document or a focused new category document inside the configured knowledge directory.

Every write requires one of two forms of authorization:

1. Explicit approval referring to the latest complete preview.
2. An unambiguous instruction in the current request to write directly without preview, review, or confirmation.

Direct-write authorization applies only to that request. It is not stored as a preference and does not authorize later writes, background capture, or broader filesystem access.

## Data not collected

The Skill does not:

- Send content to a server controlled by this project.
- Store telemetry or analytics.
- Require an API key.
- Automatically scan, index, embed, synchronize, or upload a vault.
- Automatically capture conversations at session end.
- Automatically recall saved notes in later conversations.

The host agent provider may process prompts and files according to its own product terms and privacy settings. Review those settings separately.

## Threats and mitigations

### Overbroad filesystem access

The host agent may have permission to read more than the Skill needs. Configure the narrowest practical knowledge directory and review every permission request.

### Prompt injection inside notes

Markdown notes are treated as untrusted reference data. Instructions found inside notes must not be executed or allowed to override this Skill.

### Path traversal and symlink escape

The target must remain inside the configured knowledge directory. The agent must reject traversal paths and symlinks resolving outside that directory.

### Sensitive data in the conversation

Credentials and unnecessary personal data are removed by default before preview. Placeholders should be used instead of active secrets.

### Host model behavior

Agent behavior depends on the host product and model. Review mode is safer for sensitive or high-impact material. Direct-write mode is a deliberate convenience option, not a substitute for filesystem sandboxing, narrow permissions, post-write verification, and backups.

## Safe publishing

This repository must contain only fictional examples and generic paths such as `/path/to/my-vault`. Personal vault paths, real notes, conversation exports, screenshots, credentials, local configuration, and Git author email addresses must not be added.
