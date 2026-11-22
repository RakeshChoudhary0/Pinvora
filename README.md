# Pinvora

**Every pin. Every board.**

![License: Apache-2.0](https://img.shields.io/badge/license-Apache--2.0-blue) ![Status: early development](https://img.shields.io/badge/status-early%20development-orange)

A free, browser-based IoT and PCB studio. Wire it, code it, simulate it, and send it to a PCB factory, all in one browser tab.

> **Status: early development (Phase 1).** The wiring canvas and custom part builder are the first milestone. Features marked *Planned* are on the roadmap but not built yet. Expect breaking changes.

---

## Table of Contents

- [Why this project exists](#why-this-project-exists)
- [Who it is for](#who-it-is-for)
- [Features](#features)
- [Supported hardware and simulation targets](#supported-hardware-and-simulation-targets)
- [Screenshots](#screenshots)
- [Tech stack](#tech-stack)
- [Getting started](#getting-started)
- [Project structure](#project-structure)
- [How custom parts work](#how-custom-parts-work)
- [Validation rules](#validation-rules)
- [Roadmap](#roadmap)
- [Known limitations](#known-limitations)
- [Project Documentation (PRD and SRD)](#project-documentation)
- [Contributing](#contributing)
- [Community parts guidelines](#community-parts-guidelines)
- [Security](#security)
- [Licensing and attribution](#licensing-and-attribution)
- [FAQ](#faq)
- [Acknowledgements](#acknowledgements)

---

## Why this project exists

Learning and prototyping IoT is expensive. Boards, GPS and LoRa modules, 4G modems, and BMS hardware cost money, and one wiring mistake (5V into a 3.3V pin, a missing common ground) can destroy a part. Existing tools are also fragmented: one for simulation, another for schematics, another for PCB layout.

Pinvora aims to remove the hardware barrier and join the whole pipeline in one place:

**Wire → Code → Simulate → Design PCB → Export Gerber**

## Who it is for

| User | What they get |
|---|---|
| Students | A free, no-hardware way to build and test college and hackathon projects |
| Makers and hobbyists | Fast prototyping and a path to a real PCB |
| Educators | A shared environment for labs and assignments (Planned) |
| Startups and freelancers | Quick validation and BOM/Gerber export before ordering hardware |
| Module and board makers | A way to publish parts with pinouts and simulation models (Planned) |

## Features

Legend: ✅ working · 🚧 in progress · 📋 planned

### Wiring canvas and IoT library

- 🚧 Drag-and-drop canvas with multiple boards and parts in one project
- 🚧 Typed pins: 3V3, 5V, GND, GPIO, ADC, PWM, I2C, UART, SPI, CAN
- 🚧 Live electrical guardrails: 5V-to-3.3V warnings, missing common GND, TX/RX swaps, shorted outputs
- 🚧 Starter library: Arduino Uno, ESP32 DevKit, MPU6050 or DHT22, LED, relay module
- 🚧 Save and load projects as JSON
- 📋 Expanded library: Nano, Mega, ESP32-C3/S3, Raspberry Pi Pico, STM32, GPS, LoRa SX1278, CAN transceivers, RS485/Modbus, 4G modems, motor drivers, OLED displays, BMS modules
- 📋 Multi-node systems (for example several sensor nodes and a gateway)

### Custom part and pinout builder

- 🚧 Define any part: pin names, functions, voltage levels
- 🚧 Layout presets (single row, dual row, grid) with configurable pitch (default 2.54 mm)
- 🚧 Through-hole pads (drill and copper ring) and SMD pads
- 🚧 One definition generates both the wiring block and the PCB footprint
- 📋 Universal MCU generator
- 📋 Community parts library with versions, licenses, and moderation

### Code editor and browser simulation

- 📋 Monaco editor for Arduino C/C++ and MicroPython beside the circuit
- 📋 Run Arduino Uno firmware in the browser (avr8js)
- 📋 Run Raspberry Pi Pico firmware (rp2040js) and MicroPython (WebAssembly)
- 📋 Serial monitor and environment sliders (temperature, GPS, IMU tilt, battery voltage)
- 📋 IoT dashboard widgets: gauges, charts, maps, toggles
- 📋 Cloud compile service for Arduino C/C++

### PCB layout and export

- 📋 Netlist carries over from the wiring canvas to a 2D PCB editor
- 📋 Board outline, footprint placement, manual routing on two layers
- 📋 Design rule checks (clearance, overlap, unconnected nets)
- 📋 Export Gerber, drill files, and BOM as a zip
- 📋 Autorouting by integrating an existing router
- 📋 2D and 3D board preview

### Student ecosystem

- 📋 Shareable project links
- 📋 Starter templates: smart irrigation, line-following robot, drone telemetry, EV BMS
- 📋 Classroom mode with assignments and submissions
- 📋 Virtual MQTT/WebSocket endpoints for app testing

## Supported hardware and simulation targets

Not every MCU can be executed in a browser today, so support is split into two levels.

| Target | Wiring and pin checks | PCB footprint | Firmware execution in browser |
|---|---|---|---|
| Arduino Uno / Nano (ATmega328P) | Yes | Yes | Planned via avr8js |
| Arduino Mega (ATmega2560) | Yes | Yes | Planned, where supported |
| Raspberry Pi Pico (RP2040) | Yes | Yes | Planned via rp2040js |
| MicroPython | n/a | n/a | Planned via WebAssembly |
| ESP32 / ESP32-C3 / ESP32-S3 | Yes | Yes | **Not supported yet** |
| STM32 | Yes | Yes | **Not supported yet** |
| Custom MCU (Universal MCU generator) | Planned | Planned | No |

"Every MCU in the world" means wiring and footprint support through the custom part builder. It does not mean firmware emulation for every chip.

Sensor and module behavior in simulation is approximated for learning and logic testing. It is not an electrically accurate model.

## Screenshots

*Add screenshots or a short GIF here once the canvas is running.*

```
docs/images/canvas.png
docs/images/custom-part-builder.png
```

## Tech stack

| Area | Technology |
|---|---|
| Frontend | React, TypeScript, Vite, Tailwind CSS |
| State | Zustand |
| Wiring canvas | React Flow (`@xyflow/react`) |
| Data validation | Zod |
| Code editor | Monaco Editor (`@monaco-editor/react`) |
| AVR simulation | avr8js |
| RP2040 simulation | rp2040js |
| MicroPython | MicroPython WebAssembly port |
| PCB tooling | Custom editor; tscircuit and Freerouting under evaluation |
| Compile service | Arduino CLI in sandboxed containers (Node.js or FastAPI) |
| Storage | PostgreSQL and S3-compatible object storage |

## Getting started

### Prerequisites

- Node.js 20 or newer (LTS recommended)
- npm (comes with Node.js)
- A current version of Chrome, Edge, Firefox, or Safari

### Install and run

```bash
# 1. Clone the repository
git clone https://github.com/RakeshChoudhary0/pinvora.git
cd pinvora

# 2. Install dependencies
npm install

# 3. Start the dev server
npm run dev
```

Open `http://localhost:5173` in your browser.

### Other scripts

```bash
npm run build      # Production build
npm run preview    # Preview the production build
npm run lint       # Lint the code
npm run test       # Run unit tests
npm run typecheck  # TypeScript type check
```

Adjust these to match the scripts in your `package.json`.

### Environment variables

Phase 1 runs fully in the browser and needs no environment variables. Later phases will use a `.env` file:

```env
VITE_API_URL=http://localhost:8080
```

Never commit `.env` files or secrets.

## Project structure

*Planned layout; update as the code evolves.*

```
pinvora/
├─ src/
│  ├─ canvas/          # React Flow canvas, PartNode, wire handling
│  ├─ parts/           # Part definitions, library, custom part builder
│  ├─ validation/      # Electrical rules (one pure function per rule)
│  ├─ simulation/      # Web Workers, avr8js/rp2040js wrappers, peripheral models
│  ├─ editor/          # Monaco editor integration
│  ├─ pcb/             # PCB editor, DRC, Gerber and BOM export
│  ├─ dashboard/       # Gauges, charts, serial monitor
│  ├─ store/           # Zustand stores
│  └─ schemas/         # Zod schemas (PartDefinition, Project)
├─ server/             # Compile service and API (later phases)
├─ public/             # Static assets, sample hex files
├─ docs/               # PRD, SRD, architecture notes, images
└─ tests/
```

## How custom parts work

Every part, built-in or user-made, is described by one `PartDefinition`. That single definition drives the wiring block, validation, simulation metadata, and the PCB footprint, so a custom part works everywhere without redoing it.

```ts
interface PartPin {
  id: string;
  name: string;
  types: PinType[];            // for example ['GPIO', 'PWM', 'I2C_SDA']
  voltage?: number;            // logic level in volts
  pad: {
    x: number; y: number;      // millimeters
    shape: 'circle' | 'rect' | 'oval';
    kind: 'through-hole' | 'smd';
    size: number;              // copper diameter, mm
    drill?: number;            // mm, through-hole only
  };
}

interface PartDefinition {
  id: string;
  version: string;
  name: string;
  category: 'mcu' | 'sensor' | 'actuator' | 'power' | 'comms';
  license: string;
  pins: PartPin[];
  body: { width: number; height: number };
  sim?: { engine: 'avr8js' | 'rp2040js' | 'model'; ref: string };
}
```

Parts are validated with Zod before they are saved or uploaded.

## Validation rules

| Rule | Severity |
|---|---|
| 5V output connected to a 3.3V-only input | Error |
| No common GND between connected parts | Error |
| Two outputs driving the same net | Error |
| UART TX connected to TX, or RX to RX | Warning |
| Power pin left unconnected | Warning |
| Duplicate I2C address on one bus | Warning |
| I2C bus without pull-ups | Info |

Each rule is a small pure function with its own tests, so adding a rule means adding one file.

## Roadmap

| Phase | Focus | Status |
|---|---|---|
| 1 | Wiring canvas, validation, starter parts, JSON save/load, custom part builder | 🚧 In progress |
| 2 | Monaco editor, avr8js, serial monitor, sliders, MicroPython, Pico, dashboard, compile service | 📋 Planned |
| 3 | PCB editor, DRC, Gerber and BOM export | 📋 Planned |
| 4 | Community library, classroom mode, templates, MQTT endpoints | 📋 Planned |

Phases may be reordered based on user feedback. Full requirements are in [Project Documentation](#project-documentation) below.

## Known limitations

- ESP32 and STM32 firmware cannot be executed in the browser yet.
- Sensor models approximate behavior; they do not model analog electrical characteristics.
- LoRa, ESP-NOW, and 4G multi-node simulation is a late-phase goal.
- Exported PCB files must be checked by the user before manufacturing. Always review the design in a Gerber viewer and the manufacturer's upload checker.
- Cloud compile will have rate limits to control cost.

## Project Documentation

This section holds the full product and system requirements. Each part is collapsible; click a heading to expand it.

- **PRD (Product Requirements Document):** what we are building, for whom, and how it earns money.
- **SRD / SRS (System Requirements Document / Software Requirements Specification):** how it is built, with technical requirements.

*Figures marked "assumption" are planning estimates to validate, not facts.*

---

# Part A: Product Requirements Document (PRD)

<details>
<summary><strong>A1. Product overview and problem statement</strong></summary>

**What it is:** A free-to-start, browser-based engineering studio where users wire IoT hardware, create custom parts and footprints, write and run microcontroller code, simulate sensors, and export manufacturing-ready PCB files (Gerber, drill, BOM) without buying lab hardware.

**Pitch:** Wire it, code it, simulate it, and send it to a PCB factory, all in one browser tab.

| Problem | Who feels it | Impact |
|---|---|---|
| Hardware is costly (MCU boards, GPS, LoRa, 4G, BMS) | Students, hobbyists, colleges | Projects delayed or never built |
| Wiring mistakes (5V into 3.3V, missing GND, swapped TX/RX) destroy parts | Beginners | Wasted money, lost confidence |
| Fragmented tools (simulator, schematic, PCB in separate apps) | Makers, educators | Rework, data lost between tools |
| Missing parts in libraries | Everyone | Users cannot model their real hardware |
| Labs cannot give every student a kit | Colleges, bootcamps | Poor hands-on learning |

</details>

<details>
<summary><strong>A2. Vision, goals, and non-goals</strong></summary>

**Vision:** The default place where a student or maker goes from idea to a real, orderable IoT board without owning hardware.

**Goals**

1. A beginner builds and validates a multi-board IoT circuit in under 10 minutes.
2. A custom part is created once and works in wiring, simulation, and PCB.
3. Real firmware runs in the browser for supported targets (AVR, RP2040, MicroPython).
4. Exported PCB files are accepted by a factory on the first upload.
5. A sustainable, low-cost business with a free tier that drives growth.

**Non-goals (v1)**

- Cycle-accurate emulation of ESP32, ESP32-C3/S3, or STM32 (wiring and PCB support only at first)
- Analog/SPICE-level circuit simulation
- High-speed, RF, or multi-layer (4+) PCB design
- Native mobile apps
- Guaranteeing electrical certification or production-readiness of exported boards

</details>

<details>
<summary><strong>A3. Target users and personas</strong></summary>

| Persona | Description | Main need | Willingness to pay |
|---|---|---|---|
| Student (primary) | Engineering and diploma students doing college or hackathon projects | Free, no-hardware way to build and test | Low |
| Maker / hobbyist | Home automation, robots, drones | Fast prototyping, PCB export | Medium |
| Educator / lab instructor | Teaches embedded systems and IoT | Classroom management, assignments, grading | High (institution budget) |
| Startup / freelance developer | Prototypes before ordering hardware | Validation, shareable demos, BOM | High |
| Hardware vendor / module maker | Sells sensors, boards, modules | Library presence, simulation models | High (marketing budget) |

**Initial market focus:** Engineering students and makers in India and similar cost-sensitive markets, then global expansion (assumption).

</details>

<details>
<summary><strong>A4. Market and competition</strong></summary>

| Tool | Strength | Gap this project fills |
|---|---|---|
| Wokwi | Strong browser simulation | Weak PCB pipeline and custom-part-to-footprint flow |
| Tinkercad Circuits | Beginner friendly | Limited MCUs, no real PCB export |
| EasyEDA / Flux | PCB design | No firmware simulation |
| KiCad / Fritzing | Powerful desktop tools | Install required, no browser code execution |
| EWsim.io (EWskills) | Browser mixed-signal simulator that runs microcontroller firmware, 200+ components | Tied to its own learning platform; no custom-part-to-PCB pipeline (verify before launch) |
| iCircuit | Polished mobile simulator with Pico MicroPython support | Mobile app, paid, no Gerber/PCB export (verify before launch) |

**Differentiator:** the integrated pipeline (wire, code, simulate, PCB) with one custom-part definition that drives every stage, plus live electrical guardrails for beginners. Verify competitor features before launch, as they change.

</details>

<details>
<summary><strong>A5. Features and priorities</strong></summary>

Priority: **P0** = MVP, **P1** = after MVP, **P2** = later.

**Module A: Wiring canvas and heavy IoT library**

| ID | Feature | Priority |
|---|---|---|
| A1 | Drag-and-drop canvas with multiple boards and parts | P0 |
| A2 | Typed pins (3V3, 5V, GND, GPIO, ADC, PWM, I2C, UART, SPI, CAN) | P0 |
| A3 | Live validation: voltage mismatch, missing common GND, TX/RX swap, shorted outputs | P0 |
| A4 | Starter library (Uno, ESP32 DevKit, MPU6050/DHT22, LED, relay) | P0 |
| A5 | JSON project save/load | P0 |
| A6 | Expanded library (Nano, Mega, ESP32-C3/S3, Pico, STM32, GPS, LoRa, CAN, RS485, 4G, motor drivers, OLED, BMS) | P1 |
| A7 | Multi-node systems linked by LoRa or ESP-NOW | P2 |

**Module B: Custom part and pinout builder**

| ID | Feature | Priority |
|---|---|---|
| B1 | Create custom part: pin names, types, voltage, functions | P0 |
| B2 | Layout presets (single row, dual row, grid) with pitch (default 2.54 mm) | P0 |
| B3 | Through-hole pads (drill and copper ring) and SMD pads | P0 |
| B4 | One definition generates the wiring block and the PCB footprint | P0 |
| B5 | Universal MCU generator | P1 |
| B6 | Community library: publish, version, report, moderate | P1 |

**Module C: Code editor and browser simulation**

| ID | Feature | Priority |
|---|---|---|
| C1 | Monaco editor with Arduino C/C++ and MicroPython | P1 |
| C2 | Run precompiled hex on Uno via avr8js (Web Worker) | P1 |
| C3 | Serial monitor | P1 |
| C4 | Environment sliders (temperature, GPS, IMU tilt, battery voltage) | P1 |
| C5 | Raspberry Pi Pico via rp2040js; MicroPython in WebAssembly | P1 |
| C6 | IoT dashboard widgets (gauges, charts, map, toggles) | P1 |
| C7 | Cloud compile for Arduino C/C++ | P1 |
| C8 | Virtual MQTT/WebSocket endpoints | P2 |
| C9 | ESP32 / STM32 execution | P2 (research; may depend on third-party emulators) |

**Module D: PCB layout and manufacturing export**

| ID | Feature | Priority |
|---|---|---|
| D1 | Netlist carries over from wiring canvas to PCB editor | P1 |
| D2 | Board outline, footprint placement, manual routing (2-layer) | P1 |
| D3 | Design Rule Check (clearance, overlap, unconnected nets) | P1 |
| D4 | Gerber, drill, and BOM export as .zip | P1 |
| D5 | Autorouting (integrate an existing router) | P2 |
| D6 | 2D/3D board preview | P2 |

**Module E: Student ecosystem**

| ID | Feature | Priority |
|---|---|---|
| E1 | Shareable project links | P1 |
| E2 | Starter templates (smart irrigation, line-following robot, drone telemetry, EV BMS) | P1 |
| E3 | Classroom mode: assignments, submissions, teacher view | P1 |
| E4 | Order-PCB button with fab partner handoff | P1 |

**Key user stories**

- As a student, I want a warning when I connect 5V to a 3.3V pin so I do not destroy my part.
- As a maker, I want to create a custom sensor once so it appears in wiring and the PCB without redoing work.
- As a student, I want to run my Arduino code and see an LED blink so I can test without hardware.
- As an educator, I want to see each student's project and results so I can grade remotely.
- As a startup developer, I want a BOM and Gerber export so I can order a prototype board.

</details>

<details>
<summary><strong>A6. Success metrics</strong></summary>

| Metric | Target at 6 months after Phase 1 (assumption) |
|---|---|
| Registered users | 5,000 |
| Weekly active users | 800 |
| Projects created per active user per month | 3 |
| Share of projects using a custom part | 20% |
| Phase 2 users who run a simulation at least once | 50% |
| Free-to-paid conversion | 2% to 4% |
| Gerber exports that pass a factory's upload check | above 90% |
| Day-30 retention | 20% |

</details>

<details>
<summary><strong>A7. Business model: how the project earns money</strong></summary>

IoT is an expensive field, but this product is cheap to run because simulation executes in the user's browser. The main server costs are compile jobs and storage. A generous free tier is affordable, and revenue comes from several streams.

**Revenue streams**

| # | Stream | How it works | Timing |
|---|---|---|---|
| 1 | Freemium subscriptions | Free tier for learning; Pro tier for heavier use | Phase 2 onward |
| 2 | Institution / classroom licenses | Colleges and bootcamps pay per student or per lab | Phase 4 |
| 3 | PCB fabrication referrals | "Order this PCB" hands off to partner fabs (for example JLCPCB, PCBWay) for a referral commission, if offered | Phase 3 |
| 4 | Component / BOM affiliate links | BOM lines link to distributors (LCSC, Mouser, DigiKey, local Indian distributors) | Phase 3 |
| 5 | Hardware vendor partnerships | Module makers pay to feature verified parts with simulation models | Phase 4 |
| 6 | Compile credits | Extra cloud compile and priority queue | Phase 2 |
| 7 | Courses, workshops, hackathons | Paid guided courses, certification, sponsored hackathons | Anytime |
| 8 | API / white-label | Embed the simulator or part builder in other education sites | Later |

**Pricing plan (assumption: validate with real users)**

| Plan | Price | Includes |
|---|---|---|
| Free | $0 | Wiring, validation, custom parts, AVR/RP2040/MicroPython simulation, limited daily cloud compiles, 5 cloud projects, community library |
| Pro | about $6 to $9/month (India about ₹199 to ₹399) | Unlimited projects, more compiles, private projects, PCB export without watermark, larger boards, priority compile queue |
| Student Pro | about 50% off with verification | Same as Pro |
| Classroom / Institution | about $2 to $4 per student per year, or flat lab license | Teacher dashboard, assignments, auto-checks, bulk accounts, SSO |
| Team / Startup | about $15 to $25 per seat per month | Shared libraries, version history, private part libraries |

**Cost structure:** static frontend hosting (free or cheap); compile servers (main variable cost, reduced by caching, rate limits, and queues); database and object storage; domain, email, monitoring; moderation and support time; payment gateway fees.

**Illustrative unit economics (assumption):** If 10,000 users reach the platform and 3% convert to Pro at an average of $5/month, monthly recurring revenue is about $1,500. Affiliate and institution income add to this, while server cost stays modest because simulation is client-side. Treat this as a hypothesis, not a forecast.

**Monetization principles**

- Keep learning free: the free tier must be good enough for a student project.
- Charge for convenience, scale, and professional use, not for core learning.
- Never make a free user pay to avoid a mistake the tool should have warned about.
- Be honest about export quality: do not promise a factory-ready board without DRC and a verified fab check.

</details>

<details>
<summary><strong>A8. Go-to-market strategy</strong></summary>

1. Launch Phase 1 early on Product Hunt, Reddit (embedded and maker communities), Hacker News, and student groups.
2. Publish short YouTube and Instagram builds ("build a smart irrigation system without buying hardware").
3. Pilot with a few engineering colleges, offering free classroom access in exchange for feedback and case studies.
4. Supply the platform as the official tool at hackathons.
5. Grow the community parts library so every new user adds value for others.
6. Invite module makers to publish official, simulated parts.

</details>

<details>
<summary><strong>A9. Risks and mitigations</strong></summary>

| Risk | Likelihood | Mitigation |
|---|---|---|
| ESP32/STM32 not simulatable in browser | High | Ship wiring and PCB support first; run AVR/RP2040/MicroPython; revisit later |
| Scope too large for one developer | High | Thin vertical slices, strict phase gates, reuse open-source tools |
| Wrong footprints cause wasted PCB orders | Medium | DRC, verification badges, moderation, clear disclaimers |
| Compile server abuse or cost | Medium | Sandboxing, rate limits, caching, quotas |
| Open-source license conflicts (CC-BY-SA, GPL) | Medium | License audit per asset; store attribution; legal review before commercial launch |
| Strong competitors | Medium | Focus on integrated pipeline and student price point |
| Low willingness to pay among students | High | Institution licenses, affiliates, vendor revenue |

</details>

<details>
<summary><strong>A10. Assumptions and open questions</strong></summary>

- Final product name, domain, and branding are undecided.
- Which fab partners offer affiliate or API programs must be confirmed.
- Whether Fritzing and KiCad assets can be bundled depends on each license; to be audited.
- Pricing and conversion rates are untested; run willingness-to-pay interviews during Phase 1.
- Whether ESP32 simulation can be offered via a third-party or open emulator needs research.

</details>

---

# Part B: System Requirements Document (SRD / SRS)

<details>
<summary><strong>B1. Introduction</strong></summary>

**Purpose:** Define the technical requirements, architecture, and constraints needed to build the product described in Part A.

**Scope:** Frontend web application, backend services (compile, storage, auth), simulation workers, PCB engine, and exports.

**Definitions:** MCU (microcontroller unit), DRC (design rule check), BOM (bill of materials), Gerber (PCB manufacturing format), netlist (list of electrical connections), footprint (physical pad layout of a part).

</details>

<details>
<summary><strong>B2. System architecture</strong></summary>

```
Browser (React + TypeScript)
 ├─ Wiring Canvas (React Flow)
 ├─ Custom Part Builder (SVG preview)
 ├─ Code Editor (Monaco)
 ├─ Simulation Worker (Web Worker: avr8js / rp2040js / MicroPython WASM)
 ├─ Dashboard + Serial Monitor
 └─ PCB Editor (canvas/SVG) + Gerber exporter
        │  HTTPS
        ▼
Backend
 ├─ API (Node.js or FastAPI)
 ├─ Auth
 ├─ Compile Service (sandboxed Arduino CLI, queue, cache)
 ├─ PostgreSQL (users, projects, parts, shares)
 └─ Object storage (project files, compiled artifacts, exports)
```

**Key design decisions**

1. Simulation and PCB export run client-side, keeping server cost low and working offline after load.
2. A single `PartDefinition` format is the source of truth for wiring, simulation, and PCB footprint.
3. The netlist is derived from the wiring graph and consumed by the PCB editor.
4. Compile is the only mandatory server-side compute.

</details>

<details>
<summary><strong>B3. Technology stack</strong></summary>

See the [Tech stack](#tech-stack) section above. Choices to evaluate before committing: tscircuit for PCB tooling, Freerouting for autorouting, and free-tier limits of the chosen hosts (they change).

</details>

<details>
<summary><strong>B4. Functional requirements</strong></summary>

Priority: M = must (MVP), S = should, C = could.

**Wiring canvas**

| ID | Requirement | Priority |
|---|---|---|
| FR-CAN-01 | Place, move, rotate, and delete parts on a canvas | M |
| FR-CAN-02 | Render one connection handle per pin from the part's `PartDefinition` | M |
| FR-CAN-03 | Draw and delete wires between pins | M |
| FR-CAN-04 | Check connections while dragging (`isValidConnection`) and show the reason when rejected | M |
| FR-CAN-05 | Whole-graph linter on every change, listing issues by severity (error, warning, info) | M |
| FR-CAN-06 | Undo and redo | S |
| FR-CAN-07 | Multiple boards in one project | M |

**Validation rules**

| ID | Rule | Severity |
|---|---|---|
| FR-VAL-01 | 5V output connected to a 3.3V-only input pin | Error |
| FR-VAL-02 | No common GND between connected parts | Error |
| FR-VAL-03 | UART TX to TX, or RX to RX | Warning |
| FR-VAL-04 | Two outputs driving the same net | Error |
| FR-VAL-05 | Power pin left unconnected | Warning |
| FR-VAL-06 | I2C bus missing pull-ups where the part has none | Info |
| FR-VAL-07 | Duplicate I2C address on one bus | Warning |
| FR-VAL-08 | Rules are small, pure, individually testable functions; new rules are added by adding a file | M |

**Custom part builder**

| ID | Requirement | Priority |
|---|---|---|
| FR-PART-01 | Define part name, category, body size, and pins | M |
| FR-PART-02 | Each pin has a name, one or more function types, and a logic voltage | M |
| FR-PART-03 | Each pin has pad data: x/y (mm), shape, kind (through-hole or SMD), copper size, drill | M |
| FR-PART-04 | Layout presets (single row, dual row, grid) and configurable pitch, default 2.54 mm | M |
| FR-PART-05 | Live SVG footprint preview | M |
| FR-PART-06 | Validate parts before saving (unique pin IDs, drill smaller than copper size, no overlapping pads) | M |
| FR-PART-07 | A saved part works in wiring, simulation metadata, and PCB footprint without further input | M |
| FR-PART-08 | Publish a part to the community library with version and license | S |

**Code editor and simulation**

| ID | Requirement | Priority |
|---|---|---|
| FR-SIM-01 | Code editor with syntax highlighting for C/C++ and Python | S |
| FR-SIM-02 | Run AVR firmware from a .hex file in a Web Worker without blocking the UI | S |
| FR-SIM-03 | Map simulated pin changes to visible canvas state (for example an LED lighting up) | S |
| FR-SIM-04 | Serial monitor with output and input | S |
| FR-SIM-05 | Environment sliders feeding sensor models | S |
| FR-SIM-06 | Behavioral models for LED, button, potentiometer, DHT22, MPU6050 (I2C), SSD1306 OLED (I2C), UART GPS | S |
| FR-SIM-07 | Run RP2040 firmware and MicroPython in the browser | S |
| FR-SIM-08 | Clearly label parts and MCUs that are wiring-only (not simulated) | M |
| FR-SIM-09 | Compile API for Arduino C/C++ | S |

**Dashboard**

| ID | Requirement | Priority |
|---|---|---|
| FR-DASH-01 | Drag-and-drop gauges, line charts, toggles, and a map widget bound to serial or simulated values | C |
| FR-DASH-02 | Dashboard layouts saved with the project | C |

**PCB editor and export**

| ID | Requirement | Priority |
|---|---|---|
| FR-PCB-01 | Generate a netlist and ratsnest from the wiring graph | S |
| FR-PCB-02 | Define a board outline and place footprints | S |
| FR-PCB-03 | Route copper traces on two layers with vias | S |
| FR-PCB-04 | DRC for clearance, minimum trace width, drill size, unconnected nets, and overlaps, with rules per fab profile | S |
| FR-PCB-05 | Export Gerber (copper, mask, silkscreen, outline), drill files, and BOM (CSV) as a zip | S |
| FR-PCB-06 | Verify exports against a reference Gerber viewer and at least one fab's upload checker | S |
| FR-PCB-07 | Autorouter by integrating an existing engine | C |

**Accounts, projects, and sharing**

| ID | Requirement | Priority |
|---|---|---|
| FR-ACC-01 | Register and sign in by email and social login | S |
| FR-ACC-02 | Save projects locally (JSON) without an account | M |
| FR-ACC-03 | Signed-in users save to the cloud and share by link (view or fork) | S |
| FR-ACC-04 | Teachers create classes and assignments and view submissions | S |
| FR-ACC-05 | Subscription billing through a payment provider with plan limits enforced server-side | S |

</details>

<details>
<summary><strong>B5. Data model</strong></summary>

The `PartDefinition` is the single source of truth (see [How custom parts work](#how-custom-parts-work)). All schemas are validated with Zod on load and upload.

```ts
interface Project {
  id: string;
  schemaVersion: number;
  nodes: PlacedPart[];        // partId, position, rotation
  edges: Wire[];              // fromPin, toPin
  code: Record<string, string>;
  dashboard?: DashboardLayout;
  pcb?: PcbLayout;            // outline, placements, tracks, vias
}
```

**Database tables (PostgreSQL):** users, projects, project_versions, parts, part_versions, shares, classes, assignments, submissions, subscriptions, compile_jobs, reports.

**Versioning rule:** every saved project records its `schemaVersion`, and migrations run on load so old projects never break.

</details>

<details>
<summary><strong>B6. Simulation engine requirements</strong></summary>

| ID | Requirement |
|---|---|
| SIM-01 | Each simulated MCU runs in its own Web Worker, communicating by message passing |
| SIM-02 | Worker to UI: pin state changes, serial output, errors, timing. UI to worker: start, stop, reset, serial input, sensor values |
| SIM-03 | Peripheral model interface exposes attach(bus or pins), onTransaction(data), update(environment); new sensors implement it |
| SIM-04 | Launch targets: ATmega328P (Uno/Nano), ATmega2560 (Mega) where feasible via avr8js, RP2040 via rp2040js, MicroPython via WebAssembly |
| SIM-05 | UI throttles canvas updates (for example 30 to 60 fps) regardless of simulation speed |
| SIM-06 | Show simulation speed and warn when real-time speed cannot be kept |
| SIM-07 | ESP32, ESP32-C3/S3, and STM32 are wiring and PCB only at launch, and labeled as such |

**Known limit:** Peripheral models approximate behavior. The product does not claim electrical accuracy for sensors, only functional behavior suitable for learning and logic testing.

</details>

<details>
<summary><strong>B7. Compile service requirements</strong></summary>

```
Browser -> POST /compile { board, code, libraries }
       -> authenticate + rate-limit
       -> hash(code + board + libs) -> cache hit? return artifact
       -> queue job -> sandboxed worker runs arduino-cli compile
       -> store artifact -> return .hex or error text
```

| ID | Requirement |
|---|---|
| CMP-01 | Compile in isolated containers with no network access, CPU and memory limits, and a hard timeout (for example 30 to 60 seconds) |
| CMP-02 | Cache results by content hash |
| CMP-03 | Rate-limit users by plan (anonymous, free, Pro) |
| CMP-04 | Only a pre-installed, curated set of libraries is available |
| CMP-05 | Return compiler errors with line numbers and show them in the editor |
| CMP-06 | Use a job queue so spikes do not crash the service |
| CMP-07 | Delete or expire source code and artifacts after a retention period |

</details>

<details>
<summary><strong>B8. PCB engine and export requirements</strong></summary>

| ID | Requirement |
|---|---|
| PCB-01 | Units are millimeters internally, with a single documented origin and axis convention |
| PCB-02 | Supported: 2-layer boards, rectangular and polygonal outlines, through-hole and SMD pads, vias, copper pours (later) |
| PCB-03 | Fab profiles (minimum trace width, clearance, drill, annular ring) selectable per manufacturer |
| PCB-04 | Gerber output in RS-274X with Excellon drill files; layers named to common fab conventions |
| PCB-05 | BOM export: reference, value, footprint, quantity, and manufacturer part number where available |
| PCB-06 | A pre-export checklist runs DRC and warns of unresolved issues before download |
| PCB-07 | Automated tests compare generated output with known-good files |

</details>

<details>
<summary><strong>B9. API summary</strong></summary>

| Endpoint | Purpose |
|---|---|
| `POST /auth/*` | Register, login, refresh |
| `GET/POST/PUT/DELETE /projects` | Project CRUD |
| `POST /projects/:id/share` | Create view or fork link |
| `GET/POST /parts`, `POST /parts/:id/publish` | Part library and community publishing |
| `POST /parts/:id/report` | Report a bad part |
| `POST /compile` | Submit compile job |
| `GET /compile/:jobId` | Poll status and result |
| `GET/POST /classes`, `/assignments`, `/submissions` | Classroom mode |
| `POST /billing/webhook` | Payment provider events |

All endpoints use JSON over HTTPS, versioned under `/v1`, with consistent error responses and pagination.

</details>

<details>
<summary><strong>B10. Non-functional requirements</strong></summary>

| Category | Requirement |
|---|---|
| Performance | Canvas stays responsive with at least 200 parts and 500 wires; first load under 5 seconds on typical broadband (assumption); simulation runs off the main thread |
| Scalability | Static, CDN-served frontend; horizontally scalable backend; compile workers scale independently |
| Availability | Frontend and local mode work when the backend is down; target 99% backend uptime in early stage |
| Compatibility | Latest two versions of Chrome, Edge, Firefox, and Safari on desktop; tablets best-effort; phones view-only at first |
| Usability | First circuit in under 10 minutes; keyboard shortcuts; clear error messages |
| Accessibility | Keyboard navigation, sufficient contrast, never rely on color alone for warnings |
| Reliability | Local autosave every few seconds; recover after browser crash |
| Maintainability | TypeScript strict mode, linting, modular rules and parts, documented schemas |
| Internationalization | Externalized text for translation (Hindi and other languages later) |
| Observability | Error tracking, privacy-respecting analytics, compile queue metrics, cost dashboards |

</details>

<details>
<summary><strong>B11. Security and privacy requirements</strong></summary>

| ID | Requirement |
|---|---|
| SEC-01 | Compile jobs run untrusted code: containers, no network, resource limits, non-root users |
| SEC-02 | Hashed credentials or a trusted identity provider; short-lived tokens |
| SEC-03 | Authorization checks on every project, class, and part endpoint |
| SEC-04 | Community parts are data only; validate every upload against the Zod schema and size limits |
| SEC-05 | Sanitize all user-provided text and SVG before rendering to prevent XSS |
| SEC-06 | Rate limiting and abuse detection on public endpoints |
| SEC-07 | Payments handled entirely by a payment provider; card data is never stored |
| SEC-08 | Privacy policy and terms; data export and deletion on request; comply with applicable laws (for example India's DPDP Act and GDPR where relevant); confirm with legal counsel |
| SEC-09 | Student accounts may include minors: collect minimal data and obtain consent where required |

</details>

<details>
<summary><strong>B12. Infrastructure and estimated cost (assumption)</strong></summary>

| Stage | Setup | Rough monthly cost |
|---|---|---|
| Prototype / Phase 1 | Static hosting plus local storage only | Near zero |
| Phase 2 | Small API, database, one compile container | Low (tens of dollars) |
| Growth | Managed database, object storage, autoscaled compile workers, monitoring | Hundreds of dollars, scaling with compile usage |

**Cost controls:** content-hash caching, per-plan quotas, precompiled examples, and keeping all simulation client-side. Check current provider free-tier limits before choosing hosts.

</details>

<details>
<summary><strong>B13. Testing and quality requirements</strong></summary>

| Area | Approach |
|---|---|
| Validation rules | Unit tests for every rule with passing and failing cases |
| Part generator | Property tests: generated pad positions, no overlaps, correct pitch |
| Simulation | Run known firmware (blink, serial echo, I2C read) and assert expected pin and serial output |
| Gerber/BOM export | Compare with known-good files; open in an independent Gerber viewer; test-order a physical board before claiming factory-ready |
| Frontend | Component tests plus end-to-end tests of core flows |
| Compile service | Security tests (fork bombs, large output, network attempts) and load tests |
| Cross-browser | Manual and automated checks on supported browsers |

</details>

<details>
<summary><strong>B14. Licensing and legal requirements</strong></summary>

- Audit the license of every bundled asset (Fritzing parts, KiCad footprints, tscircuit, avr8js, rp2040js, MicroPython, Monaco, Freerouting). Some licenses (CC-BY-SA, GPL) impose attribution or share-alike obligations that affect a commercial product.
- Store license and author on each library part and show attribution.
- Community uploads require a license choice and a statement that the uploader has the right to publish.
- Provide takedown and report procedures.
- Do not use manufacturer logos or trademarks without permission.
- Exported PCBs carry a disclaimer: users are responsible for verifying designs before manufacture.

</details>

<details>
<summary><strong>B15. Milestones and acceptance criteria</strong></summary>

| Milestone | Acceptance criteria |
|---|---|
| **M1: Wiring MVP** | User places 5 starter parts, wires them, sees at least 4 validation rules fire correctly, saves and reloads JSON |
| **M2: Custom parts** | User builds a custom 8-pin module with through-hole pads; it appears on the canvas and in a footprint preview without further input |
| **M3: First simulation** | Precompiled blink hex runs on a simulated Uno, an LED toggles on the canvas, and the serial monitor shows output |
| **M4: Compile + sensors** | User compiles a sketch via the cloud service and reads a simulated I2C sensor controlled by a slider |
| **M5: PCB export** | A simple project exports Gerber, drill, and BOM that pass a Gerber viewer and a fab's upload check |
| **M6: Classroom + billing** | Teacher creates a class and assignment; a student submits; a paid plan can be purchased and enforced |

</details>

<details>
<summary><strong>B16. Dependencies, open items, and glossary</strong></summary>

**Dependencies and open items**

- Confirm that selected open-source libraries are maintained and licensed for commercial use.
- Confirm partner fab and distributor affiliate programs.
- Choose backend language and hosting provider.
- Decide how community moderation is staffed.
- Research feasibility of ESP32 and STM32 execution before promising it publicly.

**Glossary**

| Term | Meaning |
|---|---|
| MCU | Microcontroller unit, the programmable chip on a board |
| Netlist | List of which pins are electrically connected |
| Footprint | Physical pad layout of a part on a PCB |
| Through-hole | Pad with a drilled hole for leaded components |
| SMD | Surface-mount device pad, no drill |
| DRC | Design rule check, automated PCB rule verification |
| Gerber | Standard file format for PCB manufacturing layers |
| BOM | Bill of materials, list of parts to buy |
| Web Worker | Browser background thread for heavy computation |
| WASM | WebAssembly, fast code execution format in browsers |

</details>


## Contributing

Contributions are welcome once the core structure is stable.

1. Open an issue to discuss larger changes before starting work.
2. Fork the repo and create a branch: `git checkout -b feature/your-feature`.
3. Follow the code style (TypeScript strict mode, ESLint, Prettier).
4. Add tests, especially for validation rules and export code.
5. Run `npm run lint && npm run test` before committing.
6. Open a pull request describing what changed and why.

Good first contributions: new validation rules, new part definitions, sensor models, documentation, and bug reports.

Please read [`CONTRIBUTING.md`](CONTRIBUTING.md) and [`CODE_OF_CONDUCT.md`](CODE_OF_CONDUCT.md) before contributing.

## Community parts guidelines

Wrong footprints waste real money on PCB orders, so published parts are held to a higher bar:

- Include the datasheet or source reference for pinout and dimensions.
- Choose a license and confirm you have the right to publish the part.
- Pad drill sizes must be smaller than copper sizes, and pads must not overlap.
- Parts are data only. Executable code is never accepted in a part.
- Parts may be reported, reviewed, and removed. Verified parts receive a badge.

## Security

- Compile jobs run untrusted code and are sandboxed with no network, resource limits, and timeouts.
- Please report vulnerabilities privately as described in [`SECURITY.md`](SECURITY.md) (or by email to `<rakeshchoudhary1154@gmail.com>`) instead of opening a public issue.

## Licensing and attribution

- **Project license:** Pinvora is licensed under the [Apache License 2.0](LICENSE). See the [`NOTICE`](NOTICE) file for attribution.
- **Name and logo:** The Apache license does not grant rights to use the "Pinvora" name or logo (Section 6 of the license). Forks should use a different name.
- **Contributions:** Unless you state otherwise, any contribution you submit is licensed under Apache-2.0 (Section 5 of the license).
- Third-party libraries and assets keep their own licenses. Fritzing parts, KiCad footprints, tscircuit, avr8js, rp2040js, MicroPython, Monaco Editor, and Freerouting each have their own terms (some are CC-BY-SA or GPL, which add attribution or share-alike requirements). They are recorded in [`THIRD_PARTY_LICENSES.md`](THIRD_PARTY_LICENSES.md); verify compatibility before any commercial release.
- Product names and logos belong to their owners. This project is not affiliated with Arduino, Espressif, Raspberry Pi, STMicroelectronics, or any other vendor.

## FAQ

**Do I need hardware to use it?**
No. The goal is to wire, code, and simulate without owning any boards.

**Can I run my own Arduino code?**
Planned. Early versions will run precompiled examples; cloud compile comes after the simulator works.

**Is it free?**
The core learning features are intended to stay free. Optional paid plans may cover heavier usage, private projects, and classroom tools.

**Can I order a real PCB from it?**
That is the Phase 3 goal. Review and verify the exported files before ordering.

**Does it simulate ESP32?**
Not yet. ESP32 and STM32 are supported for wiring and PCB design only.

## Acknowledgements

Built on the work of the open-source community, including React Flow, Monaco Editor, avr8js, rp2040js, MicroPython, KiCad, Fritzing, tscircuit, and Arduino CLI.

---

*If this project helps you, consider giving it a star and sharing feedback through issues.*
