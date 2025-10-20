# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a sophisticated single-page application for OFTO (Offshore Transmission Owner) scheme analysis, designed as a professional equity research dashboard. The application processes Excel data locally in the browser to generate professional visualizations and investment analysis reports.

## Report Writing Guidelines

All content in the Analysis Report section must follow UK Government/Corporate report writing standards. This ensures formal, plain-English content with clear signposting and consistent structure.

### Writing Style Principles

**Tone**: Professional, direct, and neutral. Avoid hype or promotional language.

**Voice**: Use "we" for organizational actions and decisions; use third-person ("the company") sparingly for formal commitments.

**Plain English**: Short sentences and familiar words. Avoid unnecessary jargon. Define all acronyms on first use.

**Sentence Structure**: Average 15-20 words. One idea per sentence. Active voice preferred.

**Tense**: Present for ongoing facts and decisions; future for planned actions; past for methods already completed.

### Quantitative Qualifiers (Standardized)

Define once and reuse consistently:
- **majority** = clearly >50%
- **about half** = ~50% ± a few percentage points
- **many** = >70%
- **some** = 30–70%
- **a few** = <30%

Provide actual counts in parentheses first time (e.g., "sixteen (16) respondents…").

### Report Structure (Macro-Level)

```
1. Background
   1.1. Foundation and Regulatory Framework
   1.2. Ofgem's Objectives
   1.3. The Authority's Role
2. [Analysis Section]
   2.1. [Topic Area]
   2.2. [Topic Area]
3. Findings / Assessment
4. Investment Thesis
5. Next Steps
```

### Section Pattern (Micro-Structure - Reusable)

For each analytical section, use this consistent pattern:

**[Purpose]**
- 1–3 sentences: what this section does

**[Summary of responses / Findings]**
- Quantified counts where possible
- Use standardized qualifiers
- Evidence-first, no rhetoric

**[Position / Decision]**
- State decision or position first, then rationale
- Reference enabling frameworks
- Indicate future exploration areas

**[Implications]** (optional)
- Effects on stakeholders, operations, risk, cost, timelines

**[Next steps]** (if not covered globally)
- Concrete actions, owner, timing

### Language Rules

**Spelling**: UK forms (licence not license, programme not program)

**Dates**: Long form ("25 April 2022" not "4/25/22")

**Numbers**: Spell out one through nine; use numerals for 10+

**Acronyms**: Define on first use: "Offshore Transmission Owner (OFTO)"

**Headings**: Numbered (1, 1.1, 1.1.1). Sentence case. Short and descriptive.

**Lists**:
- Bullets for themes or unordered items
- Numbered lists for sequences or procedures

### Evidence & Referencing

- Cite legal/policy anchors via footnotes when they inform decisions
- Be explicit when evidence is mixed
- Separate fact from decision: report evidence first, then state position
- Use footnotes for sources (numbered, terse description + link)

### Formatting Standards

**Headings Hierarchy**:
- H2: Main sections (1., 2., 3.)
- H3: Subsections (1.1., 1.2., 2.1.)
- H4: Sub-subsections (1.3.1., 1.3.2.)
- H5: Detail items within sub-subsections

**Visual Elements**:
- Highlight boxes for quoted regulatory text or key frameworks
- Color-coded scenario boxes for financial analysis
- Tables for quantitative comparisons
- Maintain McKinsey color palette for professional appearance

### Content Principles

**Conciseness**: Cut unnecessary words. "The regime was introduced" not "The regime was established and introduced".

**Directness**: Lead with conclusions. "Ofgem manages tenders" not "It is Ofgem's responsibility to manage tenders".

**Precision**: Technical terms used correctly. Legal references accurate.

**Signposting**: Use section references ("See §2.3") to guide readers.

**Scannability**: Readers should be able to extract key points from headings and first sentences alone.

## Architecture

**Technology Stack:**
- Pure HTML/CSS/JavaScript (no build process required)
- D3.js v7 for data visualizations
- SheetJS (xlsx library) for Excel file processing
- TailwindCSS via CDN for styling
- Lato and Merriweather fonts for professional typography

**Key Design Principles:**
- **Client-side only**: All data processing occurs in browser - nothing sent to servers
- **Privacy-first**: Excel database files never leave user's computer
- **McKinsey aesthetic**: Professional consulting-grade design with specific color palette
- **Responsive**: Charts re-render on window resize

## Running the Application

```bash
# Simply open in browser
start index.html

# OR use a local server (recommended for development)
python -m http.server 8000
# Navigate to http://localhost:8000
```

**No build, compile, or npm install required** - this is a static HTML file.

## Code Structure

**Single File Architecture** (`index.html`):
- Lines 1-180: HTML head with CDN imports and McKinsey-style CSS
- Lines 181-418: HTML body with header, tabs, and content sections
- Lines 420-890: JavaScript for data handling and D3.js visualizations

**Three Main Tabs:**
1. **Visualizations** (lines 219-263): File upload + 4 D3.js charts
2. **Analysis Report** (lines 265-385): McKinsey pyramid principle structured report
3. **References** (lines 387-409): Data sources and citations

