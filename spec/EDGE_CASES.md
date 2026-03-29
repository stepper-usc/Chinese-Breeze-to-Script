# Edge Cases

## 1. Mixed-content chapter XHTML
A chapter XHTML file may contain story text plus glossary markers, images, comprehension boxes, and glossary entries.

Rule:
- keep the story text
- remove inline glossary markers
- exclude comprehension blocks
- exclude glossary entries
- preserve story order exactly

## 2. Whole non-story sections
Some EPUB sections may be entirely non-narrative, such as introductions, character lists, vocabulary pages, exercises, or answer keys.

Rule:
Classify these as non-story sections and skip them entirely, except front matter needed for canonical character extraction.

## 3. Glossary link markers inside text
Example source: `死[1]了`

Rule:
Remove the marker and keep the surrounding story text unchanged.

Output: `死了`

## 4. Heading contamination by glossary markers
A chapter title may be interrupted by glossary markers.

Rule:
Remove the markers and preserve the clean heading text.

## 5. Unnamed speaker identified by narration
If dialogue appears first and nearby narration identifies the speaker indirectly, use the grounded role label.

Example preferred label: `打电话的男人:`

## 6. Proper nouns visually underlined in EPUB
Rule:
Preserve the text, not the underline styling.

## 7. Decorative images between paragraphs
Rule:
Ignore the image and preserve surrounding text order.

## 8. Malformed quotation extraction
Rule:
Use the smallest possible repair needed to classify speech. Do not rewrite spoken content.

## 9. Internal thought vs spoken dialogue
Rule:
If clearly spoken, treat as dialogue. If clearly internal thought, treat as narration unless the project later adopts a separate thought convention.

## 10. Imperfect extracted fallback formatting
If the extracted fallback preserves section order and story text but spacing is messy, use it anyway. Repair only what is minimally necessary for consistent output.
