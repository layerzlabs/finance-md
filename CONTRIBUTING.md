# Contributing to FINANCE.md

FINANCE.md is an open standard, currently a **0.1 draft**. Field names, defaults and validation rules may still change before a 1.0 is cut — early input is exactly what we need.

## Welcome contributions

- **New examples** under `examples/` (a sector, a deal type, a regulatory regime — anything that exercises the format in a way the four existing examples don't).
- **Spec clarifications** in `SPEC.md` when something is ambiguous in practice.
- **Schema fixes** in `schema/finance-md.schema.yaml` when validation lets through (or rejects) something it shouldn't.
- **Tool integrations** — pointers to how an editor, agent runtime or modeling tool consumes a `FINANCE.md`, added to the README.

If you're considering a **breaking change** to the schema or to a required field, please open a GitHub Discussion or an issue first so we can align before you spend time on a PR.

## Workflow

1. Fork the repo and create a branch from `main`.
2. Make your change. Keep diffs focused — one logical change per PR.
3. If you're adding or modifying an example, make sure its YAML front matter validates against `schema/finance-md.schema.yaml`. Extract the front matter (everything between the first two `---` lines) into a temporary YAML file and run it through any JSON Schema validator that supports draft 2020-12 (`ajv-cli`, `check-jsonschema`, …). A small extraction helper will likely land in `scripts/` later.
4. Open a PR against `main`. The PR template will prompt for a short summary and a test plan.

## Commit style

Short, imperative present tense. Conventional Commits prefixes are welcome but not required:

```
feat: add infrastructure concession example
fix(schema): allow empty glossary
docs: clarify EBITDA section in SPEC
```

## Sign-off (DCO)

By submitting a PR, you certify that your contribution complies with the [Developer Certificate of Origin](https://developercertificate.org/). Add a `Signed-off-by: Your Name <you@example.com>` line to each commit with `git commit -s`. This is currently encouraged, not enforced — we may turn it into a required check before 1.0.

## License

FINANCE.md is MIT-licensed. Contributions are accepted under the same license.

## Questions

Open a GitHub Discussion for design questions, a GitHub Issue for concrete bugs or proposals.
