# YMS Lab 🧪⚡
### *Any Input. Any Format. Always Polished.*

> A PWA (installable web app) for students and corporate professionals that takes any messy, unstructured, low-quality data — Word docs, Excel sheets, PDFs, PowerPoints, raw text, CSVs — and transforms it into beautifully formatted, professional-grade Excel workbooks, PowerPoint decks, infographics, and dynamic illustrations using AI — with offline support built in.

---

<br/>

##  What Is YMS Lab? 

Imagine you have a huge pile of crumpled, messy notes thrown all over the floor. Some are random paragraphs. Some are broken tables. Some are bullet points that make no sense. None of it looks presentable.

Now imagine a magic machine. You throw all those messy notes in — and out comes a perfectly organised, beautifully designed document with proper headings, clean charts, right colours, correct formatting, and everything in exactly the right place.

**That's YMS Lab.**

You give it anything:
- A messy Word document you typed at 2 AM 📄
- A broken Excel sheet someone emailed you 📊
- Lecture notes you scribbled in a rush 📝
- A rough PDF report with no structure 📑
- Raw text you just pasted from anywhere 📋

And it gives you back:
- A clean, professional Excel workbook ✅
- A polished, themed PowerPoint deck ✅
- A stunning, data-driven infographic ✅
- A stylised illustration or visual ✅

It uses **Artificial Intelligence** to read and understand your chaotic input, figure out what it's really about, decide the best way to organise it, and then build a clean professional version — fully formatted, validated, and ready to use or present.

No design skills needed. No manual formatting. No broken exports. Ever.

---

<br/>

## 🎯 Who Is This For?

| User | Their Problem | How YMS Lab Helps |
|------|-------------|-------------------|
| **Students** | Messy lecture notes, scattered research, rough drafts before exams | Converts notes into revision decks, study sheets, visual summaries |
| **Corporate Workers** | Raw meeting notes, unformatted reports, rough data from multiple sources | Turns them into client-ready decks, clean reports, polished Excel models |
| **Anyone** | Any disorganised file or text that needs to look professional | One upload → professional output, every time |

---

<br/>

## 🔄 Full Workflow — Step by Step

```
┌─────────────────────────────────────────────────────────────────┐
│                         YMS LAB PIPELINE                        │
│                                                                 │
│  YOU UPLOAD          AI PROCESSES           YOU DOWNLOAD        │
│  ──────────          ────────────           ────────────        │
│  Word / Excel   →    Read & Parse      →                        │
│  PDF / PPT      →    AI Understands    →    Excel Workbook      │
│  CSV / Text     →    Structures JSON   →    PowerPoint Deck     │
│  Pasted notes   →    Picks Output      →    Infographic SVG     │
│  (any quality)  →    Builds File       →    Illustration        │
│                 →    Validates File    →    (preview first)     │
│                 →    Shows Preview     →    ✅ Download          │
└─────────────────────────────────────────────────────────────────┘
```

<br/>

### 📂 Step 1 — Upload Anything
You drag and drop a file, paste raw text, or upload from your device. YMS Lab accepts all of these:

| Input Type | File Extension | Notes |
|-----------|---------------|-------|
| Word Document | `.docx` | Any formatting quality — even totally broken |
| Excel / Spreadsheet | `.xlsx`, `.csv` | With or without proper structure |
| PDF | `.pdf` | Text-based or scanned (OCR in Phase 2) |
| PowerPoint | `.pptx` | Old decks with inconsistent formatting |
| Plain Text | `.txt` | Raw notes, copied content, anything |
| Pasted Text | — | Direct paste into the input area |

The quality of what you upload literally does not matter. Messy, inconsistent, half-finished — all fine.

---

### 🔍 Step 2 — Reading Your File (Parsers)
*"Before understanding, we read."*

YMS Lab doesn't just look at your file — it reads inside it and extracts every piece of text, number, structure, and data hidden in there. Different file types speak different languages, so we use different "reader" libraries for each:

| File Type | Library | What It Does |
|-----------|---------|-------------|
| `.docx` (Word) | **mammoth.js** | Extracts text, headings, lists, tables from Word format — even preserving document hierarchy |
| `.xlsx` / `.csv` | **SheetJS (xlsx)** | Reads every cell, row, column, and formula from Excel and CSV files |
| `.pdf` | **pdf.js** | Parses PDF page-by-page and extracts raw text content |
| `.pptx` | **pptxgenjs** | Reads slide titles, content blocks, and speaker notes from PowerPoint files |
| Plain text | Native JS | Read directly — no library needed |

