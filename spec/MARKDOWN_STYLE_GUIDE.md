# Markdown Style Guide

## Purpose
Keep outputs readable on GitHub and stable for downstream parsing.

## Required format

### Chapter heading
```md
# 1. 有一个小姐死了
```

### Character list section
```md
## Characters in this chapter

- 打电话的男人
- 李亮
```

### Script section
```md
## Script

[这是在中国的北京。]

李亮: 在那儿等着，不要让人进去！
```

## Spacing rules
1. One blank line after each header.
2. One blank line between narration and dialogue blocks.
3. No trailing commentary after script lines.
4. No markdown tables.
5. No inline HTML in final output.
6. No copied footnote or hyperlink anchors.
7. No code fences in final output files.

## Goals
The final markdown should be:
- easy to read on GitHub
- easy to assign for a reading group
- friendly to popup dictionary tools
- easy for future GPT parsing
- visually clear between narration and dialogue
