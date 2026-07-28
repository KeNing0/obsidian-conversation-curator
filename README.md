# Obsidian Conversation Curator

[English](README.md) | [简体中文](README.zh-CN.md)

An Agent Skill for turning selected AI conversations into directly readable personal knowledge and maintaining long-lived category documents in an Obsidian vault.

It is designed for people who want to build a personal knowledge base they can browse and reuse, without turning every conversation into a fragmented note or an automatic memory system.

## What makes it different

- **Two deliberate write modes:** review the complete proposed text by default, or explicitly request direct writing for a single task when you do not need a preview.
- **One category, one living document:** it updates an existing topic document instead of creating a new note for every conversation.
- **No over-summarization:** conclusions that are already clear are preserved; reasoning, conditions, examples, commands, numbers, links, and exceptions remain when they matter.
- **No forced template:** the skill does not require YAML, tags, tasks, dates, or a fixed note structure.
- **Privacy-first:** it removes secrets and unnecessary personal data by default and reads only what is necessary inside the configured knowledge directory.
- **No separate API:** it uses the model and filesystem tools already provided by your agent. It has no server, embeddings, database, background service, or model API key.

## Good use cases

Use this skill when you want to:

- Preserve the conclusions from a long research or learning conversation.
- Add a newly learned procedure to an existing technical knowledge document.
- Merge an investment, product, writing, travel, health, or study discussion into the relevant topic file.
- Store a decision together with its reasoning, trade-offs, conditions, and exceptions.
- Turn selected messages, rather than an entire chat, into durable reference material.
- Ask the agent to infer the right category when you do not know where the knowledge belongs.
- Preview a possible knowledge-base update without saving anything yet.
- Explicitly deposit routine material directly when you do not need to review it first.

This skill is **not** intended for:

- Automatically saving every conversation.
- Replaying or recalling old notes in future chats.
- Building a RAG system, vector database, or semantic search service.
- Backing up an Obsidian vault.
- Syncing notes between devices.
- Keeping raw chat transcripts as one file per session.

## How it works

1. You tell the agent which conversation or messages to preserve.
2. The agent selects review mode by default. It selects direct-write mode only when the current request explicitly says to skip preview, review, or confirmation.
3. You optionally name a knowledge category.
4. The agent checks only the relevant Markdown documents in your configured knowledge directory.
5. It updates a suitable category document or prepares a focused new one.
6. In review mode, you see and approve the complete proposed change. In direct-write mode, the agent proceeds without a routine pre-write review.
7. The agent makes a minimal edit, verifies the saved result, and reports what changed.

Direct-write permission applies only to the current request. It does not become a permanent setting, authorize background capture, or weaken privacy and path checks.

## Requirements

