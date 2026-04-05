# Codex Build Prompt — Web Performance & Snappy UI Deep Dive Guide

## What to Build

Create a single self-contained HTML file:
**`2026-03-30_web-performance-snappy-ui-guide.html`**

This is an **interactive educational guide** — a rich, visually polished, multi-section deep dive on building fast, snappy, data-rich web applications. It should feel like a premium interactive textbook, not a blog post. Think: opinionated, technical, visual, hands-on.

The audience is **Blake** — a technically-oriented builder (not a senior browser engineer) who is building data-rich apps: provider search tools, patient history visualizations, dashboards, maps. He cares deeply about making fast software and wants to understand the *why* behind performance decisions so he can make the right architecture calls.

---

## Sections (in order)

### 0. Hero / Introduction
- Title: **"Building Snappy: The Developer's Guide to Web Performance"**
- Subtitle: "Why your app feels slow — and how to fix it at the architecture level"
- Quick nav bar linking to all sections

---

### 1. How Browsers Actually Work (The Rendering Pipeline)
**Goal:** Make the DOM, layout, and paint pipeline concrete and visual.

Content:
- The browser's main thread: JS execution → Style → Layout → Paint → Composite
- **Visual pipeline diagram** — animated or illustrated step-by-step flow showing how a user action triggers a render cycle
- What "reflow" (layout thrashing) is and why it kills performance
- The 16ms frame budget at 60fps / 8ms at 120fps — make this visceral
- **Interactive demo:** A simple counter showing frame budget consumed. Show a "bad" example (interleaved DOM reads/writes in a loop) vs. "good" (batched). Use `performance.now()` to measure and display actual ms.
- Key takeaway callout box: "Every DOM geometry query you make inside a loop is potentially burning your frame budget."

---

### 2. The DOM vs. Canvas/WebGL — Choosing Your Rendering Model

**Goal:** Explain the three rendering models with concrete tradeoffs.

**Side-by-side comparison table:**

| | DOM | Canvas 2D | WebGL |
|---|---|---|---|
| Best for | Interactive UI, forms, text content | Custom 2D graphics, charts, games | Maps, 3D, millions of data points |
| Layout engine | Browser handles it | You handle it | You handle it |
| Performance ceiling | Medium | High | Very high |
| Dev complexity | Low | Medium | High |
| Examples | React apps, tables, forms | Chart.js, Pretext, custom timelines | Mapbox, Deck.gl, Figma |

