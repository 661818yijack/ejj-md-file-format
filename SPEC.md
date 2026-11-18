# EJJ MD File Format 1

Status: draft.

An EJJ MD document combines YAML metadata with a Markdown body. This draft
defines a profile for catalogs of coding standards.

## Document layout

- Use UTF-8 and the `.md` extension. Readers accept LF and CRLF line endings.
- Start the document with a line containing exactly `---`. A second line containing
  exactly `---` ends the header. The lines between them are a single YAML 1.2 mapping.
- Use the YAML 1.2 Core schema for scalar resolution and restrict metadata to
  JSON-compatible values. Mapping keys must be unique strings. Anchors, aliases,
  explicit tags, and merge keys are outside this profile and must be rejected.
- Interpret everything after the closing delimiter as CommonMark Markdown.
  A later `---` line belongs to the body.
- A fenced block with the info string `mermaid` contains Mermaid source. A
  renderer may render it as a diagram. A plain Markdown reader can display it
  as code.

## Standards metadata

The [JSON Schema](schema/standard-entry.schema.json) defines the allowed fields,
required fields, and values. A document declares its format version in
`format_version`. Readers implementing this draft accept version `1`.

| Field | Meaning |
| --- | --- |
| `id` | Stable identifier for the entry. Keep it when moving or renaming a file. |
| `kind` | `rule` for a scoped expectation or `principle` for a guideline that calls for judgment. |
| `category` | One of the five standards categories listed in the schema. |
| `severity` | `must` requires an explicit exception for deviations, `should` sets an expectation with justified deviations, and `consider` calls for evaluation where relevant. |
| `checks` | Assigned checks. An empty list represents an unassigned entry. |
| `references` | Optional list of IDs of related entries in the same catalog. |

A check records three attributes.

| Field | Values |
| --- | --- |
| `enforcement` | `process`, `hook`, `ci`, or `human-review`. These identify where the check happens. |
| `effect` | `blocking` prevents the associated action when the check fails. `advisory` reports findings. |
| `verifiability` | `deterministic`, `ai-judgment`, or `human-judgment`. These identify how compliance is assessed. |

Severity applies to the entry. Enforcement, effect, and verifiability apply to
each check individually.

## Catalog validation

A validator first checks the header syntax and then applies the JSON Schema to
the parsed metadata. Catalog validation also checks that each ID is unique and
that every ID in `references` resolves to an entry. These checks operate across
the whole catalog.

The Markdown file is the editable source. JSON and XML exports can be generated
from it. Export mappings are open for a later draft.
