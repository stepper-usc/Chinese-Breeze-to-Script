# Prompt Template Addendum for GitHub Use

Add these rules when running the repository workflow through a GitHub connector:

- Prefer exact-path fetches for known files in `spec/`, `input/<BOOK_ID>/book.epub`, and `input/<BOOK_ID>/extracted/`.
- If folder browsing is unreliable, do not treat that alone as proof a standardized path is absent.
- If the directly provided book file clearly identifies the target, infer `<BOOK_ID>` from that file and continue.
- Prefer readable extracted files for parsing when they are present.
- Use the raw EPUB mainly for authority, verification, and ambiguity resolution.
- If repository write access exists, commit the final markdown to `output/<BOOK_ID>_annotated_script.md`.
- If repo write access does not exist, report that limitation explicitly.
