# Contributing

Contributions that improve classification, safe previews, conflict handling, portability, documentation, or privacy protections are welcome.

## Principles

- Preserve review mode as the default.
- Preserve explicit, per-request direct-write opt-in; never infer it from a general deposit request or persist it as a preference.
- Keep the Skill instruction-only unless deterministic code is clearly necessary.
- Do not add background capture, automatic recall, telemetry, or network dependencies to the core Skill.
- Keep `SKILL.md` focused and under 500 lines.
- Use fictional examples and generic paths.
- Do not include private notes, real conversation exports, credentials, or personal configuration.

## Development

1. Fork or clone the repository.
2. Make changes in `skills/obsidian-conversation-curator/`.
3. Test against a disposable fictional Markdown vault.
4. Verify that refusal, preview-only, revise-preview, confirm-write, and explicit direct-write paths all behave correctly.
5. Validate the Skill metadata and folder name.
6. Scan the complete Git diff and history for secrets and personal data.
7. Open a pull request explaining the behavior change and its privacy impact.

## Documentation

Keep `README.md` and `README.zh-CN.md` aligned when changing user-visible behavior, installation, or examples.

## Scope changes

Features such as semantic search, automatic session capture, cloud sync, API integrations, or memory recall materially change the privacy model. Propose them as separate optional projects or integrations rather than silently expanding the core Skill.