- Install the Obsidian desktop app from the official [Obsidian download page](https://obsidian.md/download).
- Create or open a local Obsidian vault.
- Use Codex or another compatible agent that can read and edit local Markdown files.

No separate model API, API key, server, database, or Obsidian plugin is required. Obsidian does not need to remain open while the agent edits the vault's Markdown files.

## Installation

### The easiest way: ask Codex to install it

Send this message to Codex:

```text
Please install the obsidian-conversation-curator Skill from
https://github.com/KeNing0/obsidian-conversation-curator/tree/main/skills/obsidian-conversation-curator
as a user-level Skill. After installing it, tell me how to invoke it.
Do not read or modify my vault during installation.
```

If your Codex environment exposes the built-in installer, you can also start the request with:

```text
Use $skill-installer to install obsidian-conversation-curator from
https://github.com/KeNing0/obsidian-conversation-curator/tree/main/skills/obsidian-conversation-curator
```

### Manual installation for Codex

Clone or download this repository, then copy the complete skill folder:

```bash
mkdir -p ~/.agents/skills
cp -R skills/obsidian-conversation-curator ~/.agents/skills/
```

For a repository-scoped installation:

```bash
mkdir -p .agents/skills
cp -R /path/to/obsidian-conversation-curator/skills/obsidian-conversation-curator .agents/skills/
```

Some existing Codex installations also discover user skills from `~/.codex/skills/`. If your setup already uses that location, copy the same folder there.

Restart the agent if the new skill does not appear immediately.

### Claude Code

Copy the skill folder to the user or project skill directory:

```bash
# User-level
mkdir -p ~/.claude/skills
cp -R skills/obsidian-conversation-curator ~/.claude/skills/

# Project-level
mkdir -p .claude/skills
cp -R skills/obsidian-conversation-curator .claude/skills/
```

Invoke it as `/obsidian-conversation-curator` where slash-command skill invocation is supported, or ask Claude to use the installed skill by name.

### Other agents

This project follows the open [Agent Skills specification](https://agentskills.io/specification). For another compatible agent, copy `skills/obsidian-conversation-curator/` into that agent's documented skills directory. The agent must be able to read and edit local Markdown files.

Tool names and permission screens vary by agent. Review mode remains the default. Direct writing is allowed only when the current request explicitly asks to skip preview or confirmation.

## First-time setup

The skill deliberately contains no personal paths. On first use, tell the agent:

1. Where your Obsidian vault is.
2. Which folder contains your long-lived category documents.

For example:

```text
Use $obsidian-conversation-curator.
My Obsidian vault is at /path/to/my-vault.
My knowledge-category folder is 01_knowledge.
Use these paths for this request only.
Do not write anything until I approve the complete preview.
```

If you want the paths to persist, put them in your agent's trusted project instructions. Do not publish that personal configuration with this Skill.

## Everyday usage

### 1. You already know the category

```text
Use $obsidian-conversation-curator to deposit the current conversation
into my "AI tools" knowledge document. Show me the complete text first.
```

### 2. Let the agent choose the category

```text
Use $obsidian-conversation-curator to preserve the useful knowledge
from this conversation. I have not chosen a category, so check my existing
knowledge documents and recommend the best destination. Preview only for now.
```

### 3. Write directly without a pre-write review

Use direct-write mode only when you already trust the scope and want the deposit completed immediately:

```text
Use $obsidian-conversation-curator. For this request, do not show a preview
or ask for confirmation. Directly deposit the current conversation into my
Obsidian personal knowledge base. Infer the category if needed. After writing,
tell me the exact file and show me the complete content that was added.
```

You can also specify the destination:

```text
Use $obsidian-conversation-curator to write this discussion directly to my
"Knowledge management" document. No preview or second confirmation is needed
for this request. Preserve the detailed conclusions and report the result.
```

Phrases such as `write directly`, `no preview`, `no review`, or `no confirmation` opt in for that request only. A general request such as “save this conversation” still uses review mode.

### 4. Save only selected material

```text
Use $obsidian-conversation-curator, but process only the discussion beginning
with "Why local Markdown is enough" and ending with the security checklist.
Ignore the earlier setup conversation.
```

### 5. Preserve detailed reasoning

```text
Deposit this discussion into "Product decisions".
Keep the alternatives, rejection reasons, conditions, and risks.
Do not turn it into a short executive summary.
```

### 6. Revise before saving

```text
Do not write yet. Change the proposed category to "Knowledge management",
keep the second example in full, and show me the complete preview again.
```

After the updated preview looks right:

```text
Confirm write. Apply exactly the latest preview.
```

### 7. Split multiple topics

```text
This conversation contains both a GitHub publishing workflow and an Obsidian
privacy checklist. Prepare separate previews for the appropriate category
documents and do not write either one until I approve them.
```

### 8. Cancel safely

```text
Cancel this deposit. Do not modify any files.
```

## What review-mode approval should look like

The agent's preview should tell you:

- Which part of the conversation it used.
- Which category it selected.
- The target document and whether it already exists.
- Where the new content will be inserted.
- The complete text to be written.
- Which secrets or personal details were removed.
- Which statements still need verification.

A vague response such as “looks okay” should not be treated as approval if the target or text is ambiguous. Use a clear response such as:

```text
Confirm writing the latest preview to the AI tools document.
```

## Privacy and permissions

The Skill itself:

- Contains no personal vault path.
- Makes no network requests.
- Requires no API key.
- Runs no bundled scripts.
- Does not index the whole vault.
- Does not automatically capture or recall conversations.

Every write still requires one of two forms of authorization: approval of the latest complete preview, or an explicit direct-write instruction in the current request. However, your host agent may have broad filesystem permissions. Review the agent's permission request and keep the configured knowledge directory as narrow as practical. See [PRIVACY.md](PRIVACY.md) for the full threat model.

## Repository structure

```text
skills/obsidian-conversation-curator/
├── SKILL.md
└── agents/
    └── openai.yaml
```

Human-facing documentation and fictional examples remain at the repository root and are not required at runtime.

## Compatibility

- Obsidian desktop with a local Markdown vault.
- Codex and other agents that support the Agent Skills specification and local file access.

Obsidian must be installed for the intended personal-knowledge-base workflow, but it does not need to remain open. The agent edits the vault's underlying Markdown files.

## Limitations

- Classification and writing quality depend on the host model.
- Very large category documents may require more reading time and context.
- Filesystem approval behavior varies by agent.
- This skill is not a backup system. Keep normal versioned backups of important notes.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md).

## Security

Do not open a public issue containing a real secret or private note. See [SECURITY.md](SECURITY.md).

## License

MIT. See [LICENSE](LICENSE).
