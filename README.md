# OFTO Scheme Analysis Dashboard

A sophisticated, McKinsey-style analytical dashboard for evaluating OFTO (Offshore Transmission Owner) investment opportunities. Features elegant D3.js visualizations and secure client-side Excel data processing.

## Features

### Security & Privacy
- **100% Client-Side Processing**: All Excel data processing occurs in your browser
- **No Data Transmission**: Your database files never leave your computer
- **Local-Only Storage**: Data exists only in browser memory during your session

### Professional Design
- **McKinsey-Style Typography**: Lato and Merriweather fonts for consulting-grade presentation
- **Sophisticated Color Palette**: Official McKinsey color scheme
- **Pyramid Principle Report**: Structured analysis following McKinsey's communication framework

### Visualizations
- **Time Series Line Chart**: OFTO project value trends
- **Market Share Bar Chart**: Operator market positioning
- **Waterfall Chart**: Revenue composition analysis
- **Distribution Scatter Plot**: IRR distribution across tenders

## How to Use

### 1. Open the Dashboard
Simply open `index.html` in any modern web browser (Chrome, Firefox, Safari, Edge).

### 2. Prepare Your Excel File

Your Excel workbook should contain sheets with the following names and structures:

#### Sheet: "TimeSeries"
| year | value |
|------|-------|
| 2015 | 1.2   |
| 2016 | 1.8   |
| 2017 | 2.5   |

- `year`: Integer year value
- `value`: Numeric value in billions (£)

#### Sheet: "MarketShare"
| operator    | share |
|-------------|-------|
| Operator A  | 28    |
| Operator B  | 24    |
| Operator C  | 18    |

- `operator`: String name of OFTO operator
- `share`: Percentage market share (0-100)

#### Sheet: "Revenue"
| category           | value |
|--------------------|-------|
| Base Revenue       | 120   |
| Availability Bonus | 25    |
| Inflation Adj.     | 18    |

- `category`: String category name
- `value`: Numeric value in millions (£)

#### Sheet: "IRR"
| project | irr  |
|---------|------|
| P1      | 8.2  |
| P2      | 9.1  |
| P3      | 7.8  |

- `project`: String project identifier
- `irr`: Internal rate of return percentage

### 3. Upload Your Data

1. Click the "SELECT EXCEL FILE" button in the Visualizations tab
2. Choose your .xlsx or .xls file
3. The system will load and visualize your data
4. All processing happens locally - your data remains private

### 4. Customize Data Extraction (Optional)

To customize how data is extracted from your Excel file, edit the extraction functions in `index.html`:

```javascript
// Located around line 507-562
function extractTimeSeriesData() {
    if (excelData && excelData['YourSheetName']) {
        return excelData['YourSheetName'].map(row => ({
            year: row.YourYearColumn,
            value: row.YourValueColumn
        }));
    }
    // Fallback to sample data
    return [...];
}
```

Modify these functions to match your Excel structure:
- `extractTimeSeriesData()` - Line ~508
- `extractMarketShareData()` - Line ~526
- `extractRevenueData()` - Line ~539
- `extractIRRData()` - Line ~551

## Navigation

The dashboard has three main sections:

1. **Visualizations**: Interactive D3.js charts displaying your data
2. **Analysis Report**: McKinsey-style equity research analysis with pyramid principle structure
3. **References & Sources**: Data sources and methodology citations

## Technical Stack

- **D3.js v7**: Sophisticated data visualizations
- **SheetJS**: Secure Excel file processing
- **TailwindCSS**: Responsive utility-first styling
- **Vanilla JavaScript**: No framework dependencies

## Customization

### Modify Colors
Edit the CSS variables in the `<style>` section (line ~40):

```css
:root {
    --mckinsey-blue: #003d7a;
    --mckinsey-light-blue: #0073cf;
    --mckinsey-teal: #00a9ce;
    /* ... */
}
```

### Adjust Chart Dimensions
Modify margin and height values in chart rendering functions (lines 574-872).

### Update Report Content
Edit the HTML content in the "Report Content" section (lines 265-385).

## Browser Compatibility

Tested and working in:
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

## Privacy Guarantee

This application:
- ❌ Does NOT upload your data anywhere
- ❌ Does NOT connect to external APIs with your data
- ❌ Does NOT store your data persistently
- ✅ Processes everything locally in your browser
- ✅ Only loads visualization libraries from CDNs (D3.js, SheetJS)
- ✅ Clears data when you close the browser tab

## License

Copyright © 2025. All Rights Reserved.

This report is for informational purposes only and does not constitute an offer to sell or a solicitation of an offer to buy any securities.
