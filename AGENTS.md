# Send to Other View — public repository guide

## Purpose and boundary

This is the public, user-facing repository for the compiled Send to Other View Notepad++ plugin. It intentionally contains the README, license, and release history—not private C++ source or developer-only material. Authoritative source and packaging live in sibling `SendToOtherView`.

## Release rules

- Do not copy private source, local configuration, developer notes, intermediates, or unrelated history here.
- Normal Git history should not contain duplicate release ZIPs; the README links to immutable/versioned GitHub release assets.
- A public release requires explicit user authorization plus verified x64/x86 packages, matching versions, SHA-256 hashes, root ZIP layout, release assets, and user-facing documentation.
- Keep compatibility claims evidence-based. Version 1.8.0 currently supports 32-bit and 64-bit Notepad++ 8.0+; there is no ARM64 artifact.
- Changes to release assets or GitHub releases are external writes and require explicit scope.

## Validation

Run `git diff --check`; verify README links and version history; download and hash release assets when validating a published release. Cross-check package hashes and DLL versions against the private repository's `AGENTS.md` and `dist` artifacts.

## Current state — 2026-09-18

- `main` is clean and synchronized with `origin/main` at `6c24b01` (`Use GitHub release assets for downloads`).
- Remote: `https://github.com/StephenWalker999/SendToOtherViewPUBLIC.git`.
- Release/tag `v1.8.0` exists; README points to its x64/x86 release assets.
- Release immutability was recommended but has not been confirmed.
