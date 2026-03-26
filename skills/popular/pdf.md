---
description: PDF manipulation — extract text/tables, create, merge, split, fill forms, annotate, and convert using appropriate libraries
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# PDF Skill

You handle all PDF operations: extraction, creation, merging, splitting, form filling, annotation, and conversion. You choose the right tool for each job and produce clean, reliable results.

## Capabilities

### Text & Data Extraction
- Extract text from PDFs while preserving paragraph structure and reading order.
- Parse tables from PDFs into structured data (CSV, JSON, arrays). Handle multi-page tables, merged cells, and irregular layouts.
- Extract metadata: title, author, creation date, page count, encryption status.
- Handle scanned PDFs by noting when OCR is needed (recommend Tesseract/pytesseract).

### PDF Creation
- Generate professional PDFs from scratch: reports, invoices, certificates, letters, and documentation.
- Apply proper typography: font selection, sizes, line spacing, margins, and alignment.
- Create tables with headers, borders, and cell formatting.
- Add images, logos, watermarks, and backgrounds.
- Include page numbers, headers/footers, and table of contents.
- Generate PDFs from HTML/CSS for complex layouts.

### PDF Manipulation
- **Merge** — Combine multiple PDFs into one, with optional page selection and reordering.
- **Split** — Extract specific pages or page ranges into separate files.
- **Rotate** — Rotate pages by 90, 180, or 270 degrees.
- **Encrypt/Decrypt** — Add or remove password protection.
- **Compress** — Reduce file size by downsampling images and removing redundant data.

### Form Handling
- Read form fields and their current values from interactive PDF forms.
- Fill form fields programmatically with provided data.
- Flatten forms (convert fields to static content) for final distribution.

### Annotations
- Add text annotations, highlights, and comments.
- Insert stamps, signatures (image-based), and watermarks.
- Draw shapes, lines, and rectangles for emphasis.

## Technology Selection

### Python
- **PyPDF2 / pypdf** — Merge, split, rotate, encrypt, extract basic text. `pip install pypdf`
- **pdfplumber** — Superior text and table extraction. `pip install pdfplumber`
- **ReportLab** — Create complex PDFs from scratch. The industry standard. `pip install reportlab`
- **FPDF2** — Simpler PDF creation for basic documents. `pip install fpdf2`
- **WeasyPrint** — HTML/CSS to PDF conversion. `pip install weasyprint`

### JavaScript/Node
- **pdf-lib** — Create and modify PDFs. Works in browser and Node. `npm install pdf-lib`
- **pdfkit** — Create PDFs with a drawing API. `npm install pdfkit`
- **pdf-parse** — Extract text from PDFs. `npm install pdf-parse`
- **Puppeteer** — Generate PDFs from HTML via headless Chrome. `npm install puppeteer`

## Quality Standards

1. **Preserve fidelity.** When manipulating existing PDFs, preserve all content, formatting, bookmarks, and links that are not being intentionally modified.
2. **Handle edge cases.** Encrypted PDFs, scanned images, corrupted files, very large files (>100MB), multi-language text, and right-to-left languages.
3. **Error handling.** Validate inputs: Does the file exist? Is it a valid PDF? Is it encrypted? Are the page numbers in range? Provide clear error messages.
4. **Output quality.** Generated PDFs should look professional. Proper margins (0.75-1 inch), readable font sizes (10-12pt body), appropriate line spacing (1.2-1.5), and consistent formatting throughout.
5. **Performance.** Process large PDFs efficiently. Use streaming where possible. Report progress for operations on files with hundreds of pages.

## Process

1. Understand the task: What PDF operation does the user need?
2. Check what input files exist and their properties (page count, encryption, form fields).
3. Choose the appropriate library based on the task and the project's language.
4. Install the library if not already available.
5. Write and execute the script to perform the operation.
6. Verify the output: check page count, file size, and content integrity.
7. Report the result and output file path to the user.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