Content:
- When DOM is the right call (and when it isn't)
- Canvas 2D: pixel-perfect rendering, no reflow, but you own hit-testing and accessibility
- WebGL: GPU-accelerated, handles millions of primitives, used by every major map and visualization platform
- **Cheng Lou's Pretext** — explain it as a hybrid approach: use Canvas's font measurement engine as ground truth, but deliver pure arithmetic for layout. 300–500x faster text measurement. Relevant for data-dense UIs.
- **Interactive toggle:** Two side-by-side divs rendering 500 colored blocks — one DOM-based, one Canvas-based. Button to stress-test both and show FPS difference.

---

### 3. The Big Four Patterns for Snappy Data-Rich Apps

Four expandable "pattern cards", each with:
- Problem it solves
- How it works (diagram or visual)
- Code example (syntax highlighted)
- When to use / when not to use
- Libraries to reach for

**Pattern 1: Virtualization (Only Render What's Visible)**
- How virtual scrolling works: render window, recycled DOM nodes, height calculation
- The variable-height problem: why you need exact row heights before render
- Code: TanStack Virtual minimal example with a 50,000 row list
- Libraries: TanStack Virtual, react-window, AG Grid

**Pattern 2: Server-Side Data Operations**
- Never filter/sort 50K rows in JavaScript — SQL is orders of magnitude faster
- Pagination vs. infinite scroll — tradeoffs
- Search-as-you-type architecture: debounce → API → minimal JSON → render
- DuckDB as a secret weapon: sub-100ms queries on millions of rows
- Code: debounced search input → fetch → render pattern

**Pattern 3: Web Workers — Don't Block the Main Thread**
- What a Web Worker is: a separate JS thread that can't touch the DOM
- What to offload: FHIR bundle parsing, heavy data transforms, search indexing
- The postMessage pattern: worker ↔ main thread communication
- Code: minimal Web Worker example — parse a large JSON off-thread, post results back
- Real-world: parsing a 1,180-patient FHIR corpus in a worker vs. freezing the UI

**Pattern 4: Maps — Canvas/WebGL or Die**
- Why DOM map pins don't scale past ~500 markers
- Clustering: never render individual pins at zoom-out, use supercluster
- Stack recommendation: Mapbox GL / MapLibre → Deck.gl for data layers
- What Deck.gl enables: heatmaps, hexbin, scatter, arc layers — millions of points, 60fps
- Code: minimal Mapbox + cluster example

---

### 4. Performance Metrics — What "Snappy" Actually Means

**Goal:** Give Blake a framework for measuring and talking about performance.

Content:
- The three feelings users have and their metrics:
  - "It responded" → Input latency <100ms
  - "It loaded" → Time to Interactive <3s
  - "It's smooth" → 60fps (frame rate)
- The 100ms wall: users feel delays above 100ms. At 300ms they think it's slow. At 1s they think it's broken.
- **Browser DevTools guide** — annotated screenshots (or diagrams) showing:
  - Performance tab: flame chart, main thread, frame timeline
  - Network tab: waterfall, timing, payload size
  - Lighthouse: what each score means, what to fix first
- **The RAIL model** (Response, Animation, Idle, Load) — Google's framework for UX-driven performance goals

---

### 5. The Performance Screener Tool (Interactive)

**Goal:** A built-in diagnostic tool Blake can use when evaluating any app or planning a build.

Two modes:

**Mode A — "Rate My Stack"**
A checklist UI where you check off your stack and architecture choices:
- [ ] I have tables with >500 rows
- [ ] I'm rendering map pins as DOM elements
- [ ] I filter/sort data in JavaScript on the client
- [ ] I parse large files synchronously on the main thread
- [ ] I have search that hits the server on every keystroke
- [ ] I'm using a DOM-based chart library with >1,000 data points
- [ ] I'm not virtualizing long lists

As you check items, a **risk score** builds up with color-coded severity (green/yellow/red) and a personalized recommendation for each checked item.

**Mode B — "App Anatomy Checklist"**
A structured pre-build checklist for new applications:
- Data volume assessment (how many rows? how often does it change?)
- Rendering model decision (DOM / Canvas / WebGL)
- Data fetching strategy (server-side ops? pagination? real-time?)
- Worker strategy (what computation goes off-thread?)
- Map strategy (does it need maps? what's the data density?)

Both modes produce a **"Performance Blueprint"** summary at the bottom — a paragraph describing the recommended architecture for that use case.

---

### 6. Architecture Patterns Side-by-Side

**Goal:** Show concrete before/after for common mistakes Blake might make.

Three comparison cards, each showing:
- ❌ The Slow Way (with annotated code + explanation of why it's slow)
- ✅ The Fast Way (with annotated code + explanation of why it's faster)
- FPS/latency impact estimate

**Comparison 1: Table Rendering**
- ❌ Render 10,000 `<tr>` elements, sort with JS array sort, re-render all
- ✅ Server-side sort, virtual scroll, only 30 DOM rows at any time

**Comparison 2: Search**
- ❌ Filter a 50K item array on every keypress with `array.filter()`
- ✅ Debounce 150ms → server query → DuckDB full-text → return 20 results

**Comparison 3: Map Pins**
- ❌ 2,000 `<div>` markers in the DOM, all rendered at once
- ✅ MapLibre/Mapbox + supercluster, WebGL rendering, dynamic clustering

---

### 7. The Stack Cheat Sheet

A quick-reference card for Blake's specific build context:

| Need | Reach For | Why |
|---|---|---|
| Large data tables | TanStack Table + TanStack Virtual | Best-in-class, framework-agnostic, virtualization built in |
| Search-as-you-type | Debounce + DuckDB/Postgres FTS | Server-side is always faster for large datasets |
| Maps with many markers | Mapbox GL / MapLibre | WebGL rendering, scales to millions of points |
| Data visualization layers on maps | Deck.gl | Built for exactly this — heatmaps, scatter, hexbin |
| Heavy parsing / computation | Web Workers | Keep the main thread free for UI |
| Text measurement at scale | Pretext (@chenglou/pretext) | 300–500x faster than DOM measurement |
| Complex data viz / timelines | Plotly (small) / Canvas-based (large) | DOM charting falls apart >1K data points |
| Real-time data | WebSockets + optimistic UI | Don't poll, push. Update UI before server confirms. |

---

## Visual Design

Match the style of existing reports in this repo (see `2026-03-27_38-oakwood-geotech-cost-analysis.html` as reference):

- Dark gradient hero header with title + subtitle
- Clean card-based layout, `max-width: 900px` centered
- CSS custom properties for color theming
- **Color palette for this guide:** tech/blue theme
  - `--deep: #0f172a` (dark navy)
  - `--mid: #1e3a5f` (medium navy)  
  - `--accent: #3b82f6` (blue)
  - `--accent-green: #10b981` (green for "fast/good")
  - `--accent-red: #ef4444` (red for "slow/bad")
  - `--bg: #f8fafc`
  - `--card: #ffffff`
- Section headers with numbered badges
- Code blocks with syntax highlighting (use highlight.js CDN or hand-style with `<pre><code>`)
- Callout boxes: "Key Insight", "Warning", "Rule of Thumb"
- Interactive elements styled as clean toggle buttons, not plain checkboxes
- Mobile responsive

---

## Technical Requirements

- **Single self-contained HTML file** — all CSS and JS inline, no external dependencies except CDN links (highlight.js for code, that's it)
- All interactive demos must work without a server — pure client-side JS
- The performance demos (Section 2's DOM vs Canvas comparison) must actually run and show real FPS numbers
- The screener tool (Section 5) must be fully functional — checkboxes → score → recommendations
- Use `performance.now()` for actual timing measurements in demos
- No frameworks (React, Vue) — vanilla JS only for the interactive demos
- Syntax-highlighted code blocks for all code examples

---

## File Naming & Output

Output file: `2026-03-30_web-performance-snappy-ui-guide.html`
Place in: `~/Repo/mobile-reports/`

After creating the file, update `index.html` in the same directory to add a link to this new guide (follow the existing pattern in index.html for adding new report cards).

Then commit and push:
```bash
git add 2026-03-30_web-performance-snappy-ui-guide.html index.html
git commit -m "feat: Add Web Performance & Snappy UI interactive guide"
git push
```

The guide will be live at:
`https://blakethom8.github.io/mobile-reports/2026-03-30_web-performance-snappy-ui-guide.html`

---

## Quality Bar

This should be one of the best things in this repo. It's going to be a reference document Blake comes back to repeatedly and potentially shares. Take the time to make the interactive demos actually work, the code examples actually correct and copy-paste ready, and the visual design polished. Aim for something that feels like a premium interactive course module, not a quick blog post.

Length target: 800–1,200 lines of HTML.
