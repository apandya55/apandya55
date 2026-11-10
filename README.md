# Arnav Pandya

Hey, I'm Arnav. I'm 16 and a student at the [North Carolina School of Science and Mathematics](https://www.ncssm.edu/) (NCSSM) in Durham. I spend most of my time building software and hardware — usually full-stack web tools, custom PCBs, embedded firmware, or GIS data pipelines. I also write for NCSSM's *Frontier* journal, interviewing CEOs and tech leaders around North Carolina.

[arnavpandya.com](https://arnavpandya.com) · [GitHub](https://github.com/apandya55) · [LinkedIn](https://linkedin.com/in/arnavpandya) · [arnav@arnavpandya.com](mailto:arnav@arnavpandya.com)

---

## What I've Been Building

### [Upwind](https://github.com/apandya55/Upwind) — Air Quality Atlas & Dispersion Engine

Most public air-quality apps show either a real-time dial or a vague county-wide average that pretends every neighborhood breathes the same air. The raw historical records exist in federal EPA archives, but they're locked in multi-gigabyte spreadsheets that crash standard spreadsheets.

I built Upwind to give people a place-by-place view of 40 years of fine particulate (PM₂.₅) pollution across the contiguous U.S. It models 31,000+ Census towns with empirical ±4.12 µg/m³ confidence bounds, indexes 894 physical EPA monitoring stations, and maps 76,400+ industrial emission sites from the National Emissions Inventory. If a town is too far from an active monitor, the system flags it with a boundary warning instead of guessing.

Live app at [upwind-explorer.vercel.app](https://upwind-explorer.vercel.app) — public API at [upwind-national-api.vercel.app](https://upwind-national-api.vercel.app/api/health)

<details>
<summary>Architecture & technical details</summary>
<br>

- **Backend:** Python 3.12 and FastAPI serving spatial queries through pre-indexed bounding trees in under 100ms.
- **Frontend:** React 19 with client-side geographic caching so you can scrub across 40 years of data without UI lag.
- **Pipeline:** Parses raw multi-decade AQS text files, NEI facility tonnages, and Census Gazetteer coordinates into a structured geographic index. Deployed on Vercel.

</details>

---

### [HIL Debug Workbench](https://github.com/apandya55/hil_debug_workbench) — Automated Embedded Crash Recovery

If you work with microcontrollers, you know the drill: your firmware crashes on bare metal, and instead of a clean stack trace, you get a raw hex register dump over UART (`Guru Meditation Error: Core 0 panic'ed`).

Resolving that by hand means finding your cross-compiler toolchain, pulling the ELF binary out of `.pio/build/`, running `addr2line` on every frame address, reading the source, writing a fix, rebuilding, and flashing over USB. After doing that dozens of times on late-night debugging sessions, I automated the whole cycle.

The workbench monitors serial output over USB, catches the panic, maps hex addresses back to C++ source lines via `addr2line`, synthesizes a patch, and triggers PlatformIO to re-flash the board. Works with both ESP32 (Xtensa) and RP2040 (ARM) toolchains.

<details>
<summary>How the crash-to-patch loop works</summary>
<br>

```
Physical MCU ──UART panic──▶ Serial Monitor ──regex match──▶ addr2line
     ▲                                                          │
     │                                                          ▼
PlatformIO ◀──auto-flash──── Patch Generator ◀──── Source Mapping
```

1. Listens on USB serial for panic signatures, unhandled memory faults, and register dumps.
2. Resolves addresses against `firmware.elf` using the matching GNU toolchain.
3. Generates a contextual diagnostic patch from the culprit lines.
4. Triggers PlatformIO to rebuild and re-flash over USB without touching the terminal.

</details>

---

### [Muybridge CAD](https://github.com/apandya55/muybridge-cad) — 12-Angle Visual CAD Verification

Named after Eadweard Muybridge's 1878 experiment with 12 synchronized cameras to prove whether a running horse's hooves leave the ground.

Most programmatic CAD generators only check if a 3D mesh compiles and is watertight. That misses real fabrication bugs — like 0.2mm thin walls that collapse on a 3D printer, undrilled blind holes, or floating geometry on the backside that looks fine from a single perspective.

Muybridge renders 12 synchronized camera angles (two elevation tiers, 30° azimuth intervals) plus planar cross-sections into an inspection contact sheet. It runs inward normal ray-casting to measure true minimum wall thickness against slicer limits, then passes the contact sheet to a vision model to critique and patch the code before you waste filament.

Built with Python, build123d, OpenSCAD, and Next.js 15.

---

### [FlashWAF](https://github.com/apandya55/flash-waf-sim) — NAND Flash Translation Layer Simulator

NAND flash memory has a catch: you can't overwrite a page in place. You have to erase an entire block before writing to it again. That means the SSD controller has to constantly move valid data around during garbage collection, causing Write Amplification (the drive writes far more physical data than your OS asked it to).

I wrote FlashWAF to model that behavior in Python. It simulates page-mapped FTL allocation, out-of-place writes, greedy garbage collection, and write amplification under uniform, hot/cold (80/20, 90/10), and Zipfian workloads. It also includes an injected crash simulator to measure data lost from volatile staging buffers.

36 unit tests passing. Published with a citable [Zenodo DOI](https://doi.org/10.5281/zenodo.23655212).

---

### [PomodoroPebble](https://github.com/apandya55/PomodoroPebble) — Desk Timer with Custom PCB

Using timer apps on my phone kept backfiring because checking the remaining time meant looking at notifications. So I built a standalone physical timer for my desk.

It runs on a Seeed XIAO RP2040, two tactile MX mechanical switches with DSA keycaps, a 128×32 OLED screen, and four SK6812 addressable RGB LEDs on a custom 2-layer PCB I routed in KiCad. The enclosure is 3D printed with embedded neodymium magnets so the halves snap together without visible screws.

The firmware is written in C++ with a non-blocking state machine and hardware debouncing under 5ms, and it puts the display to sleep between sessions to avoid burn-in.

Build log and CAD models at [arnavpandya.com/projects/pomodoro-pebble](https://arnavpandya.com/projects/pomodoro-pebble).

---

## Other Things

- **Desk Buddy** — ESP32 robotics companion with a SPI TFT display and servos.
- **Frontier Website** — Next.js and Tailwind web presence for NCSSM's research journal.

Everything else lives at [arnavpandya.com/projects](https://arnavpandya.com/projects).

---

## Tech I Work With

```
Languages      TypeScript · Python · C++ · SQL
Frontend       React 19 · Next.js 15 · Tailwind CSS · Leaflet · Vite
Backend        FastAPI · Node.js · Express · NumPy · REST APIs
Hardware       RP2040 · ESP32 · PlatformIO · I2C / SPI / UART
Fabrication    KiCad 8 (PCB) · Fusion 360 (CAD) · CoreXY 3D Printing (PETG/PLA)
Tooling        Docker · Pytest · GDB · addr2line · GeoJSON
```

---

## About Me

I got into hardware in 8th grade when I built my first budget 3D printer. Dealing with warped beds, clogged hotends, and loose belts taught me early on that debugging physical things is a different game than software — physical problems don't come with StackOverflow threads, and you have to test things methodically.

Along with programming, I'm really interested in finance, capital markets, and how businesses scale. As a journalist for NCSSM's *Frontier*, I interview founders, CEOs, and research leads across North Carolina about how they make strategic decisions and allocate capital.

When I'm not in front of a computer, I play competitive badminton, do Model UN, or assemble 1,000 to 3,000 piece jigsaw puzzles when I need to step away from screens.
