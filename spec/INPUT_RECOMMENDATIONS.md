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
1. `input/<book_id>/book.epub` as canonical source of truth
2. `input/<book_id>/extracted/` as operational readable fallback

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
