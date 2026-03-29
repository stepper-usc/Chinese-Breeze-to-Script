# ANNOTATED_SCRIPT_EPUB_TRANSFORMATION_SCHEMA

## Status
Canonical project reference. Follow this file first.

## Purpose
Convert each book into a GitHub-friendly markdown annotated script for reading-group use.

This is a constrained structural transformation, not a rewrite.

## Repository contract

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

Interpretation:
- `input/<book_id>/book.epub` = canonical source of truth for that book
- `input/<book_id>/extracted/` = operational readable fallback for that book
- `output/<book_id>_annotated_script.md` = final deliverable for that book
- `<book_id>` = stable book identifier and folder name

## Output generation mapping
For each `input/<book_id>/`, generate exactly one corresponding output file:

`output/<book_id>_annotated_script.md`

Rules:
1. The output filename must match the input folder name exactly.
2. Do not mix content from multiple books into one output file.
3. If multiple books exist, treat each `input/<book_id>/` as an independent transformation unit.

## Input policy
### Source of truth
Preferred canonical input: the original `.epub` file.

### Operational readable fallback
Required fallback: structured extracted content derived from the EPUB, preferably XHTML/HTML extracted from the book package.

### GitHub-first usage rule
For GitHub-hosted repositories, store both:
- the raw EPUB as the archival canonical source
- the extracted readable files as the operational parsing source

Do not rely on raw EPUB body access alone.

### Input priority
Use the highest available readable source in this order:
1. Raw EPUB body text, if actually readable in the current environment
2. Extracted XHTML/HTML in `input/<book_id>/extracted/`
3. Structured extracted markdown/text preserving chapter and apparatus boundaries

If the raw EPUB is present but not directly readable, keep treating it as canonical and use the extracted folder operationally.

### Bootstrap policy when standardized input is missing or incomplete
If the user provides a book file and any required part of the standardized input is missing, first create or complete the default repository structure for that book before transformation.

Treat all of the following as requiring bootstrap or completion before generation:
- `input/<book_id>/` does not exist
- `input/<book_id>/book.epub` is missing
- `input/<book_id>/extracted/` is missing
- `input/<book_id>/extracted/` exists but has not been populated with actual readable extracted content

Bootstrap requirements:
1. Infer `<book_id>` conservatively from the directly provided book.
2. Place the directly provided book into `input/<book_id>/book.epub` when that canonical file is missing.
3. Create `input/<book_id>/extracted/` when it is missing.
4. Populate `input/<book_id>/extracted/` with the best readable extraction available in the current environment when readable extracted content is missing.
5. Do not claim that readable extraction exists unless actual readable body text was produced.
6. After bootstrap or completion, treat `input/<book_id>/` as the canonical transformation unit.

### Connector workflow rule
When using a GitHub connector or other mediated repository tool:
- prefer exact-path reads of known files over weak repository-wide search
- do not treat failed folder enumeration alone as proof that a standardized path is missing
- keep these failure modes distinct: cannot browse the tree, cannot read a known path, cannot write back to the repository
- if repository write access exists, write the final output back to `output/<book_id>_annotated_script.md`

## Scope
### Include
- actual story chapters
- mixed-content story sections that contain narrative text plus learner apparatus
- chapter titles
- narration
- dialogue
- front-matter character names for canonical speaker attribution
- story-internal embedded items such as letters, signs, or messages if they are part of the narrative

### Exclude
Treat the following as non-story material unless explicitly requested otherwise:
- character-list pages after character extraction is complete
- place-list pages
- introductions and publisher prefatory material
- vocabulary pages
- glossary/wordbank sections
- comprehension/review questions
- exercises
- answer keys
- appendices
- navigation pages
- duplicated boilerplate
- decorative image-only material with no narrative text
- glossary superscript markers such as `[1]`, `[2]` attached to story words
- glossary definition entries
- “check your understanding” boxes

## Section selection rule
Do not assume every EPUB file, section, or “chapter” is a story chapter.

First classify each section as one of:
1. story chapter
2. mixed-content story section
3. non-story section

Only transform story chapters and mixed-content story sections into script output.

Skip non-story sections entirely, except when front matter is needed for canonical character extraction.

