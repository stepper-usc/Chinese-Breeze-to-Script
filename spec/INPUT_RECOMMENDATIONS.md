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

## Bootstrap rule when only a book is provided
If the user provides only a book file and the repository does not yet contain the needed structure, create the default structure for that book before generating output.

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
2. Create `input/<book_id>/book.epub` from the provided EPUB.
3. Create `input/<book_id>/extracted/` and populate it with the best readable extraction available in the current environment.
4. Prefer XHTML/HTML extracted from the EPUB package. If that is not available, use the best structured readable fallback available.
5. Do not pretend extraction succeeded if only metadata or filenames were obtained.
6. After bootstrap, treat the new `input/<book_id>/` as the normal transformation unit.