Think of these as **translators** — each one speaks a different file language and converts it into plain text + structure that the AI can understand.

---

### 🤖 Step 3 — AI Understands and Cleans Your Content
*"The smart brain figures out what your stuff is really about."*

This is the core of YMS Lab. After your file is read, its content is sent to the **Claude AI** (by Anthropic — one of the most capable AI systems in the world). But we don't just dump the text and hope for the best.

We give Claude a very precise, structured prompt:

> *"Here is raw content from a user upload. It may be messy, inconsistent, or low quality. Your job is to: (1) understand what this content is about, (2) extract the key data, hierarchy, and intent, (3) clean it up, and (4) return ONLY a structured JSON object — no prose, no explanation, just the JSON."*

Claude responds with **clean, structured JSON** — a computer-friendly, organised summary of everything it found:

```json
{
  "title": "Q3 Sales Report",
  "intent": "financial_data",
  "confidence": 0.94,
  "sections": [
    {
      "heading": "Revenue",
      "type": "metric",
      "value": 142000,
      "unit": "USD",
      "trend": "up"
    },
    {
      "heading": "Top Products",
      "type": "table",
      "rows": [
        { "product": "Widget A", "units": 4200, "revenue": 84000 },
        { "product": "Widget B", "units": 2900, "revenue": 58000 }
      ]
    }
  ],
  "suggested_output": "excel"
}
```

This JSON is what the rest of the app runs on. The **AI never writes the file directly** — it only produces the structured data. The actual Excel/PPT/infographic is built by a separate, deterministic renderer fed by this JSON. This is what makes every export reliable and error-free, regardless of how chaotic the input was.

#### 💾 Prompt Caching
The system prompt (instructions given to Claude) is identical for every single user request. Instead of re-sending and re-paying for it every time, YMS Lab uses **prompt caching** — Anthropic stores the prompt on their side and charges only for the new content each time. This dramatically cuts API costs at scale.

#### 🛡️ Confidence Handling
If Claude returns a low-confidence result (e.g., `"confidence": 0.51`), YMS Lab does not crash or produce a broken output. Instead:
1. It degrades gracefully to a simpler-but-correct output template
2. It flags a review notice: *"We simplified the output — please check the preview before downloading"*
3. The user always gets something usable, never an error

---

### 🎛️ Step 4 — You Pick the Output
*"You decide what it becomes."*

Based on the AI's structured JSON, YMS Lab suggests the best output format — but you can always override it:

| AI Detected | Suggested Output | Override Options |
|------------|-----------------|-----------------|
| Financial data / tables | Excel Workbook | PPT, Infographic |
| Narrative / talking points | PowerPoint Deck | Excel, Illustration |
| Stats / comparisons | Infographic | Excel, PPT |
| Creative / conceptual | Illustration | Infographic, PPT |

You pick. The app listens. No forced decisions.

---

### 🔨 Step 5 — Building the Output (Renderers)
*"Now it actually makes the file — perfectly, every time."*

The structured JSON from the AI is fed into dedicated **renderer modules** — one for each output type. These are deterministic: same structured input always produces the same clean output. No randomness, no surprises.

#### 📊 Excel Renderer — `ExcelJS`
Builds a real, fully functional `.xlsx` file that opens in any version of Microsoft Excel or Google Sheets.
- Proper column headers with frozen top row
- Conditional formatting (cells colour based on values automatically)
- Auto-generated charts (bar, pie, line) from numerical data
- Formulas where appropriate (sums, averages)
- Correct column widths, font sizes, cell borders, alignment
- Multiple sheets if the content has multiple sections

#### 📽️ PowerPoint Renderer — `pptxgenjs`
Builds a real `.pptx` file that opens in PowerPoint, Keynote, or Google Slides.
- Auto-generated slide layouts: title slide, section dividers, content slides, chart slides
- Consistent theme applied throughout (fonts, colours, spacing, logo placeholder)
- Charts and data tables inserted as native slide elements (not images)
- Speaker notes added where content warrants it
- No text overflow, no clipped content, no broken layouts — ever

#### 🎨 Infographic Renderer — `SVG + Canvas API`
Builds a fully custom, data-driven infographic — rendered in the browser using scalable vector graphics.
- Template types: **Timeline**, **Comparison**, **Stat-Block**, **Process-Flow**, **Hierarchy**
- Everything is data-driven — numbers and proportions drive the visual, not manual positioning
- Scalable SVG output: looks crisp on any screen size or resolution
- Downloadable as `.svg` (for web/design) or rendered to `.png` for documents

