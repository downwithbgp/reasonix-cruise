# Spec artifacts

This directory holds planning artifacts for medium and large tasks.

## When to use

- **Medium tasks** (new feature touching 2+ files, API changes): write `spec/<slug>/tasks.md`
- **Large tasks** (architectural changes, new binaries): write `spec/<slug>/` with requirements + design + tasks

Skip spec files for trivial and small changes — they pollute the repo without value.

## Convention

- One directory per task, named with a short kebab-case slug (e.g. `spec/packet-reordering/`)
- Medium: `tasks.md` only
- Large: `requirements.md`, `design.md`, `tasks.md`
- Run `/review` on the spec before implementing — catches planning errors when they're cheapest to fix
- Commit specs alongside the implementation; they document *why* decisions were made
