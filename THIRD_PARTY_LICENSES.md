# Third-Party Licenses and Attributions

Pinvora incorporates, depends upon, or plans to integrate various third-party open-source software libraries, simulation engines, and hardware assets. Each third-party component remains subject to its own respective license terms.

> **Disclaimer:** This document serves as a tracking manifest for third-party dependencies and assets. Before any commercial distribution or SaaS launch, verify the exact license text, version, and compliance obligations (especially regarding copyleft or share-alike terms such as GPL and CC-BY-SA) for every included component.

---

## Summary of Third-Party Components

| Component                        | Category          | License                       | Upstream Repository / Source                                                  |
| :------------------------------- | :---------------- | :---------------------------- | :---------------------------------------------------------------------------- |
| **React & React DOM**            | Frontend UI       | MIT                           | [facebook/react](https://github.com/facebook/react)                           |
| **TypeScript**                   | Language          | Apache-2.0                    | [microsoft/TypeScript](https://github.com/microsoft/TypeScript)               |
| **Vite**                         | Build Tool        | MIT                           | [vitejs/vite](https://github.com/vitejs/vite)                                 |
| **Tailwind CSS**                 | Styling           | MIT                           | [tailwindlabs/tailwindcss](https://github.com/tailwindlabs/tailwindcss)       |
| **Zustand**                      | State Management  | MIT                           | [pmndrs/zustand](https://github.com/pmndrs/zustand)                           |
| **React Flow (`@xyflow/react`)** | Wiring Canvas     | MIT                           | [xyflow/xyflow](https://github.com/xyflow/xyflow)                             |
| **Zod**                          | Schema Validation | MIT                           | [colinhacks/zod](https://github.com/colinhacks/zod)                           |
| **Monaco Editor**                | Code Editor       | MIT                           | [microsoft/monaco-editor](https://github.com/microsoft/monaco-editor)         |
| **avr8js**                       | AVR Simulation    | MIT                           | [wokwi/avr8js](https://github.com/wokwi/avr8js)                               |
| **rp2040js**                     | RP2040 Simulation | MIT                           | [wokwi/rp2040js](https://github.com/wokwi/rp2040js)                           |
| **MicroPython**                  | Firmware Runtime  | MIT                           | [micropython/micropython](https://github.com/micropython/micropython)         |
| **Arduino CLI**                  | Compile Toolchain | GPL-3.0                       | [arduino/arduino-cli](https://github.com/arduino/arduino-cli)                 |
| **tscircuit**                    | PCB Tooling       | MIT                           | [tscircuit/tscircuit](https://github.com/tscircuit/tscircuit)                 |
| **Freerouting**                  | PCB Autorouter    | GPL-3.0                       | [freerouting/freerouting](https://github.com/freerouting/freerouting)         |
| **KiCad Footprints / Libraries** | Hardware Assets   | CC-BY-SA-4.0 (with exception) | [KiCad/kicad-footprints](https://gitlab.com/kicad/libraries/kicad-footprints) |
| **Fritzing Parts**               | Hardware Assets   | CC-BY-SA-3.0                  | [fritzing/fritzing-parts](https://github.com/fritzing/fritzing-parts)         |

---

## Detailed License Notes & Compliance Guidelines

### 1. Permissive Licenses (MIT / Apache-2.0)

The majority of Pinvora's frontend and browser-simulation dependencies (including **React**, **Vite**, **Tailwind CSS**, **Zustand**, **React Flow**, **Zod**, **Monaco Editor**, **avr8js**, **rp2040js**, **MicroPython**, and **tscircuit**) are licensed under the **MIT License** or **Apache License 2.0**.

- **Obligation:** Retain the original copyright notices and license texts in source distributions and compiled production bundles (e.g., via automated license-checker plugins during `npm run build`).

### 2. Copyleft Backend Tools (GPL-3.0)

- **Arduino CLI (`GPL-3.0`):** Executed as an isolated, standalone command-line binary inside sandboxed backend containers for the cloud compile service. It is not linked into Pinvora's proprietary or Apache-2.0 frontend code.
- **Freerouting (`GPL-3.0`):** Under evaluation for PCB autorouting. If integrated, it must be run as a separate process/service or isolated module in accordance with GPL-3.0 boundaries so it does not require relicensing of the core application.

### 3. Hardware & Footprint Assets (CC-BY-SA)

- **KiCad Libraries (`CC-BY-SA-4.0` with KiCad Library Exception):** KiCad footprints and symbols are licensed under Creative Commons Attribution-ShareAlike 4.0 International, with a special exception that allows users to create and distribute PCB designs without the resulting board falling under ShareAlike. However, any _modifications_ to the library files themselves must be shared under CC-BY-SA-4.0 with attribution to the KiCad team.
- **Fritzing Parts (`CC-BY-SA-3.0`):** Fritzing part definitions and SVGs are licensed under Creative Commons Attribution-ShareAlike 3.0. Any bundled or derivative parts derived from Fritzing assets must include visible attribution and remain licensed under CC-BY-SA-3.0.

---

## Standard License Texts

### The MIT License (MIT)

```text
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

### GNU General Public License v3.0 (GPL-3.0)

For components licensed under GPL-3.0 (such as Arduino CLI and Freerouting), the full license text is available at:
https://www.gnu.org/licenses/gpl-3.0.txt

### Creative Commons Attribution-ShareAlike (CC-BY-SA 3.0 / 4.0)

For hardware assets licensed under CC-BY-SA, the full legal codes are available at:

- CC-BY-SA 3.0: https://creativecommons.org/licenses/by-sa/3.0/legalcode
- CC-BY-SA 4.0: https://creativecommons.org/licenses/by-sa/4.0/legalcode

---

## Trademark Disclaimer

All product names, microcontroller designations, logos, and brands (including Arduino, ESP32, Espressif, Raspberry Pi, RP2040, STM32, STMicroelectronics, KiCad, and Fritzing) are property of their respective owners. Use of these names in Pinvora is for hardware compatibility and identification purposes only and does not imply endorsement or affiliation.
