# Source Manifest

This repository is intended to be portable. Runtime skill execution must not depend on external crawl folders, local mirrors, original books, webpages, or machine-local paths.

Each skill stores its portable source summary at:

- `skills/<skill-name>/references/source-notes.md`

The `sourceFiles` fields in `manifest.json` and each `audit.json` point to those local notes. Original source identifiers, when relevant, have been compressed into portable summaries and are not required for execution.
