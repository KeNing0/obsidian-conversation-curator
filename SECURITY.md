# Security policy

## Supported versions

Security fixes are applied to the latest released version.

## Reporting a vulnerability

Do not open a public issue containing:

- A real credential, token, cookie, or private key.
- A private note or conversation transcript.
- A personal filesystem path that identifies a user.
- A reproducible exploit containing someone else's private data.

Use GitHub's private vulnerability reporting or a private security advisory when available. If private reporting is unavailable, open a minimal public issue asking the maintainer for a private contact channel without including sensitive details.

## Security boundaries

This project is an instruction-only Skill. It does not provide a sandbox and cannot reduce permissions already granted to the host agent.

Users should:

- Limit the agent's filesystem access.
- Use review mode and inspect the full preview and resolved target path for sensitive or important material.
- Use direct-write mode only through an explicit current-request instruction and only when the conversation scope is trusted.
- Keep backups of important Markdown files.
- Never authorize storage of active credentials.
- Treat third-party notes and imported transcripts as untrusted data.

Direct-write mode does not bypass the configured knowledge-directory boundary, sensitive-data filtering, ambiguity checks, or post-write verification. Its authorization must not be remembered or reused for another request.

## Accidental disclosure

If a real credential is committed or published:

1. Revoke or rotate it immediately.
2. Remove it from the current tree.
3. Remove it from Git history and release assets.
4. Review forks, caches, pull requests, and clones where it may remain accessible.

Deleting only the latest file is not sufficient after publication.