#### 🖼️ Illustration Renderer — `SVG Icons + AI Visuals`
Generates stylised illustrations using SVG and icon libraries for visual explainers or cover images.
- For hero visuals or cover slides, optionally calls an AI image model to generate a bespoke image
- Output is embedded in your exported file

#### ✅ Validation (Non-Negotiable)
Before you ever see a download button, every output goes through an internal validator:

```
Is the file non-empty?           → ✅ / flag and retry
Does it open without errors?     → ✅ / flag and simplify
Are all expected sections there? → ✅ / flag missing sections
Is the file size reasonable?     → ✅ / flag if suspiciously small
```

If any check fails → graceful downgrade to simpler template + review flag.
If all checks pass → preview is shown and download is unlocked.

**You will never download a broken, empty, or corrupt file from YMS Lab.**

---

### 👁️ Step 6 — Preview and Download
*"See it before you take it."*

A live, interactive preview renders inside the app before you download:
- Excel: scrollable sheet with real cell data
- PPT: slide flipper showing every slide
- Infographic: full scrollable visual
- Illustration: full-size render

Light in-app edits are possible: rename a heading, tweak a colour, reorder a section. When you're satisfied — one click downloads the real, validated file.

---

<br/>

## 📴 Offline Architecture — What Works Without Internet

YMS Lab is a **PWA (Progressive Web App)** — meaning it can be installed on your phone, laptop, or desktop like a native app, and significant portions of it work without any internet connection.

Here is the honest breakdown of what works offline and what doesn't:

| Feature | Offline? | Reason |
|---------|---------|--------|
| Opening and loading the app | ✅ Yes | App shell is fully cached on your device |
| Browsing your history of past uploads and outputs | ✅ Yes | Stored in your browser's local database |
| Re-downloading any previously generated file | ✅ Yes | File is already saved locally |
| Re-theming or re-exporting a cached output | ✅ Yes | Renderer runs locally, no AI needed |
| **Uploading a new file and converting it** | ❌ Needs internet | The Claude AI model lives in the cloud |
| **New AI parsing of any content** | ❌ Needs internet | No viable in-browser model matches Claude quality |

The app always shows a clear **🟢 Online / 🔴 Offline** indicator so you always know exactly which features are available.

#### Technologies Behind Offline Support

| Technology | Role | Analogy |
|-----------|------|---------|
| **Service Worker** | Intercepts network requests and serves cached files when offline | A local assistant who has memorised the whole app |
| **Workbox** | A toolkit by Google that makes writing Service Workers reliable and easy | The instruction manual the assistant follows |
| **IndexedDB** | A full database built into your browser — stores files, history, outputs locally | A filing cabinet inside your browser |
| **Dexie.js** | A clean, promise-based JavaScript wrapper around IndexedDB | The labels and tabs on the filing cabinet |

---

<br/>

## 🧱 Full Tech Stack

### Frontend

| Tool | Version | Role | Why This One |
|------|---------|------|-------------|
| **React** | 18+ | UI component framework | Industry standard, massive ecosystem |
| **Vite** | 5+ | Build tool and dev server | Fastest build tool available |
| **TypeScript** | 5+ | Type-safe JavaScript | Catches bugs before runtime |
| **Tailwind CSS** | 3+ | Utility-first styling | Fast, consistent, no CSS file bloat |
| **Framer Motion** | 11+ | Animations and micro-interactions | Best-in-class React animation library |
| **Three.js / Spline** | Latest | 3D hero section and background 3D elements | Makes the landing page visually stunning |
| **Zustand** | 4+ | Global state management | Simpler and faster than Redux |

### File Parsers

| Library | Parses | Notes |
|---------|--------|-------|
| **mammoth.js** | `.docx` | Converts Word XML to clean HTML/text |
| **SheetJS (xlsx)** | `.xlsx`, `.csv` | Full spreadsheet read with structure |
| **pdf.js** | `.pdf` | Mozilla's battle-tested PDF reader |
| **pptxgenjs** | `.pptx` | Reads and generates PowerPoint files |

### AI Layer

| Component | Technology | Role |
|-----------|-----------|------|
| AI Engine | **Anthropic Claude API** | Core intelligence for understanding and structuring content |
| Default Model | **Claude Sonnet 4.6** | Main parsing and structuring model |
| Fast Model | **Claude Haiku 4.5** | Quick classification and sub-tasks |
| Power Model | **Claude Opus 4.8** | Complex, long, or low-confidence documents |
| Output Format | **Structured JSON via prompt** | Forces deterministic, parseable output — never freeform prose |
| Cost Optimisation | **Prompt Caching** | System prompt cached — not re-billed on every request |

