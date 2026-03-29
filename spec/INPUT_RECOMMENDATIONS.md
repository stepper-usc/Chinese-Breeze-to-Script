# Input Recommendations

## Repository layout

```text
repo/
  input/
    <book_id>/
      book.epub
      extracted/
  output/
    <book_id>_annotated_script.md
  spec/
    ...
```

## Recommended storage policy
For each book, keep both:
1. `input/<book_id>/book.epub` as the canonical source of truth
2. `input/<book_id>/extracted/` as the operational readable fallback

## Preferred extracted form
Best fallback: the EPUB unpacked into native XHTML/HTML and related files, preserving chapter boundaries, front matter, glossary sections, and hyperlink structure.

## GitHub usage rule
GitHub is best used for text-readable project files.

Recommended:
- store specs as markdown
- store extracted readable chapter files in the repository
- keep raw EPUBs as archival canonical inputs

Do not assume the runtime can unpack or read raw EPUB bodies directly just because the file exists in the repository.

## Operational rule
- Prefer the raw EPUB for truth and discrepancy resolution.
- Use `input/<book_id>/extracted/` for actual parsing when raw EPUB body text is not directly readable.
- Do not generate output from filenames, metadata, or folder structure alone.

## Bootstrap rule when standardized input is missing or incomplete
If the user provides a book file and the repository does not yet contain the full standardized input for that book, create or complete that structure before generating output.

This includes any case where one or more of the following are missing:
- `input/<book_id>/`
- `input/<book_id>/book.epub`
- `input/<book_id>/extracted/`
- readable extracted content inside `input/<book_id>/extracted/`

Expected bootstrap target:

```text
input/
  <book_id>/
    book.epub
    extracted/
output/
  <book_id>_annotated_script.md
```

Bootstrap requirements:
1. Infer `<book_id>` from the directly provided book as conservatively as possible.
2. Place the directly provided EPUB into `input/<book_id>/book.epub` whenever that canonical file is missing.
3. Create `input/<book_id>/extracted/` whenever it is missing.
4. Populate `input/<book_id>/extracted/` with the best readable extraction available in the current environment whenever readable extracted content is missing.
5. Prefer XHTML/HTML extracted from the EPUB package. If that is not available, use the best structured readable fallback available.
6. Do not pretend extraction succeeded if only metadata or filenames were obtained.
7. After bootstrap or completion, treat `input/<book_id>/` as the normal transformation unit.
