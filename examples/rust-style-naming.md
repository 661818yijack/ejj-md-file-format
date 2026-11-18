---
format_version: 1
id: rust.style.naming
kind: principle
category: code-style
severity: should
checks:
  - enforcement: human-review
    effect: advisory
    verifiability: human-judgment
references:
  - rust.style.format
---

# Choose names that communicate intent

Prefer names that describe what a function does in the vocabulary of the
project. Use a short name when the surrounding code supplies the context.

## Example

In an inventory module, `reserve_stock` describes a purpose more clearly than
`process_item`.
