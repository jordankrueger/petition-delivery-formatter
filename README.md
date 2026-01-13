![HTML](https://img.shields.io/badge/HTML-5-E34F26.svg?logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-F7DF1E.svg?logo=javascript&logoColor=black)
![Works Offline](https://img.shields.io/badge/Works-Offline-9cf.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![No Server Required](https://img.shields.io/badge/Server-None%20Required-green.svg)
![Privacy](https://img.shields.io/badge/Privacy-100%25%20Local-brightgreen.svg)
![Made for Nonprofits](https://img.shields.io/badge/Made%20for-Nonprofits-orange.svg)
![Vibecoded with Claude](https://img.shields.io/badge/Vibecoded%20with-Claude-cc785c.svg)

# Petition Delivery PDF Generators

A collection of browser-based tools for converting CSV exports from ActionKit, EveryAction, Action Network, and other activism platforms into formatted PDF documents suitable for petition deliveries.

Both tools run entirely in your browser — your data never leaves your computer.

---

## 🔒 Privacy First

**Your data never touches a server.** All CSV processing and PDF generation happens 100% client-side in your browser using JavaScript. No data is uploaded, transmitted, or stored anywhere.

For maximum confidence, you can:
1. Load either tool in your browser
2. Disconnect from the internet
3. Process your CSV files completely offline

The tools will continue to work without any network connection.

---

## Available Tools

| Tool | Purpose |
|------|---------|
| [`simple-formatter.html`](#simple-formatter) | Convert a CSV of petition signers into a clean, paginated PDF grid |
| [`district-formatter.html`](#district-formatter) | Convert a CSV into a PDF organized by legislative district (U.S. House, U.S. Senate, State House, or State Senate) |

---

## Simple Formatter

### What It Does

Converts a CSV file of petition signers into a formatted PDF with a 3-column grid layout. Each cell displays:
- **Name** (bold, first line)
- **City, State ZIP** (second line)

The tool automatically paginates as needed, handling thousands of signers efficiently.

### How to Use

1. Open `simple-formatter.html` in any modern browser
2. Drag and drop your CSV file onto the page (or click to browse)
3. Verify the column mapping — the tool auto-detects common column names, but you can adjust if needed
4. Click **Generate PDF**
5. Save the downloaded PDF

### Column Auto-Detection

The tool recognizes these common column names (case-insensitive):

| Field | Recognized Column Names |
|-------|------------------------|
| First Name | `first_name`, `firstname`, `first`, `fname`, `given_name` |
| Last Name | `last_name`, `lastname`, `last`, `lname`, `surname`, `family_name` |
| City | `city`, `town`, `locality` |
| State | `state`, `region`, `province`, `state_code`, `addr_state` |
| ZIP | `zip`, `postal`, `postal_code`, `zipcode`, `zip_code`, `postcode` |

If your CSV uses different column names, simply select the correct column from the dropdown menu.

### Output Format

- **Page size:** Letter (8.5" × 11")
- **Layout:** 3-column grid
- **Cell contents:** Name (bold) on line 1, location on line 2
- **Long text:** Automatically truncated with ellipsis (…) to fit cells

---

## District Formatter

### What It Does

Converts a CSV file of petition signers into a PDF organized by legislative district. Signers are grouped under district headings, making it easy to deliver petition signatures to specific legislators.

Supports four district types:
- **U.S. House** — Groups by congressional district
- **U.S. Senate** — Groups by state (since senators represent entire states)
- **State House** — Groups by state legislative lower chamber district
- **State Senate** — Groups by state legislative upper chamber district

Each district section includes:
- A header bar with the full district name (e.g., "Pennsylvania — Congressional District 12")
- A count of signers in that district
- A 3-column grid of signers with name and location

### How to Use

1. Open `district-formatter.html` in any modern browser
2. **Select the district type** using the radio buttons at the top
3. Drag and drop your CSV file onto the page (or click to browse)
4. Verify the column mapping:
   - The tool auto-detects name, city, state, and ZIP columns
   - For U.S. House/State House/State Senate, it also attempts to detect the district column
   - Adjust any mappings as needed using the dropdowns
5. Review the preview showing signer counts per district
6. Click **Generate PDF**
7. Save the downloaded PDF

### Column Auto-Detection

#### Personal Information Columns

| Field | Recognized Column Names |
|-------|------------------------|
| First Name | `first_name`, `firstname`, `first`, `fname`, `given_name` |
| Last Name | `last_name`, `lastname`, `last`, `lname`, `surname`, `family_name` |
| City | `city`, `town`, `locality` |
| State | `state`, `region`, `province`, `state_code`, `addr_state` |
| ZIP | `zip`, `postal`, `postal_code`, `zipcode`, `zip_code`, `postcode` |

#### District Columns (by type)

| District Type | Recognized Column Names |
|---------------|------------------------|
| U.S. House | `congressional_district`, `us_house`, `us_house_district`, `cd`, `congress_district`, `us_district`, `house_district`, `us_rep_district` |
| State House | `state_house`, `state_house_district`, `hd`, `house_district`, `state_rep_district`, `state_representative_district`, `assembly_district`, `state_assembly` |
| State Senate | `state_senate`, `state_senate_district`, `sd`, `senate_district`, `state_sen_district`, `state_senator_district` |

**Note:** For U.S. Senate, no district column is needed — signers are grouped by their state.

### Handling District Formats

Activism platforms export district data in various formats. The tool handles all of these automatically:

| Format | Example | How It's Parsed |
|--------|---------|-----------------|
| State + underscore + number | `NV_01` | Nevada, District 1 |
| State + hyphen + number | `PA-12` | Pennsylvania, District 12 |
| State + number (no separator) | `CA07` | California, District 7 |
| Prefixed with HD/SD | `HD-42` | Uses state column, District 42 |
| Prefixed without separator | `SD15` | Uses state column, District 15 |
| Full format with chamber | `PA_HD_42` | Pennsylvania, District 42 |
| Just a number | `7` | Uses state column, District 7 |

**Important:** When the district value doesn't include a state code (like `HD-42` or just `7`), the tool uses the **State** column from that row to determine which state the district belongs to.

### Handling Unknown/Missing Districts

Signers without a valid district value are:
1. **Not discarded** — they're still included in the PDF
2. **Grouped at the end** under an "Unknown District" section
3. **Displayed with whatever location info is available** (city, state, ZIP)

This ensures no signers are lost, while keeping your organized district sections clean.

### District Heading Format

The PDF displays human-readable district headings:

| District Type | Example Heading |
|---------------|-----------------|
| U.S. House | "Nevada — Congressional District 1" |
| U.S. Senate | "Pennsylvania" |
| State House | "California — State House District 42" |
| State Senate | "Texas — State Senate District 15" |

All 50 states plus DC, Puerto Rico, Guam, Virgin Islands, American Samoa, and Northern Mariana Islands are supported with full names.

### Sorting Order

Districts are sorted:
1. **Alphabetically by state** (Alabama before Alaska before Arizona...)
2. **Numerically by district number within each state** (District 1 before District 2 before District 10...)

The "Unknown District" section always appears at the end.

### Output Format

- **Page size:** Letter (8.5" × 11")
- **Layout:** District sections with header bars, followed by 3-column signer grids
- **District headers:** Dark background with white text, includes district name and signer count
- **Continuation pages:** If a district spans multiple pages, the header shows "(continued)"
- **Cell contents:** Name (bold) on line 1, location on line 2
- **Long text:** Automatically truncated with ellipsis (…) to fit cells

---

## Fully Offline Installation

By default, both tools load the jsPDF library from a CDN (unpkg.com) when you first open them. If you need a completely air-gapped setup with zero network requests:

1. Download jsPDF:
   ```
   https://unpkg.com/jspdf@3.0.4/dist/jspdf.umd.min.js
   ```

2. Save the file as `jspdf.umd.min.js` in the same folder as the HTML files

3. Edit each HTML file and change this line:
   ```html
   <script src="https://unpkg.com/jspdf@3.0.4/dist/jspdf.umd.min.js"></script>
   ```
   to:
   ```html
   <script src="jspdf.umd.min.js"></script>
   ```

After this change, the tools will work with no network access whatsoever.

---

## Browser Compatibility

These tools work in all modern browsers:
- Chrome / Chromium
- Firefox
- Safari
- Edge

No installation, plugins, or extensions required.

---

## Performance

Both tools handle large CSV files efficiently:
- **5,000+ signers:** No problem
- **10,000+ signers:** Works fine, PDF generation may take a few seconds
- **Very large files:** Limited only by your browser's memory

---

## Troubleshooting

### "CSV file appears to be empty or invalid"
- Ensure your file has a header row
- Check that the file extension is `.csv`
- Try opening the CSV in a text editor to verify it's not corrupted

### Columns not auto-detected
- Use the dropdown menus to manually select the correct columns
- The tool shows "(not found)" next to fields it couldn't auto-detect

### District showing as "Unknown"
- Verify the district column is correctly mapped
- Check that district values are in a supported format (see table above)
- Ensure the State column is mapped if your district values don't include state codes

### PDF text is cut off
- This is expected behavior — long names/locations are truncated with "…" to maintain clean formatting
- The most important information (beginning of name, city) is preserved

---

## Credits

Built with [jsPDF](https://github.com/parallax/jsPDF) for PDF generation.

---

## License

GPL-3.0 — See [LICENSE](LICENSE) for details.
