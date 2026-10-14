# Fluent File-Type Icons — Windows 11 Pack

High-quality **`.ico`** files for **92 file-type icons** from Microsoft's Fluent design system, rebuilt to the same internal standard Windows 11 uses, plus the complete source PNG set they were built from.

| | |
|---|---|
| Icons | **92** (covering **528** file extensions) |
| `.ico` sizes per file | 16 · 20 · 24 · 32 · 40 · 48 · 64 · 96 · 128 · **256** px |
| Source PNG sizes | 8 base sizes × 5 pixel ratios (1x–4x), up to 384 × 384 px |
| Total | ~15 MB of ICOs, ~22 MB of PNGs |

## Preview

| | | | | | |
|---|---|---|---|---|---|
| ![docx](png/48/docx.png) | ![xlsx](png/48/xlsx.png) | ![pptx](png/48/pptx.png) | ![pdf](png/48/pdf.png) | ![csv](png/48/csv.png) | ![code](png/48/code.png) |
| docx | xlsx | pptx | pdf | csv | code |
| ![html](png/48/html.png) | ![zip](png/48/zip.png) | ![txt](png/48/txt.png) | ![email](png/48/email.png) | ![photo](png/48/photo.png) | ![folder](png/48/folder.png) |
| html | zip | txt | email | photo | folder |

## Repository layout

```
├── ico/              92 ready-to-use multi-resolution .ico files  ← you probably want these
├── png/              source renders, mirroring the CDN layout
│   ├── 16/…96/       1× renders (16→96 px)
│   ├── 16_1.5x/…     high-DPI renders (1.5x / 2x / 3x / 4x, up to 384 px)
├── manifest.json     full extension→icon map + CDN provenance + build notes
└── LICENSE           MIT (Microsoft Corporation) — inherited from the source package
```

## Why these ICOs are high quality

- **Every size is a native render, not a resample.** Windows scales icons per DPI; each of the 10 sizes inside every `.ico` is taken from Microsoft's exact-size CDN render at that resolution, so there is no interpolation blur at any zoom level. (The only exception: 6 Power BI / campaign icons whose 128/256 px renders Microsoft never published — those are Lanczos-downscaled from the 288/384 px renders.)
- **Windows 11-standard entry format.** Sizes below 256 px are stored as 32-bit BGRA bitmaps with alpha; the 256 px entry is PNG-compressed. This is the exact hybrid Microsoft's own Windows 11 file icons use, giving maximum Explorer compatibility at every size.
- **Verified.** All 92 files were programmatically QA'd: entry structure parsed, every frame compared pixel-for-pixel against its source render, and the whole pack loaded through Windows GDI+ with zero failures.

## Usage

Use any `.ico` directly in Windows — shortcuts, file-type associations, installers, or the registry:

```
HKCR\.docx\DefaultIcon  →  C:\icons\docx.ico
```

In code, just load the file and request a size — Windows picks the sharpest frame automatically
(e.g. .NET: `new Icon("docx.ico", 256, 256)`; Win32: `SHDefExtractIcon(..., 256, ...)`).

To find the icon for a given extension (`.mdb` → `accdb`, `.7z` → `archive`, …), look it up in
`manifest.json` → `extension_to_icon`. Unknown extensions fall back to `genericfile` in the
original library.

## Provenance

Icons sourced from the CDN that
[`@fluentui/react-file-type-icons@8.18.2`](https://www.npmjs.com/package/@fluentui/react-file-type-icons)
registers (`res.cdn.office.net/…/assets/item-types/`), downloaded 2026-10-14. See `manifest.json`
for the exact base URL, the list of the 18 CDN URLs that 404, and per-folder pixel dimensions.

## License

The icons are © **Microsoft Corporation**, released under the [MIT license](LICENSE) as part of the
Fluent UI project. This repository is a packaging/redistribution of those assets for convenient
Windows use.
