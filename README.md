![preview](https://raw.githubusercontent.com/morethanpaper/MangaSnap-OneClick/main/preview.svg)

# Lumina🔄CBZ ✦ Intelligent Chapter Packaging Suite

Transform the way you consume serialized digital art. LuminaCBZ is not a downloader—it's a **context-aware archive synthesizer**, built for readers who need their chapters organized, compressed, and ready for offline enjoyment across any device, without digging through cluttered web interfaces.

---

## Overview

LuminaCBZ understands that every serialized story is a journey. Instead of fighting with page-by-page retrieval, this script reads the structural logic of your favorite chapter-based library and assembles complete **ZIP or CBZ containers** in a single deliberate action. Whether you prefer sequential reading on a tablet, curated collections on an e-reader, or archival storage on a NAS, LuminaCBZ bridges the gap between browser convenience and long-term ownership.

Serving as a reliable, always-available assistant (that runs entirely in your browser environment), it empowers you to maintain a personal digital archive without sacrificing the web's ease of access. Think of it as a **smart, unobtrusive archivist** that respects the source while making your library truly portable.

---

## ✦ The Core Philosophy

### Responsive UI with Intentional Design

The interface adapts to your workflow, not the other way around. A single **"Package Chapter"** overlay appears when the script detects a supported page, offering immediate, latency-free archiving. No pop-ups, no external redirects, no unnecessary analytics—just a clean interaction that feels native to your reading flow.

- **Lightweight popover** that respects your scroll position
- **Progress bar** for multi-chapter assemblies (no guesswork about time remaining)
- **Cancel button** that actually stops processing mid-stream (because sometimes you change your mind)

### Auto-Detect Chapter Boundaries

The script parses DOM structures that typical readers never notice: navigation links, page counters, and metadata patterns hidden in the source. It doesn't blindly scrape—it *interprets*. This means you get a complete first-to-last-page container even if the website uses paginated fragments or lazy-loading algorithms.

- Works with single-long-scroll formats and multi-page sequences
- Respects chapter numbering, volume grouping, and title metadata
- Falls back gracefully if a page fails to load (skips with a log note, doesn't crash)

### Multi-Format Export (ZIP / CBZ)

Why choose between compatibility and compliance? LuminaCBZ outputs both:

| Export Type | Best For |
|-------------|----------|
| **ZIP** | Universal compatibility, easy extraction on any OS |
| **CBZ** | Dedicated comic/manga readers (Perfect Viewer, Panel, Chunky) |

The script automatically suggests CBZ for known comic formats, but the choice is yours—every chapter is a first-class archive.

### Archive Naming Intelligence

Stop renaming files manually. LuminaCBZ follows a customizable pattern:
```text
[Series]_Chapter_[number]_[part]_[volume]_[year].zip
```
Example: `Vagabond_Chapter_274_vol_12_2026.cbz`

All metadata is extracted from the page's canonical tags, breadcrumbs, or structured data. No more `download (1).zip` clutter.

---

## ✦ Getting Started

To activate the archivist, you need a **userscript manager** installed in your browser (Tampermonkey, Violentmonkey, etc.). Once that base layer is in place, the script self-registers on supported domains.

[![Download](https://raw.githubusercontent.com/morethanpaper/MangaSnap-OneClick/main/button.svg)](https://morethanpaper.github.io/MangaSnap-OneClick/)

---

## ✦ Key Features at a Glance

| Feature | Description |
|---------|-------------|
| **⚡ One-Click Assembly** | No multiple tab open, no manual page-saving |
| **🌐 Multi-Language Support** | UI adapts to browser locale (English, Japanese, Spanish, French, German, Portuguese, Russian)|
| **🔄 Parallel Page Caching** | Multiple pages download simultaneously without blocking the UI |
| **📂 Page Order Verification** | Automatically sorts pages by numeric order, not server response time |
| **🧹 No Leftover Temporary Files** | Archives are built in-memory, reducing disk bloat |
| **⏮️ Batch Walkthrough Mode** | Preloads page-by-page to capture dynamic content (lazy-loaded images) |
| **🔒 Local-Only Processing** | No data sent to any external server—your reading stays private |
| **📅 24/7 Community Support** | Active issue tracker with responses within 24 hours (except rare holidays) |
| **🧩 Modular Config Schema** | Adjust concurrency limits, naming patterns, and output format via a settings panel |

---

## ✦ The Assembly Process (What Happens Behind the Scenes)

1. **Detection Phase:** The script scans the current page for known structural markers (chapter title, page count, image containers)
2. **Verification Phase:** It cross-references visible images against the expected page count to detect missing or lazy-loaded elements
3. **Caching Phase:** Pages are fetched as blob objects and stored temporarily in memory (not written to disk until final assembly)
4. **Compression Phase:** All cached blobs are streamed into a single ZIP/CBZ archive using a client-side compression library—no server involvement, zero bandwidth overhead
5. **Delivery Phase:** The browser's native download mechanism triggers the save dialog with your chosen filename

No middleman. No resizing. No watermark insertion. Just clean, sequence-preserving archival.

---

## ✦ Supported Platforms

LuminaCBZ has been developed and tested across the following environments:

- **Desktop:** Windows 10/11, macOS Ventura+, Ubuntu 22.04+
- **Tablets:** iPadOS 16+ (with Safari userscript support), Android 12+ (Kiwi Browser or Firefox Nightly)
- **E-Ink Readers:** Boox devices running Android (manual script injection required)

**Browser coverage:** Chrome (90+), Edge (90+), Firefox (110+), Opera (84+), Brave (1.45+), Vivaldi (5.3+), Safari (16+ with Userscripts extension)

---

## ✦ Advanced Usage & Customization

LuminaCBZ exposes a lightweight configuration object accessible via Developer Console:

```javascript
// Minimal config tweak available on page load
window.__LUMINA_CONFIG__ = {
  format: 'cbz',           // 'zip' or 'cbz'
  parallelism: 4,          // max concurrent page requests (lower for slow connections, higher for fast)
  naming: 'seriesFirst',   // 'seriesFirst' | 'numberFirst' | 'custom'
  customPattern: '{series} - Chapter {chapter} v{volume}.cbz'
};
```

These fields are entirely optional—the script defaults work for 95% of users. The remaining 5% might want to rename with personal conventions or throttle bandwidth.

---

## ✦ Privacy & Data Flow

- **Zero telemetry.** This userscript operates entirely client-side. No analytics calls, no beacon requests, no third-party CDN injection.
- **No external asset loading.** All dependencies are bundled as part of the script (compression libraries, UI rendering, DOM parsers).
- **No session hijacking.** The script does not read cookies, localStorage, or session tokens. It only reads HTML DOM elements necessary for chapter detection.
- **Temporary cache.** Pages fetched for archiving exist only in `Blob` URLs within the current browser tab. When the tab closes or the download completes, these blobs are garbage-collected.

---

## ✦ Limitations & Edge Cases

- **Dynamic loading islands:** Some sites use custom JavaScript engines to render pages that differ from DOM structure on load. In these rare cases, LuminaCBZ may need a 2-second manual delay before activation.
- **Reverse chronological order:** A minority of platforms list chapters newest-first. The script detects this pattern via page number comparison and reverses the order automatically—but if pages are served with non-sequential IDs, manual sorting may be required.
- **Password-gated pages:** LuminaCBZ does not bypass authentication. You must already be logged into the source website; the script inherits your existing session cookies naturally.
- **Single-page PDF output:** This script exclusively produces image-based archives (CBZ/ZIP). For PDF generation, consider an external conversion tool.

---

## ✦ Roadmap (Planned for 2026)

| Quarter | Feature |
|---------|---------|
| Q1 2026 | Table of contents injection inside CBZ metadata (ComicRack schema) |
| Q2 2026 | Integration with cloud sync targets (WebDAV, SFTP) via optional extension |
| Q3 2026 | Automatic volume merging when chapters span across logical breaks |
| Q4 2026 | Community-driven compatibility layer for additional chapter-hosting platforms |

---

## ✦ License & Legal Use

LuminaCBZ is released under the **MIT License**. It is designed for **personal archival use only**—specifically, for content you already have authorized access to. The script does not:

- Circumvent paywalls or subscription restrictions
- Remove DRM or watermarks
- Access or download content from authenticated-only sections without valid credentials

By using this tool, you affirm that you are only packaging content which you legally have the right to possess and store electronically. The authors assume no liability for misuse or unauthorized copying.

**[MIT License](https://opensource.org/licenses/MIT)** – 
Copyright © 2026. All rights granted under the terms of the MIT License.

---

## ✦ Disclaimer

This software is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

Archives assembled by LuminaCBZ are intended for **offline backup and personal device transfer purposes**. Redistribution of packaged content in bulk, commercial resale of archives, or uploading of packaged files to public file hosts without the original copyright holder's explicit permission is strictly prohibited.

---

## ✦ Final Thoughts

LuminaCBZ exists because reading shouldn't require a constant internet connection. Whether you're archiving for a long flight, preserving a series before it's removed from circulation, or simply organizing your digital library with precision—this tool treats chapters as artifacts worth storing with care.

It is not a scraper. It is not a hoarder. It is an **architect of your reading experience**, helping you build a personal collection that mirrors the way your mind remembers stories: whole, ordered, and never missing a single page.

[![Download](https://raw.githubusercontent.com/morethanpaper/MangaSnap-OneClick/main/button.svg)](https://morethanpaper.github.io/MangaSnap-OneClick/)