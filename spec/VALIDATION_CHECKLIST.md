# Validation Checklist

Use this checklist before accepting an output file.

## Book mapping
- [ ] The selected `book_id` matches the output filename exactly.
- [ ] The output contains content from only one book.

## Input handling
- [ ] Raw EPUB body text was used directly only if it was actually readable.
- [ ] Otherwise the extracted readable fallback was used.
- [ ] Metadata, filenames, or folder structure were not mistaken for readable story content.

## Bootstrap handling
- [ ] If any required standardized input was missing, the structure was created or completed first.
- [ ] `input/<BOOK_ID>/book.epub` was created from the directly provided book when that canonical file was missing.
- [ ] `input/<BOOK_ID>/extracted/` was created when that folder was missing.
- [ ] Readable extracted content was added when the fallback content was missing.
- [ ] Readable extracted content was claimed only if actual readable body text was produced.

## Section selection
- [ ] Each section was classified as story chapter, mixed-content story section, or non-story section.
- [ ] Non-story sections were skipped entirely except front matter needed for character extraction.
- [ ] Mixed-content story sections were filtered rather than rejected.

## Apparatus filtering
- [ ] Glossary superscript markers were removed.
- [ ] Glossary definition entries were removed.
- [ ] Comprehension boxes were removed.
- [ ] Other non-story learner apparatus was removed.

## Fidelity
- [ ] All included narrative text is present.
- [ ] Included narrative order is preserved.
- [ ] No dialogue was rewritten.
- [ ] No narration was paraphrased.
- [ ] No translation or summary was introduced.

## Attribution
- [ ] Every dialogue line has a speaker label.
- [ ] Canonical front-matter names were used when available.
- [ ] Grounded role labels were used for unnamed speakers when justified.
- [ ] Uncertainty was marked conservatively when needed.
- [ ] Each chapter character list includes only speakers used in that chapter.

## Repository workflow
- [ ] Exact-path file reads were preferred when repository browsing was weak.
- [ ] Inability to browse the tree was not confused with inability to read a known path.
- [ ] The final output was written back to the repository when write access was available.

## Markdown format
- [ ] The output uses H1 chapter headings.
- [ ] The output uses `## Characters in this chapter`.
- [ ] The output uses `## Script`.
- [ ] Narration is formatted as bracketed standalone paragraphs.
- [ ] Dialogue is formatted as `Speaker: line`.
- [ ] Spacing is consistent and GitHub-friendly.
