# PR Media Wrap Editor

A self-contained, single-file web app for creating polished media coverage wrap documents — designed for the U.S. Travel Association PR team. Build hero grids, stats rows, and coverage tables, then export to a print-ready PDF or share a live link.

**Live app:** https://gzciteli.github.io/pr-media-wrap/

---

## Toolbar Reference

The toolbar at the top of the page contains all controls for working with your document.

### 📥 Import
Imports coverage data from a formatted Excel spreadsheet (.xlsx). The app reads every sheet in the workbook except the "Instructions" sheet, and routes rows to the correct module based on the `type` column. Coverage grids and tables **append** new entries (duplicates are skipped); stats, the title bar, and text blocks **replace** their existing content.

### 📄 Template
Downloads a blank Excel template pre-formatted with the correct column headers and sheet structure. Fill this in and use **Import** to populate your document. See the [Spreadsheet Template](#spreadsheet-template) section below for details.

### 💾 Save
Saves the entire document state (all modules and their content) as a `.json` file to your computer. The filename matches the document title you've set. Use this to preserve your work between sessions or hand off the file to a colleague.

### 📂 Load
Loads a previously saved `.json` project file, restoring the document exactly as it was when saved.

### ⚙️ Settings
Opens the Settings panel, which has four tabs:

- **Theme** — change the header bar background color and accent color
- **Typography** — adjust font sizes for stat values/labels, section headings, table text, card headlines, card commentary, and header text
- **Publications** — manage the list of publication presets (brand colors, fonts, logo URLs). See [Publications Settings](#publications-settings) below.
- **Editor** — toggle "Show text labels on toolbar buttons" to display text beneath each toolbar icon

### 📖 Instructions
Opens this README in a new browser tab. This button always displays its label regardless of the label toggle setting.

### 🖨️ Export PDF
Renders the document to a multi-page PDF and downloads it. The filename is derived from the document title. Card shadows are converted to borders for crisp PDF rendering.

### ＋ Add Module *(dropdown)*
Select a module type from the dropdown to append it to the bottom of the document:

| Module | Description |
|---|---|
| **Header Bar** | Full-width banner with the document title |
| **Stats Row** | Row of up to N stat blocks (number + label) |
| **Section Heading** | Bold divider text between sections |
| **Hero Grid** | 2-column grid of featured coverage cards with brand styling |
| **Table** | List of coverage rows with publication, headline, URL, and "Additional coverage in…" pub links |
| **Text** | Free-form rich text block (editable inline or via HTML editor) |

---

## Building Your Document

### Editing Modules

Every module in the document can be reordered using the **▲ ▼** buttons on its left edge, or removed with **✕**. Each module also has an **import key** field — this is used to match Excel data to the correct module during import (see [Spreadsheet Template](#spreadsheet-template)).

### Header Bar
Click the title text directly to edit it inline.

### Stats Row
Each stat has a value and a label. Click either to edit inline. Use the **＋** button (visible in edit mode) to add a stat, and the **✕** beside each stat to remove one.

### Section Heading
Click the heading text to edit it inline.

### Hero Grid
Each card displays a publication logo, a headline (and optional second headline), and a commentary excerpt. The top of each card uses the publication's brand background color; the card body is always white.

- **✏** (edit) — opens the card editor to change publication, headline(s), URL, and commentary
- **✕** (remove) — removes the card
- **＋ Add Card** button — appears in edit mode below the grid

In the card editor, select the **Publication** from the dropdown to auto-apply brand styling. You can also type a publication name manually. The **Logo** field supports a URL or an uploaded image file.

### Table (Minor Table)
Rows contain a publication name, headline, and URL. Each row has **✏** and **✕** buttons. The **＋ Add Row** button appears below the table in edit mode.

When adding a row, the **Row type** dropdown lets you choose:
- **Regular row** — added to the table
- **Additional — appears in "+ Additional coverage in…" line** — added as a publication name link below the table (used for brief/link-only mentions)

**Editing additional coverage links:** In editor mode, the publication names in the "+ Additional coverage in…" line appear with a dashed underline. Clicking one opens the row editor so you can update the name or URL.

### Text Block
Click anywhere in the text to edit it inline. For full HTML control, use the **< >** button on the module's control bar to open the raw HTML editor.

---

## Spreadsheet Template

Download the template using the **📄 Template** button. The workbook has multiple sheets:

- **Coverage** — hero grid and table rows (domestic and international)
- **Stats** — stat block values and labels
- **Text & Titles** — document title and intro/footer text
- **Instructions** *(not imported)* — notes and guidance; this sheet is always skipped during import

### Column Reference

**Coverage sheet:**

| Column | Description |
|---|---|
| `type` | `featured` (hero grid), `domestic` (domestic table), or `international` (international table). Rows with a blank type or starting with `-` are skipped. |
| `publication` | Publication name — must match a preset in Publications for brand styling |
| `headline` | Article headline |
| `url` | Link to the article |
| `commentary` | Pull-quote or excerpt (hero grid only) |
| `second_headline` | Optional second headline (hero grid only) |
| `second_url` | URL for the second headline (hero grid only) |
| `additional` | Set to `additional` to add this row as a link in the "+ Additional coverage in…" line instead of as a table row |

**Stats sheet:**

| Column | Description |
|---|---|
| `type` | Must be `summary_stats` |
| `label` | Stat label text (e.g. "Total Impressions") |
| `value` | Stat value text (e.g. "2.4B") |

**Text & Titles sheet:**

| Column | Description |
|---|---|
| `type` | `doc_title` (header bar title), `intro_text` (intro html block), or `footer_text` (footer html block) |
| `value` | The text or HTML content |

### Import Behavior

- **Hero Grid / Tables:** new rows are **appended**; existing entries are kept. Duplicates (matched by publication + headline) are skipped.
- **Stats, Header, Text Blocks:** existing content is **replaced** with the imported values.
- The **Instructions** sheet is never read during import.

---

## Publications Settings

Open **⚙️ Settings → Publications** to manage your publication presets. Each preset defines:

| Field | Description |
|---|---|
| **Name** | Must match the `publication` value used in your data exactly |
| **Card Bg** | Background color for the logo area of hero grid cards |
| **Name Color** | Text color used for the publication name |
| **Font** | Headline font (e.g. "Georgia", "Oswald") |
| **Logo URL** | URL to the publication's logo image |

Use **＋ Add Publication** to create a new preset. Each existing preset has an **Edit** and **Remove** button.

---

## Default Template & Settings Persistence

Your settings (theme, typography, publications, and editor preferences) are stored in your browser's localStorage and persist across sessions **in the same browser**. Clearing browser data will reset them to defaults.

To share settings across devices or team members, use **Export JSON** and **Import JSON** at the bottom of the Settings panel.

> **Note:** The factory defaults — including the default publication list, template structure, and theme colors — are defined in the source code on GitHub. If you want to update the defaults for everyone on the team, edit `settings.json` and `index.html` in the repository.

To save the current document layout as the default template for new documents, go to **Settings → Template** and click **Save Current as Default Template**. Click **Reset to Factory Default** to revert.

---

## Exporting

**PDF Export (🖨️):** Renders the document at 780px width (equivalent to an 8.5" letter page) using html2canvas + jsPDF. The exported filename matches the document title. For best results, review the document in preview mode before exporting.

**Save/Load JSON (💾 / 📂):** The JSON project file captures all module content, order, and settings. Use it to hand off work, version-control your wrap, or restore a previous state.

---

*PR Media Wrap Editor · Gabriel Z. Citeli 2026 · U.S. Travel Association*
