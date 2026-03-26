---
description: Create and edit Excel spreadsheets — formulas, charts, conditional formatting, pivot tables, and data validation
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Excel Spreadsheet (XLSX) Skill

You create, edit, and analyze Excel spreadsheets programmatically. You build professional workbooks with formulas, charts, formatting, data validation, and pivot tables that look like they were crafted by an Excel power user.

## Capabilities

### Spreadsheet Creation
- Generate workbooks with multiple named sheets, organized logically (Summary, Data, Charts, Reference).
- Write data with proper column headers, data types (numbers as numbers, dates as dates, not strings), and column widths auto-fitted to content.
- Apply professional formatting: header row styling (bold, colored background, frozen panes), alternating row colors, number formats (currency, percentage, dates), and cell borders.
- Add formulas: SUM, AVERAGE, COUNT, VLOOKUP, INDEX/MATCH, IF/IFERROR, SUMIFS, and array formulas where appropriate.
- Create named ranges for formula readability and data validation sources.

### Charts & Visualization
- Generate charts: bar, column, line, pie, scatter, area, combo charts, and sparklines.
- Configure chart elements: title, axis labels, legends, data labels, trendlines, and gridlines.
- Style charts with professional color palettes and clean typography.
- Place charts on dedicated chart sheets or embedded in data sheets with proper sizing and positioning.

### Data Features
- **Conditional Formatting** — Color scales, data bars, icon sets, and rule-based formatting (highlight cells above/below average, top N, duplicates).
- **Data Validation** — Dropdown lists, number ranges, date ranges, custom formulas, and input messages/error alerts.
- **Pivot Tables** — Summarize data by categories with row/column grouping, value aggregation (sum, count, average), and calculated fields.
- **Filters & Sorting** — Auto-filters on header rows, custom sort orders, and filter views.
- **Tables** — Convert ranges to Excel tables with structured references, total rows, and auto-expanding formulas.

### Data Analysis
- Read existing Excel files and extract data into structured formats.
- Parse formulas and identify dependencies between cells.
- Detect data quality issues: blanks, duplicates, inconsistent formats, outliers.
- Generate summary statistics and data profiles.

## Technology Selection

### Python (openpyxl) — Most Common
```python
from openpyxl import Workbook, load_workbook
from openpyxl.styles import Font, PatternFill, Alignment, Border
from openpyxl.chart import BarChart, LineChart, PieChart, Reference
from openpyxl.formatting.rule import ColorScaleRule, DataBarRule
from openpyxl.utils import get_column_letter
```
- Install: `pip install openpyxl`
- For heavy data processing, use `pandas` with `openpyxl` engine: `df.to_excel('output.xlsx', engine='openpyxl')`

### JavaScript/Node (ExcelJS)
```javascript
import ExcelJS from 'exceljs';
```
- Install: `npm install exceljs`
- For browser-side: use SheetJS (`xlsx` package) for reading, ExcelJS for creation.

## Quality Standards

1. **Professional appearance.** Spreadsheets must be presentation-ready. Consistent formatting, logical layout, frozen header rows, appropriate column widths, and print-area configuration.
2. **Correct data types.** Numbers are numbers (right-aligned), dates are Excel date serials (not strings), currencies have proper format codes, percentages are decimal values with percent format.
3. **Formula hygiene.** Use structured references and named ranges. Avoid hardcoded values in formulas. Add IFERROR wrappers for lookups. Document complex formulas with cell comments.
4. **Usability.** Add filter dropdowns on data headers. Freeze the top row and first column where appropriate. Group related columns. Hide helper/calculation columns.
5. **Print readiness.** Set print area, page orientation, margins, headers/footers, and repeat rows/columns for multi-page printouts.

## Process

1. Understand what data the user has and what they need the spreadsheet to show.
2. Design the workbook structure: sheet names, data layout, summary/dashboard sheet.
3. Write the script to generate the spreadsheet programmatically.
4. Run the script and verify the output opens correctly in Excel.
5. Iterate on formatting, formulas, and charts as needed.

Transform raw data into insightful, well-organized spreadsheets that tell a story. A good spreadsheet guides the reader from summary to detail.

<!-- From claude-skills-hub by @ShadmanSakibRahman — https://github.com/ShadmanSakibRahman/claude-skills-hub -->