## Data Flow

```
User uploads Excel file
    ↓
handleFileUpload() - line 461
    ↓
SheetJS parses to JSON (stored in excelData global)
    ↓
processDataForVisualizations() - line 496
    ↓
Extract functions filter data for each chart (lines 507-562)
    ↓
renderAllCharts() calls 4 D3.js render functions (lines 566-872)
```

**Critical**: Data never leaves browser. Global `excelData` object stores raw Excel data, `visualizationData` stores processed chart data.

## Excel Data Structure

The application expects four sheets with specific column names:

- **TimeSeries**: `year` (int), `value` (number in billions)
- **MarketShare**: `operator` (string), `share` (percentage 0-100)
- **Revenue**: `category` (string), `value` (number in millions)
- **IRR**: `project` (string), `irr` (percentage)

**Customization Point**: Edit extract functions (lines 507-562) to match different Excel structures.

## Visualization Details

**Chart 1 - Time Series Line Chart** (lines 574-638):
- Smooth line with data points
- Grid lines for readability
- McKinsey blue color scheme
- Y-axis formatted as "£Xbn"

**Chart 2 - Horizontal Bar Chart** (lines 641-702):
- Color-coded bars using McKinsey palette
- Inline percentage labels
- Left-aligned operator names

**Chart 3 - Waterfall Chart** (lines 705-796):
- Cumulative revenue buildup visualization
- Dotted connector lines between segments
- Rotated x-axis labels for readability
- Values displayed as "£Xm"

**Chart 4 - Distribution Scatter Plot** (lines 799-872):
- Individual project IRR points
- Mean line overlay (orange dashed)
- Purple dots for McKinsey aesthetic
- Percentage formatted y-axis

## McKinsey Style Guidelines

**Color Palette** (CSS variables, line 40-48):
- Primary: `#003d7a` (McKinsey blue)
- Secondary: `#0073cf` (light blue), `#00a9ce` (teal)
- Accents: `#00ab84` (green), `#ff8200` (orange), `#6e2c91` (purple)
- Neutrals: `#5f6062` (gray), `#e6e7e8` (light gray)

**Typography**:
- Headers: Lato, 700 weight, -0.02em letter spacing
- Body: Lato, 400 weight, -0.01em letter spacing
- Serif accent: Merriweather for emphasis

**Report Structure** (Pyramid Principle):
1. Key message first in insight box (line 270-272)
2. Executive summary with 3 supporting points (lines 274-290)
3. Detailed sections with sub-arguments
4. Visual hierarchy with color-coded scenario boxes

## Common Development Tasks

### Add a New Chart

1. Add HTML container in visualizations section:
```html
<div class="chart-container">
    <div class="chart-title">Your Chart Title</div>
    <div class="chart-subtitle">Subtitle</div>
    <div id="chart5"></div>
</div>
```

2. Create data extraction function:
```javascript
function extractYourData() {
    if (excelData && excelData['YourSheet']) {
        return excelData['YourSheet'];
    }
    return [/* sample data */];
}
```

3. Add to `processDataForVisualizations()` (line 496)

4. Create render function following D3.js pattern from existing charts

5. Call from `renderAllCharts()` (line 566)

### Modify Report Content

Edit HTML directly in lines 265-385. Maintain structure:
- Use `.insight-box` for key messages
- Use `.supporting-point` for bulleted insights
- Follow color-coded scenario boxes pattern

### Change Data Source Format

Modify extraction functions (lines 507-562) to map your column names:
```javascript
return excelData['YourSheet'].map(row => ({
    year: row.YourYearColumn,  // Map to your column name
    value: row.YourValueColumn
}));
```

### Adjust Chart Styling

Charts use McKinsey color palette defined in `colors` object (line 427). Modify chart render functions to change:
- Margins: `margin` object in each render function
- Dimensions: `width`/`height` calculations
- Colors: Use `colors.blue`, `colors.orange`, etc.
- Fonts: Axes use Lato via CSS class `.axis`

## Security Considerations

**What IS secure:**
- Excel file processing (100% client-side via FileReader API)
- Data storage (in-memory JavaScript objects only)
- No external API calls with user data

**What to maintain:**
- Never add fetch/XMLHttpRequest with user data
- Never add localStorage/sessionStorage for sensitive data
- Keep all processing in `handleFileUpload()` function

## Browser Compatibility

Tested in Chrome 90+, Firefox 88+, Safari 14+, Edge 90+. Requires:
- ES6 support (arrow functions, template literals)
- FileReader API
- D3.js v7 compatibility

## Known Limitations

- Large Excel files (>50MB) may cause performance issues
- Charts don't export to PNG/SVG (could add html2canvas)
- No data persistence (by design for privacy)
- Mobile experience not optimized (desktop-first design)

## File References

- `index.html:420-890` - All JavaScript logic
- `index.html:20-180` - McKinsey styling
- `index.html:270-272` - Pyramid principle key message
- `index.html:461-492` - Secure file upload handler
- `index.html:574-872` - D3.js chart implementations
