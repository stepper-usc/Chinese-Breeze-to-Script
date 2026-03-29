# Prompt Template

Use this instruction when asking a future GPT model to generate an annotated script from this repository.

```text
Generate the annotated script for the directly provided book using the repository as the project source.

Instructions:
- Read `spec/ANNOTATED_SCRIPT_SCHEMA.md` first and follow it as the canonical spec.
- Use supporting files in `spec/` as needed.
- Identify the target book automatically from the directly provided files and/or the relevant book folder in the repository. Do not require the user to retype the book name if the target book is already clear from context or provided files.
- Match the target book to the correct `<BOOK_ID>` folder under `input/`.
- Treat `input/<BOOK_ID>/book.epub` as canonical.
- Treat `input/<BOOK_ID>/extracted/` as the readable fallback.
- If raw EPUB body text is not directly readable, continue with `input/<BOOK_ID>/extracted/`; do not stop.
- If any required part of the standardized input is missing, first create or complete it from the directly provided book before generation. This includes missing `input/<BOOK_ID>/`, missing `input/<BOOK_ID>/book.epub`, missing `input/<BOOK_ID>/extracted/`, or missing readable extracted content inside `input/<BOOK_ID>/extracted/`.
- Place the directly provided book into `input/<BOOK_ID>/book.epub` whenever that canonical file is missing.
- Create/populate `input/<BOOK_ID>/extracted/` whenever the readable fallback is missing or unreadable.
- Prefer exact-path reads of known files over weak repository-wide search.
- Do not treat failed folder browsing alone as proof that a standardized path is missing.
- Do not generate output from metadata alone.
- Do not assume every EPUB file/section is a story chapter.
- First classify each section as story chapter, mixed-content story section, or non-story section.
- Only transform story chapters and mixed-content story sections.
- Skip non-story sections entirely, except front matter needed for canonical character extraction.
- Parse mixed-content XHTML according to the schema: preserve story text, remove inline glossary markers, and exclude glossary/wordbank/comprehension and other non-story learner apparatus.
- Generate exactly one file:
  `output/<BOOK_ID>_annotated_script.md`
- Preserve original included story text exactly and in order.
- Do not rewrite, summarize, translate, simplify, or correct.
- Use canonical character names from front matter when available.
- Follow the markdown formatting rules in the spec.
- If repository write access exists, write the final file back into `output/<BOOK_ID>_annotated_script.md` rather than only returning a local artifact.
- Validate the result against `spec/VALIDATION_CHECKLIST.md` before finalizing.
```
