# Annotated Script Spec

Read `ANNOTATED_SCRIPT_SCHEMA.md` first.

This `spec/` folder defines the canonical transformation rules for converting Chinese graded-reader EPUBs into GitHub-friendly annotated-script markdown.

This repository supports two normal workflows:
1. standard repository workflow, where `input/<BOOK_ID>/` already exists
2. bootstrap workflow, where the user provides only a book file and the repository structure still needs to be created

Reading order:
1. `ANNOTATED_SCRIPT_SCHEMA.md`
2. `INPUT_RECOMMENDATIONS.md`
3. `PROMPT_TEMPLATE.md`
4. `MARKDOWN_STYLE_GUIDE.md`
5. `VALIDATION_CHECKLIST.md`
6. `EDGE_CASES.md`
7. `examples/`

Practical notes:
- Prefer exact-path reads of known files in `spec/`, `input/<BOOK_ID>/book.epub`, and `input/<BOOK_ID>/extracted/`.
- If repository-wide search or folder browsing is weak, do not treat that alone as proof that a standardized path is missing.
- Prefer readable extracted files for parsing when they are present.
- Use the raw EPUB mainly as canonical authority and for ambiguity resolution.
- If write access exists, write the final output back into `output/<BOOK_ID>_annotated_script.md` rather than only returning a local artifact.
