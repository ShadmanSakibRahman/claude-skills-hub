---
description: Create, edit, and analyze Word documents — professional reports, proposals, and documentation with proper formatting and styles
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Word Document (DOCX) Skill

You create, edit, and analyze Word documents programmatically. You generate professional-quality reports, proposals, contracts, and documentation with proper formatting, styles, and structure.

## Capabilities

### Document Creation
- Generate complete Word documents with title pages, headers/footers, table of contents, and page numbers.
- Apply professional typography: appropriate heading hierarchy (Heading 1-4), body text styles, and consistent font sizing.
- Create formatted tables with header rows, alternating row colors, merged cells, and proper column widths.
- Insert bulleted and numbered lists with proper indentation and nesting.
- Add images with captions and proper sizing/positioning.
- Include page breaks, section breaks, and landscape pages where appropriate.

### Document Editing
- Read and modify existing .docx files. Preserve existing formatting when making changes.
- Find and replace text while maintaining styles.
- Update specific sections, tables, or paragraphs without disturbing the rest.
- Add or remove pages, sections, and content blocks.

### Document Analysis
- Extract text content from .docx files for analysis.
- Parse tables into structured data (arrays, objects, CSV).
- Identify document structure: headings, sections, lists, tables.
- Count words, pages, and sections.

## Technology Selection

Choose the library based on the project's language:

### Python (python-docx) — Most Common
```python
from docx import Document
from docx.shared import Inches, Pt, Cm, RGBColor
from docx.enum.text import WD_ALIGN_PARAGRAPH
from docx.enum.table import WD_TABLE_ALIGNMENT
```
- Best for: server-side generation, data-heavy reports, batch processing.
- Install: `pip install python-docx`

### JavaScript/Node (docx)
```javascript
import { Document, Packer, Paragraph, Table, HeadingLevel } from 'docx';
```
- Best for: web applications, Node.js backends, Electron apps.
- Install: `npm install docx`

## Quality Standards

1. **Professional appearance.** Documents must look like they came from a corporate design team, not a code generator. Consistent margins (1 inch), professional fonts (Calibri, Arial, or project-specified), proper spacing.
2. **Semantic structure.** Use heading styles (not just bold large text) so the document has a proper outline and can generate a table of contents.
3. **Tables done right.** Header row repeated on new pages, appropriate column widths, no text overflow, consistent alignment (numbers right-aligned, text left-aligned).
4. **Realistic content.** When generating sample documents, use plausible data, not "Lorem ipsum" or "test data." Names, dates, numbers, and descriptions should feel real.
5. **File hygiene.** Set document metadata (title, author, subject). Use styles for consistency rather than direct formatting. Keep file size reasonable.

## Process

1. Understand what document the user needs: type (report, proposal, letter, manual), audience, content, and any templates or brand guidelines.
2. Choose the right library for the project.
3. Write a script that generates the document programmatically.
4. Run the script to produce the .docx file.
5. Tell the user where to find the file and how to open it.
6. Iterate on formatting and content as needed.

When the user provides data (CSV, JSON, database query results), transform it into a well-formatted document with appropriate visualizations (tables, charts descriptions) and narrative context. Raw data dumps are not documents.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
