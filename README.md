<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="VisionTherapySuite/Assets.xcassets/AppIcon.appiconset/Untitled%20design.png">
    <img src="VisionTherapySuite/Assets.xcassets/AppIcon.appiconset/Untitled%20design-2.png" alt="Vision Therapy Suite icon" width="128" height="128">
  </picture>
</p>

<h1 align="center">Vision Therapy Suite</h1>

<p align="center"><strong>True-size therapy charts, fresh every time.</strong></p>

<p align="center">
  <img alt="iOS 17.6+" src="https://img.shields.io/badge/iOS-17.6%2B-black">
  <img alt="iPhone and iPad" src="https://img.shields.io/badge/iPhone%20%26%20iPad-universal-black">
  <img alt="SwiftUI" src="https://img.shields.io/badge/SwiftUI-Observation-black">
  <img alt="No dependencies" src="https://img.shields.io/badge/dependencies-none-black">
  <img alt="Data not collected" src="https://img.shields.io/badge/privacy-data%20not%20collected-black">
</p>

---

Vision Therapy Suite makes printable worksheets for optometrists and vision therapists. Pick your settings, tap **New Chart**, and print a sheet that's sized to the millimetre and different every time. Every chart has a short code on it, so you can bring back the exact same sheet, settings and all, whenever you need it.

No photocopying the same worn-out chart. No accounts. No cloud. Just charts.

## Features

### Visual Chart (Hart-style)
- **3×3 or 4×4 grids** of letters (A–Z, no repeats) or numbers (1–9).
- **1, 2 or 4 charts per page**, each a tight, evenly spaced card you could cut out.
- **True physical size.** Set the character height in **mm, pt or px**, down to 0.01 mm. A 12 mm letter prints at 12 mm.
- **Fonts and colour:** Mono, Sans, Rounded or Serif in black, red, green or blue, in four weights.
- **Border and grid lines**, each on its own switch.
- **Near/far pairs:** near cards matched to the wall chart's visual angle (wall at 2–6 m, near at 30–50 cm).

### Slap Tap
- **10 × 5 sheets** of b/d/p/q symbols in three levels: singles, doubles, then rests.
- **Glyph size and thickness** to suit the patient.
- **Built-in metronome:** 0–300 BPM, five sounds, accented beats, every-beat or every-bar clicks, tap tempo and a beat light.

### Both tools
- **Chart codes.** Every sheet's code (like `V3L1B12-1042`) brings back the same chart, layout, fonts and print settings. Patient details are never part of it.
- **Packets** of 5, 10 or 20 consecutive sheets, with an optional cover page, instructions and a practice log.
- **Share card:** choose what goes in the footer (logo, code, details, 50 mm ruler) and add an optional name and date line.
- **One-tap share:** print, save to Files, AirDrop or email straight from the share sheet.
- **Present mode:** full-screen charts for a tablet or a mirrored TV. Swipe for the next one.
- **Recent charts and quick start** on the Home tab.

## Privacy

Everything runs on the device. There's no account, no network access, no analytics and no tracking.

- Patient names and dates are typed per print, never saved, and never put in a chart code.
- Exported PDFs are deleted as soon as the share sheet closes.
- The App Store privacy label is **Data Not Collected**.

Read the full [privacy policy](https://mr3entley.github.io/VTS/privacy.html) or visit [support](https://mr3entley.github.io/VTS/support.html).

## Printing for accurate size

1. Print at **100% scale** (not "fit to page"), one page per sheet.
2. Measure the **50 mm bar** in the footer with a ruler. If it's 50 mm, every character on the sheet is true to size.

## Getting started

### Requirements

| | |
| --- | --- |
| Xcode | 27 or later |
| Deployment target | iOS 17.6, iPhone and iPad |
| Language | Swift 5 mode, SwiftUI, Observation, Swift Testing |
| Dependencies | None. Apple frameworks only. |

### Build and run

```bash
git clone https://github.com/<your-account>/<this-repo>.git
cd <this-repo>
open VisionTherapySuite.xcodeproj
```

Pick a simulator or device, then press **⌘R**. Run the tests with **⌘U**.

## Project layout

```
VisionTherapySuite/
├── App/          Entry point, launch screen, tab bar
├── Brand/        Design tokens and styled components
├── Core/         Chart codes, seeded RNG, history, units, storage
├── Export/       Share settings, share codes, PDF export flow
├── Home/         Home tab, recent charts, About
├── Metronome/    Audio engine, sounds and controls
├── PDF/          Page geometry, headers, footers, cover page, rendering
├── Present/      Full-screen Present mode
├── Shared/       Generator scaffold, settings cards, preview, Share card
├── SlapTap/      Slap Tap generator, model, glyphs, sheet, screen
└── VisualChart/  Visual Chart generator, model, layout, near cards, screen
VisionTherapySuiteTests/   Swift Testing suites
```

Small files, one job each. The generators and code parsers are pure Swift, so they're quick to test.

For how everything works under the hood (chart codes, true-size layout, the PDF pipeline, the metronome scheduler and how to add a new generator), see **[DEVELOPMENT.md](DEVELOPMENT.md)**.

## How chart codes work

A chart code describes the sheet. It never describes the patient.

```
V3L2B12.5OG-1042-P10C
││││││   ││ │    └─ share settings: a 10-sheet packet (P10) with a cover (C)
││││││   ││ └─ chart number: seeds the characters
││││││   │└─ G: grid lines on
││││││   └─ O: border on
│││││└─ character height: 12.5 mm
││││└─ weight: B for bold
│││└─ charts per page: 2
││└─ content: L for letters
│└─ grid: 3×3
└─ V: Visual Chart
```

Characters come from a seeded random generator (SplitMix64 with its own shuffle), so the same number always draws the same chart on every device and every version. Settings that are left at their defaults are left out of the code, which keeps codes short.

## Disclaimer

Vision Therapy Suite makes printable worksheets for vision therapy done under the direction of an eye care professional. It doesn't diagnose, measure or treat anything, and it's no substitute for professional advice.

## License

© 2026 Jeffrey Bentley. All rights reserved.
