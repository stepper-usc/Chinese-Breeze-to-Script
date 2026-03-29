# Validation Checklist

Use this checklist before accepting an output file.

## Book mapping
- [ ] The selected `book_id` matches the output filename exactly.
- [ ] The output contains content from only one book.

## Input handling
- [ ] Raw EPUB body text was used directly only if it was actually readable.
- [ ] Otherwise the extracted readable fallback was used.
- [ ] Metadata, filenames, or folder structure were not mistaken for readable story content.

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

## Markdown format
- [ ] The output uses H1 chapter headings.
- [ ] The output uses `## Characters in this chapter`.
- [ ] The output uses `## Script`.
- [ ] Narration is formatted as bracketed standalone paragraphs.
- [ ] Dialogue is formatted as `Speaker: line`.
- [ ] Spacing is consistent and GitHub-friendly.
