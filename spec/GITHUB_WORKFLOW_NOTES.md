# GitHub Workflow Notes

Use exact-path reads for known files.

If repository-wide search or folder browsing is weak, do not assume standardized paths are missing.

When `input/<BOOK_ID>/extracted/` exists and is readable, use it as the primary parsing source. Use `book.epub` for authority and verification.

Keep these failure modes separate:
- cannot browse the repo tree
- cannot read a known file path
- cannot write back to the repo

If write access exists, commit the finished file to `output/<BOOK_ID>_annotated_script.md` rather than only returning a local artifact.
