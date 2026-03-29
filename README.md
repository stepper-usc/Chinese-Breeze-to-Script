# GitHub Repository Layout

This repository is organized for multi-book annotated-script generation.

```text
repo/
  input/
    <book_id>/
      book.epub
      extracted/
        ...EPUB-extracted contents...
  output/
    <book_id>_annotated_script.md
  spec/
    README.md
    ANNOTATED_SCRIPT_SCHEMA.md
    INPUT_RECOMMENDATIONS.md
    PROMPT_TEMPLATE.md
    EDGE_CASES.md
    MARKDOWN_STYLE_GUIDE.md
    VALIDATION_CHECKLIST.md
    examples/
      chapter_01_example_output.md
      chapter_01_source_notes.md
```

Primary entry point: `spec/ANNOTATED_SCRIPT_SCHEMA.md`

Operational summary:
- `input/<book_id>/book.epub` is the canonical source of truth.
- `input/<book_id>/extracted/` is the operational readable fallback.
- Generate exactly one file per book: `output/<book_id>_annotated_script.md`.
- Use GitHub-hosted readable extracted files for actual parsing when connector/runtime access to the raw EPUB is limited.