### Output Generators

| Library | Generates | Output Format |
|---------|---------|--------------|
| **ExcelJS** | Excel workbooks | `.xlsx` |
| **pptxgenjs** | PowerPoint decks | `.pptx` |
| **SVG / Canvas API** | Infographics | `.svg` / `.png` |
| **AI Image Model** (optional) | Illustration hero images | Embedded in output |

### Offline Infrastructure

| Technology | Role |
|-----------|------|
| **Service Worker** | Caches full app shell for offline loading |
| **Workbox** | Manages caching strategies cleanly |
| **IndexedDB** | Browser-side database for uploads, outputs, history |
| **Dexie.js** | Developer-friendly IndexedDB wrapper |

### Backend (AI Orchestration Layer)

| Tool | Role |
|------|------|
| **FastAPI (Python) or Node.js** | Handles Claude API calls, auth, and any server-side heavy processing |
| **Vercel / Netlify** | Frontend hosting with one-command deploys |
| **Environment Variables** | API key and config stored securely, never in frontend code |

---

<br/>

## 📁 Project Structure

```
yms-lab/
│
├── public/
│   ├── manifest.json              # PWA manifest (app name, icons, theme colour)
│   ├── sw.js                      # Service Worker entry point
│   └── icons/                     # App icons for all screen sizes
│
├── src/
│   │
│   ├── pages/
│   │   ├── Landing.tsx            # 3D animated home/marketing page
│   │   └── Workspace.tsx          # Main conversion workspace UI
│   │
│   ├── components/
│   │   ├── UploadZone.tsx         # Drag-and-drop + file picker input area
│   │   ├── OutputPicker.tsx       # UI for choosing Excel / PPT / Infographic
│   │   ├── PreviewPanel.tsx       # Live preview of generated output before download
│   │   ├── StatusBar.tsx          # 🟢 Online / 🔴 Offline indicator
│   │   ├── HistoryDrawer.tsx      # Browse and re-export past files
│   │   └── ProgressTracker.tsx    # Step-by-step visual progress during conversion
│   │
│   ├── parsers/                   # File reading / input extraction
│   │   ├── wordParser.ts          # mammoth.js — reads .docx
│   │   ├── excelParser.ts         # SheetJS — reads .xlsx and .csv
│   │   ├── pdfParser.ts           # pdf.js — reads .pdf
│   │   ├── pptParser.ts           # pptxgenjs — reads .pptx
│   │   └── textParser.ts          # Native — reads raw plain text
│   │
│   ├── ai/                        # Everything Claude API related
│   │   ├── router.ts              # Picks Haiku / Sonnet / Opus per task complexity
│   │   ├── prompts.ts             # All system prompts — instructions to Claude
│   │   ├── structurer.ts          # Sends parsed content → Claude → gets JSON back
│   │   └── validator.ts           # Checks Claude's JSON is well-formed before use
│   │
│   ├── generators/                # Output file renderers
│   │   ├── excelGenerator.ts      # ExcelJS — builds .xlsx from structured JSON
│   │   ├── pptGenerator.ts        # pptxgenjs — builds .pptx from structured JSON
│   │   ├── infographicGenerator.ts # SVG/Canvas — renders infographic from JSON
│   │   ├── illustrationGenerator.ts # SVG + AI image — renders illustration
│   │   └── outputValidator.ts     # Validates every output file before download unlock
│   │
│   ├── store/
│   │   └── appStore.ts            # Zustand — global state (upload, AI stage, output)
│   │
│   ├── offline/
│   │   ├── db.ts                  # Dexie.js — IndexedDB schema and setup
│   │   └── cache.ts               # Save and retrieve past outputs locally
│   │
│   ├── utils/
│   │   ├── fileUtils.ts           # File type detection, size checks, MIME helpers
│   │   └── formatUtils.ts         # Formatting helpers (dates, numbers, units)
│   │
│   └── main.tsx                   # App entry point
│
├── workbox.config.js              # Service Worker caching rules
├── vite.config.ts                 # Vite build configuration + PWA plugin
├── tailwind.config.ts             # Tailwind design tokens and theme
├── tsconfig.json                  # TypeScript config
├── .env                           # API keys (never commit this)
├── .env.example                   # Template showing required env variables
├── .gitignore                     # node_modules, .env, dist excluded
└── README.md                      # This file
```

