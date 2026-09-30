# I FUCK PDF

> **Your Files Never Leave Your Browser** — A privacy-first, fully client-side PDF and image processing suite.

30 tools (26 working, 4 in progress) for document and image work that run entirely in
your browser via WebAssembly. **No uploads. No servers. No sign-up. No data ever leaves
your device.**

---

## ✨ Features

Find a tool by searching or filtering by category — or press <kbd>/</kbd> to jump
straight to the search field. Every tool opens in a focused workspace: drop a file,
adjust the options, download the result. Tools are deep-linkable (`#merge-pdf`), so
you can bookmark or share a specific job.

### 📄 Edit Workflows
| Tool | Description |
|------|-------------|
| **Merge PDF** | Combine multiple PDFs into one document |
| **Split PDF** | Extract pages into separate PDF files |
| **Compress PDF** | Reduce PDF file size (real image recompression via Ghostscript WASM) |
| **Organize PDF** | Reorder, remove, and rearrange pages via drag-and-drop |
| **Rotate PDF** | Rotate individual pages by 90°, 180°, or 270° |
| **Watermark PDF** | Add text watermarks with custom position, color, opacity, and rotation |
| **Page Numbers** | Insert page numbers with customizable position and format (arabic, zero-padded, or roman numerals up to 3999) |

### 🔄 Conversion
| Tool | Description |
|------|-------------|
| **PDF to PPT** | Convert PDF pages to PowerPoint slides |
| **PPT to PDF** | Convert PowerPoint files to PDF (slides are read in their real order) |
| **PDF to JPG** | Export PDF pages as JPEG images |
| **JPG to PDF** | Create a PDF from JPG, PNG, WebP and other browser-decodable images |
| **Word to PDF** | Convert DOCX documents to PDF, with word wrapping |
| **PDF to Word** | Convert PDF pages to a Word document |
| **Excel to PDF** | Convert XLSX spreadsheets to PDF, with columns clipped to the page |

### 🔒 Security
| Tool | Description |
|------|-------------|
| **Protect PDF** | Encrypt PDFs with password protection (Standard 128-bit RC4) |
| **Unlock PDF** | Remove password protection from encrypted PDFs |
| **Sign PDF** | Add a dated signature block to the last page |
| **Repair PDF** | Rebuild the internal structure of damaged PDF files. Files with a broken cross-reference table are recovered by re-rendering; a file that is password protected is rejected with a pointer to Unlock PDF, since it cannot be structurally repaired |

### 🤖 AI Workflows
| Tool | Description |
|------|-------------|
| **OCR PDF** | Extract text from scanned PDFs using Tesseract.js — supports English, French, German, Spanish, Italian, Portuguese, Dutch |
| **Chat with PDF** | 🚧 Coming Soon — Local AI chat powered by WebNN/WebGPU |
| **Summarize PDF** | 🚧 Coming Soon — Local AI summarization |
| **Extract Tables** | 🚧 Coming Soon — Local AI table extraction |
| **Resume Parser** | 🚧 Coming Soon — Local AI resume parsing |

### 🖼️ Image Tools
| Tool | Description |
|------|-------------|
| **Compress Image** | Reduce image file size with quality control |
| **Resize Image** | Scale images to custom dimensions |
| **Crop Image** | Interactive cropping with adjustable region and aspect-ratio lock |
| **Rotate Image** | Rotate images in 90° steps |
| **Upscale Image** | Increase image resolution |
| **Watermark Image** | Add text watermarks to images |
| **Convert to JPG** | Convert images (PNG, WebP, etc.) to JPEG format |

> **Note on image formats:** every image tool preserves the source format, and the
> download extension always matches the bytes that were actually produced. JPEG in
> means JPEG out, PNG in means PNG out — the file name never misrepresents the
> contents.

---

## 🧠 How It Works

All processing is powered by industry-standard open-source libraries compiled to WebAssembly or running natively in JavaScript:

- **[PDF-Lib](https://pdf-lib.js.org/)** — PDF creation and manipulation
- **[pdf.js](https://mozilla.github.io/pdf.js/)** — PDF rendering (Mozilla's PDF engine)
- **[PptxGenJS](https://github.com/gitbrent/PptxGenJS)** — PowerPoint generation
- **[docx](https://docx.js.org/)** — Word document generation
- **[SheetJS](https://sheetjs.com/)** — Excel file processing
- **[Tesseract.js](https://tesseract.projectnaptha.com/)** — OCR in the browser
- **[Ghostscript (WASM)](https://github.com/jsscheller/ghostscript-wasm)** — Real PDF recompression (Compress PDF)
- **[JSZip](https://stuk.github.io/jszip/)** — Archive handling
- **[SortableJS](https://sortablejs.github.io/Sortable/)** — Drag-and-drop page reordering

The Protect PDF / Unlock PDF tools implement **Standard PDF 2.0 (128-bit RC4)** encryption natively in JavaScript, fully compatible with Adobe Acrobat, Chrome, Edge, Safari, Preview, and all standard PDF readers.

### Font coverage

The text-based PDF tools (watermark, page numbers, sign, Word→PDF, Excel→PDF,
PPT→PDF) draw with pdf-lib's built-in **WinAnsi** fonts, which cover Latin-1
only. Non-Latin scripts and emoji cannot be rendered with them. Rather than
failing midway through a document, these tools now:

- **Sign / Watermark:** reject the input up front with a message naming the cause.
- **Word / Excel / PPT→PDF:** skip the affected lines or paragraphs and report
  how many were skipped, so the rest of the document still converts.

---

## 🔐 Privacy & Security

- **Zero uploads** — All files are processed locally in your browser. Nothing is ever sent to any server.
- **No account required** — No sign-up, no tracking, no cookies.
- **No storage** — Files are never persisted. Once you close the tab, everything is gone.
- **Open source** — Full transparency. The entire application is a single HTML file you can inspect, download, and self-host.

---

## 🚀 Getting Started

Simply open the [live site](https://backuprp2temp-oss.github.io/I-FUCK-PDF/) in any modern browser.

To self-host:

```bash
git clone https://github.com/backuprp2temp-oss/I-FUCK-PDF.git
cd I-FUCK-PDF
# Serve the directory with any HTTP server:
python -m http.server 8000
# or
npx serve .
```

Then open `http://localhost:8000` in your browser.

> **Note:** Some tools (OCR, PDF.js rendering) require the page to be served over HTTP (not opened as a `file://` URL) due to browser CORS and Web Worker restrictions.

---

## 🛠️ Tech Stack

| Layer | Technology |
|-------|-----------|
| **UI** | Tailwind CSS (CDN) for layout scaffolding, a custom token + component layer for everything visual, Lucide Icons |
| **Typography** | Inter (interface), JetBrains Mono (machine values) |
| **PDF** | PDF-Lib, pdf.js |
| **Office** | PptxGenJS, docx, SheetJS |
| **OCR** | Tesseract.js |
| **Utilities** | JSZip, SortableJS |
| **Encryption** | Custom MD5 + RC4 implementation (PDF 2.0 spec) |
| **Runtime** | 100% client-side — no backend, no build step |

---

## 📁 Project Structure

```
I-FUCK-PDF/
├── index.html   # Single-page application (all HTML, CSS, and JS)
└── README.md    # This file
```

The entire application is a **single HTML file** — no build tools, no package managers, no dependencies to install.

---

## 🎨 Design System

The interface is one restrained system rather than a per-screen set of styles.
Adding a tool means composing existing parts, not inventing new ones.

**Palette budget — a warm paper canvas, one ink, a three-step neutral ramp, and a
single chromatic accent** reserved for trust and success signals. Nothing else gets
a hue, which is what keeps 30 tools looking like one product.

| Role | Token | Value |
|------|-------|-------|
| Canvas | `--canvas` | `#fafaf9` |
| Surface | `--surface` | `#ffffff` |
| Muted surface | `--surface-2` | `#f4f3f0` |
| Hairline | `--line` | `#e5e4de` |
| Ink (also the primary action) | `--ink` | `#1a1a17` |
| Body text | `--ink-2` | `#45443e` |
| Secondary text (≥ 4.5:1) | `--muted` | `#6a6960` |
| Accent — trust & success | `--brand` | `#0f6b52` |
| Danger / warning | `--danger` / `--warn` | `#9f2d1c` / `#7d4f0d` |

**Other decisions**

- **Hierarchy from type and space**, not borders and shadows. Shadows are reserved
  for what genuinely floats: the header, dialogs, the sticky action bar.
- **A 4 / 6 / 8 / 12 px radius scale**, used deliberately rather than one radius
  applied everywhere.
- **Inter for interface text, JetBrains Mono for machine values** — file sizes, page
  counts, pixel dimensions, engine names. Mono is what makes a metadata line read as
  data rather than a sentence.
- **Motion is 110–280 ms**, easing out, and is fully disabled under
  `prefers-reduced-motion`.
- **One focus ring everywhere** (a 2 px ink outline) and no `outline: none` without
  a replacement.

**Shared components** live in one place near the top of the script, so a screen is
described rather than hand-built:

| Helper | Produces |
|--------|----------|
| `UI.panel` `UI.field` `UI.range` `UI.toggle` `UI.select` | Settings blocks and form controls |
| `UI.chipGroup` `UI.tileGroup` `UI.swatches` `UI.picker` | Exclusive choice groups |
| `UI.dropzone` `UI.fileCard` | File input and selected-file summary |
| `UI.action` `UI.secondaryAction` `Wire.actions` `Wire.actionPair` | Buttons and the sticky action bar |
| `UI.alert` `UI.result` `UI.note` | Success, error, warning and aside states |
| `UI.pageGrid` `UI.fileRows` | Thumbnail grids and multi-file lists |
| `Wire.fail` `Wire.warn` | The shared failure and "not quite" paths |

**Accessibility**

- Every control is a real `<button>`, `<a>` or labelled form field — no click
  handlers on `<div>`s.
- Position pickers, colour swatches and option groups are keyboard-operable and
  expose `aria-pressed`.
- Results announce through `role="status"`, failures through `role="alert"`, and the
  tool search announces its result count on every keystroke.
- `Escape` closes a workspace or dialog and returns focus to where it came from.
  `/` focuses the search field.
- Tools are deep-linkable (`#merge-pdf`), and focus moves into the workspace on open.

---

## 🤝 Contributing

Contributions are welcome! Since the entire app is a single HTML file, most changes are straightforward:

1. Fork the repository
2. Make your changes in `index.html`
3. Submit a pull request

### Adding a tool

1. Add an entry to `TOOL_META` (name, category, icon, a one-line description and a
   capability tag). This is what makes it appear in the library — the landing page
   has no hard-coded tool list.
2. Add a `TOOLS['<id>']` definition with `name`, `icon`, `state`, `render()`,
   `init()` and `cleanup()`.
3. Build the screen from the `UI` helpers above. Keep every `id` unique and
   prefixed with the tool id.
4. `render()` returns markup only; `init()` wires behaviour. With no build step and
   no framework, keeping the two apart is what prevents them drifting.

---

## 📄 License

This project is open source. See the repository for license details.

---

## ⚠️ Disclaimer

This tool is provided for legitimate document processing purposes only. The encryption features (Protect PDF / Unlock PDF) implement standard PDF security mechanisms and should be used in compliance with applicable laws and regulations.
