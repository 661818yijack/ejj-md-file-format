# EJJ MD File Format

EJJ MD is a draft text format for writing documents that people can read and
tools can validate. The first profile describes coding standards using YAML
front matter, Markdown prose, and optional Mermaid diagrams.

- [Draft specification](SPEC.md)
- [Standards entry schema](schema/standard-entry.schema.json)
- [Example rule with a diagram](examples/rust-style-format.md)
- [Example principle with a cross-reference](examples/rust-style-naming.md)

Each standards entry has a stable ID, a category, and a severity. Each assigned
check records where it happens, whether it blocks an action, and how it is
verified. The Markdown body holds the rationale and examples.
