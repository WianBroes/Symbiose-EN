# Skills — Index

Skills are procedure modules loaded on demand. Each folder contains a `SKILL.md` with the instructions.

## Available

| Skill | File | Description |
|-------|------|-------------|
| **import** | `import/SKILL.md` | Document import and indexing. Converts PDF, DOCX → markdown, preserves originals. |
| **export** | `export/SKILL.md` | Profile, framework, or backup export. Prepares a migration or publication. |
| **closure** | `closure/SKILL.md` | Session closure ritual. Macro-scan, traits, skills, TRANSFERT, snapshot. Triggered by "close", "we're done". |
| **dream** | `dream/SKILL.md` | Observation consolidation (append → compact). Triggered automatically every 10 closures, or manually by "do a dream". |
| **new-project** | `new-project/SKILL.md` | Create a new project folder following vault conventions (number, emoji, template, icon). Triggered by "new project", "add a folder", "create a project". |
| **update** | `update/SKILL.md` | Update `_SYSTEM/` from git. Checks, displays CHANGELOG diff, applies, migrates if necessary. Triggered by "update", "check update". |
| **mirror** | `mirror/SKILL.md` | FR→EN synchronization. Detects missing or outdated files, translates on demand via Claude, validates and commits to Symbiose-EN. Triggered by "mirror", "mirror check", "mirror [file]". |

## Usage

The AI loads a skill when the context calls for it. No automatic loading — progressive disclosure: only the description is visible, the content is read on demand.