## Mixed-content XHTML policy
A chapter XHTML file may contain a mixture of:
- chapter heading
- story paragraphs
- inline glossary markers
- underlined proper nouns
- images
- comprehension boxes
- glossary/wordbank entries
- navigation links

This is normal and not a parsing failure.

Transformation rule for mixed-content story sections:
1. Keep the chapter heading, after removing learner-apparatus markers.
2. Keep story paragraphs.
3. Keep narrative text order exactly.
4. Remove inline glossary markers from headings and story paragraphs.
5. Ignore purely decorative images unless the user explicitly wants image descriptions.
6. Exclude comprehension boxes.
7. Exclude glossary/wordbank entries.
8. Exclude navigation/support links.
9. Preserve the underlying story wording otherwise exactly.

## Core invariants
1. Preserve all included narrative text.
2. Preserve included narrative order exactly.
3. Do not paraphrase.
4. Do not translate.
5. Do not summarize.
6. Do not silently rewrite punctuation or wording.
7. Do not add interpretive stage directions.
8. Only add the structural formatting allowed by this schema.
9. If uncertain, choose the most conservative transformation.
10. When excluding apparatus, exclude it consistently by rule.
11. Do not invent content missing from the readable source.

## Canonical character extraction
Use the front-matter character list when available.

Rules:
1. Extract Chinese names exactly as written.
2. Use the Chinese name as the canonical speaker label.
3. Ignore pinyin and English descriptions for speaker-label purposes.
4. Ignore place lists.
5. Do not invent aliases.

## Dialogue handling
1. Detect dialogue primarily from quotation marks.
2. Remove only the outer quotation marks in final script lines.
3. Preserve all internal dialogue text exactly.
4. Reporting clauses remain narration unless quoted.

Example:
- Source: `他说：“你来了。”`
- Output:
  - `[他说：]`
  - `某人: 你来了。`

## Narration handling
1. Anything not classified as dialogue defaults to narration.
2. Wrap narration in square brackets.
3. Preserve narration text exactly.

Example:
- Source: `他走进房间。`
- Output: `[他走进房间。]`

## Speaker attribution
Attribution priority:
1. explicit local attribution
2. immediate nearby narrative context
3. stable alternating turns in a local exchange
4. scene continuity
5. canonical character-list compatibility

If still uncertain, mark ambiguity conservatively rather than inventing certainty.

Allowed ambiguity labels:
- `[可能是X]:`
- `[说话者不明]:`

## Per-chapter character list
At the start of each transformed chapter, include only speakers who actually speak in that chapter.

Ordering:
1. canonical named speakers
2. other named speakers
3. minor role-based speakers

Do not include silent or merely mentioned characters.

## Output schema
Use this structure exactly:

```text
# <chapter title>

## Characters in this chapter

- <character_1>
- <character_2>

## Script

[<narration block 1>]

<speaker_label_1>: <dialogue block 1>

[<narration block 2>]

<speaker_label_2>: <dialogue block 2>
```

## Markdown policy
The output must be GitHub-friendly markdown.

Required:
- one H1 chapter heading per chapter section
- `## Characters in this chapter`
- `## Script`
- bracketed narration paragraphs
- `Speaker: line` dialogue format

Forbidden in final output:
- inline HTML
- copied EPUB anchors
- copied footnote/glossary links
- markdown tables
- explanatory commentary

## Validation rules
Before finalizing, verify:
1. the selected `book_id` matches the output filename
2. only the selected book’s content appears in the output
3. non-story sections were skipped entirely
4. mixed-content story sections were filtered correctly
5. glossary markers were removed
6. glossary definitions were removed
7. comprehension boxes were removed
8. included narrative text is preserved and in order
9. no rewriting, translation, or summary was introduced
10. every dialogue line has a speaker label
11. the chapter character list includes only speakers used in that chapter
12. bootstrap actions were completed correctly when the repository initially lacked the book structure
13. the final output was written back to the repository when write access was available

## Failure modes
Invalid output includes:
- generating from metadata alone
- treating all EPUB sections as story chapters
- including glossary/comprehension material in the script
- omitting included narrative text
- rewriting the story text
- mixing content from multiple books
- output filename not matching the input folder name
- claiming a bootstrap extraction succeeded when no readable extracted text was produced