---

<br/>

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ installed
- An Anthropic API key from [console.anthropic.com](https://console.anthropic.com)

### Install and Run

```bash
# 1. Clone the repository
git clone https://github.com/yourusername/yms-lab.git
cd yms-lab

# 2. Install all dependencies
npm install

# 3. Set up your environment variables
cp .env.example .env
# Open .env and add your Anthropic API key:
# VITE_ANTHROPIC_API_KEY=sk-ant-xxxxxxxxxxxxxxxx

# 4. Start the development server
npm run dev

# 5. Open in your browser
# → http://localhost:5173
```

### Build for Production

```bash
npm run build       # Compiles + bundles everything
npm run preview     # Test the production build locally
vercel --prod       # Deploy to Vercel
```

The Service Worker and PWA manifest are auto-generated during build. After deployment, users can install YMS Lab from their browser directly to their home screen or desktop.

---

<br/>

## 🔐 Environment Variables

| Variable | Required | Description |
|---------|---------|-------------|
| `VITE_ANTHROPIC_API_KEY` | ✅ Yes | Your Claude API key from console.anthropic.com |
| `VITE_DEFAULT_MODEL` | Optional | Override default model (default: `claude-sonnet-4-6`) |
| `VITE_API_BASE_URL` | Optional | If using a backend proxy instead of direct API calls |

⚠️ **Never commit your `.env` file to GitHub. It's in `.gitignore` by default.**

---

<br/>

## 🎨 Design System

YMS Lab's UI is built around a single design principle:

> *"The interface gets out of the way. The transformation is the product."*

| Design Decision | Choice | Reason |
|----------------|--------|--------|
| **Mode** | Dark mode default | Professional, premium, easy on the eyes during late-night sessions |
| **Typography** | Satoshi / General Sans | Modern, clean, confident — not a generic Google Font |
| **Accent** | Single bold gradient | One strong colour direction, no visual noise |
| **Motion** | Purposeful 3D only | The landing page 3D shows a document literally morphing into a chart — that's the product story, not decoration |
| **3D Library** | Three.js / Spline | Smooth WebGL-powered 3D that runs in the browser with no app install |
| **Animations** | Framer Motion | Hover states, page transitions, progress indicators — all satisfying micro-interactions |
| **Skeleton Loaders** | Yes, during AI processing | The "waiting for AI" moment becomes a branded visual transformation instead of a boring spinner |

Reference products for design direction: **Linear** (polish), **Stripe** (storytelling), **Gamma** (clean output), **Arc Browser** (playful-premium).

---

<br/>

## 🗺️ Roadmap

| Phase | Features | Status |
|-------|---------|--------|
| **Phase 1 — MVP** | Upload txt/docx/csv/xlsx → Export Excel + PPT, PWA shell + offline history, 3D landing page, full validation pipeline | 🔨 Building |
| **Phase 2** | PDF + image/OCR input, Infographic + Illustration generators, in-app light editing, team sharing for corporate use | 📋 Planned |
| **Phase 3** | Lightweight offline AI fallback (transformers.js), template library, version history, collaboration features | 💡 Future |

---

<br/>

## 🏛️ Architecture Decisions — Why We Built It This Way

**Why does the AI return JSON instead of writing the file directly?**
If you ask an LLM to write an Excel file directly, you get inconsistent, often broken output — the model hallucinates formatting, invents columns, or produces malformed data. By separating the AI (understands content → returns JSON) from the renderer (consumes JSON → builds file), we guarantee every export is structurally correct. The AI handles intelligence; the renderer handles precision.

**Why three AI models instead of one?**
Cost and quality both matter. Running Claude Opus 4.8 on every single request — including simple ones like "is this financial data or a presentation?" — is like using a surgical robot to make toast. Routing by task complexity means quality where it counts and efficiency everywhere else.

**Why not just run the AI fully offline?**
There is no in-browser model today that matches Claude-level quality at parsing real-world messy documents. Promising full offline AI would mean shipping a lower-quality product and calling it the same thing. Instead, YMS Lab is honest: offline caching, history, and re-exports work fully; new AI parsing requires a connection. The UI tells you clearly which mode you're in.

**Why PWA instead of a native app?**
One codebase. Works on every OS. Installable from the browser. No App Store approval process. Updates instantly. For a tool used by students on college Wi-Fi and corporate workers on various devices, a PWA is a stronger practical choice than native apps for each platform.

---

<br/>
*YMS Lab — because your ideas deserve better than a messy file.*
