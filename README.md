# Arnav Pandya

I'm a 16-year-old software engineer and hardware builder at the [North Carolina School of Science and Mathematics](https://www.ncssm.edu/) (NCSSM) in Durham. I spend most of my time building full-stack web tools, routing custom PCBs, writing embedded firmware, and working with spatial data. I also write for NCSSM's *Frontier* journal, where I interview CEOs and research leaders across North Carolina.

[arnavpandya.com](https://arnavpandya.com) · [GitHub](https://github.com/apandya55) · [LinkedIn](https://linkedin.com/in/arnavpandya) · [arnav@arnavpandya.com](mailto:arnav@arnavpandya.com)

---

## Projects

### [Upwind](https://github.com/apandya55/Upwind) — National Air Quality Atlas
Most air-quality apps show a real-time dial or a single county average that ignores neighborhood differences. The raw historical data sits in federal EPA archives across multi-gigabyte spreadsheets that crash standard tools.

I built Upwind to make 40 years of historical fine particulate (PM₂.₅) pollution easy to explore town by town:
- **31,000+** U.S. Census places modeled with empirical ±4.12 µg/m³ 90% confidence bounds.
- **894** physical EPA monitoring stations and **76,400+** industrial emission facilities mapped nationwide.
- Built with Python 3.12, FastAPI, and React 19, serving spatial bounding-tree queries in under 100ms.
- Places too far from an active reference monitor are flagged with a data boundary warning rather than an unverified estimate.

*Live site:* [upwind-explorer.vercel.app](https://upwind-explorer.vercel.app) · *API:* [upwind-national-api.vercel.app](https://upwind-national-api.vercel.app/api/health)

---

### [HIL Debug Workbench](https://github.com/apandya55/hil_debug_workbench) — Automated Embedded Diagnostics
When firmware crashes on bare metal, microcontrollers spit out cryptic hex register dumps over UART instead of a stack trace. Fixing it usually means finding cross-compiler binaries, locating the build ELF file, running `addr2line` on each address by hand, and repeating the cycle dozens of times.

HIL Debug Workbench automates that entire loop over USB:
- Monitors serial output for kernel panics, register dumps, and memory faults.
- Demangles and maps hex addresses back to exact C++ source lines via `addr2line`.
- Synthesizes a fix patch and re-flashes the board automatically through PlatformIO.
- Supports both ESP32 (Xtensa) and RP2040 (ARM) toolchains.

---

### [Muybridge CAD](https://github.com/apandya55/muybridge-cad) — Multi-Angle Geometric CAD Verification
Named after Eadweard Muybridge's 1878 multi-camera study that captured whether a galloping horse ever becomes fully airborne.

Most programmatic CAD code checks only whether a 3D mesh compiles and is watertight. That misses real manufacturing defects like paper-thin walls, blind holes, or floating geometry on the backside. Muybridge renders a 12-camera inspection plate (two elevation tiers, 30° azimuth intervals) plus cross-sections, shoots hundreds of inward normal rays to measure true minimum wall thickness, and uses a vision model to critique and patch geometry before 3D printing. Built with Python, build123d, OpenSCAD, and Next.js 15.

---

### [FlashWAF](https://github.com/apandya55/flash-waf-sim) — NAND Flash Translation Layer Simulator
NAND flash memory cannot overwrite pages in place; it must erase an entire block before reprogramming. This constraint forces SSD controllers to constantly relocate valid data during garbage collection, causing Write Amplification (the drive writes more physical data than requested).

FlashWAF is an open-source Python simulator that models page-mapped FTL allocation, out-of-place writes, greedy garbage collection, and write amplification under uniform, hot/cold (80/20, 90/10), and Zipfian workloads. Includes crash injection testing to evaluate volatile buffer loss.

Published with a citable [Zenodo DOI: 10.5281/zenodo.23655212](https://doi.org/10.5281/zenodo.23655212). 36 unit tests passing.

---

### [PomodoroPebble](https://github.com/apandya55/PomodoroPebble) — Desk Timer with Custom PCB
Using phone timers always came with the urge to check notifications, so I built a physical desk timer from scratch.

- Runs on a Seeed XIAO RP2040 microcontroller.
- Two clicky MX mechanical keyboard switches with DSA keycaps and a 128x32 OLED display.
- 4x SK6812 addressable RGB LEDs on a custom 2-layer PCB designed in KiCad.
- 3D-printed enclosure with recessed neodymium magnets that snap together without visible screws.
- Non-blocking C++ firmware with hardware debouncing under 5ms and auto-sleep display protection.

Build log & CAD renders: [arnavpandya.com/projects/pomodoro-pebble](https://arnavpandya.com/projects/pomodoro-pebble)

---

## Tech Stack

- **Languages:** TypeScript, Python, C++, SQL
- **Frontend & Web:** React 19, Next.js 15, Tailwind CSS, Leaflet, Vite
- **Backend & Data:** FastAPI, Node.js, Express, NumPy, REST APIs, GeoJSON
- **Embedded & Hardware:** Seeed XIAO RP2040, ESP32, PlatformIO, I2C / SPI / UART
- **Design & Making:** KiCad 8 (PCB design), Fusion 360 (CAD), CoreXY 3D Printing (PETG/PLA)
- **Tools:** Docker, Pytest, GDB, GNU toolchains (`addr2line`)

---

## About Me

I got into building physical things in 8th grade when I built my first budget 3D printer. Fixing warped beds, clogged hotends, and tuning stepper drivers taught me how to methodically debug hardware when there are no error messages or StackOverflow answers.

Outside of software and electronics, I'm interested in finance and capital markets. For NCSSM's *Frontier* journal, I interview founders, CEOs, and research executives across North Carolina about capital allocation and scaling engineering teams.

When I step away from computers, I play competitive badminton, do Model UN conferences, and assemble 1,000 to 3,000 piece jigsaw puzzles.
