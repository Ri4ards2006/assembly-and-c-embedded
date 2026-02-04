# ⚡ Embedded Assembly Lab

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Target: ARM Cortex-M4](https://img.shields.io/badge/Target-ARM%20Cortex--M4-blue.svg)](https://www.arm.com/)
[![Focus: Low-Level](https://img.shields.io/badge/Focus-Low--Level%20Analysis-red.svg)]()

> A professional-grade laboratory for dissecting C/C++ into ARM Assembly. Designed to bridge the gap between high-level logic and register-level execution.

---

## 🏛 Project Architecture

| Directory | Purpose | Contents |
| :--- | :--- | :--- |
| 📁 `src/` | **Lab Experiments** | Isolated C & ASM modules with localized notes. |
| 📁 `docs/` | **Knowledge Base** | Detailed specs on ABI, Pipeline stalls, and ISA. |
| 📁 `scripts/` | **Automation** | Toolchain wrappers for consistent disassembly output. |

---

## 🔬 Core Analysis Workflow

To ensure a "bit-accurate" understanding, every experiment follows the **Observation-Dissection-Conclusion (ODC)** pattern:

1.  **Code (C):** Write minimal, high-impact C code.
2.  **Disassemble:** Use the `scripts/generate_asm.sh` to extract annotated assembly.
3.  **Analyze:** Identify register allocation, branch overhead, and stack pointer movement.



---

## 📊 Roadmap & Mastery Progress

### Phase 1: The Basics (Memory & Logic)
- [x] **01_stack_frames:** Understanding `PUSH`, `POP`, and `LR`.
- [ ] **02_calling_convention:** How the ABI handles >4 arguments.
- [ ] **03_control_flow:** `B`, `BL`, `BX` and the status register (CPSR).

### Phase 2: Hardware Interfacing
- [ ] **04_interrupt_vectors:** Context saving during ISRs.
- [ ] **05_volatile_guards:** Preventing compiler-driven register caching.

### Phase 3: Advanced Optimization
- [ ] **06_simd_neon:** (Optional) Vector instructions for DSP.
- [ ] **07_pipeline_stalls:** Analyzing NOPs and execution alignment.

---

## ⚙️ Setup & Toolchain

To replicate these experiments, you need the **GNU Arm Embedded Toolchain**.

```bash
# Generate disassembly with symbols and source intermixing
arm-none-eabi-gcc -S -fverbose-asm -Og -g main.c -o analysis.s
Developed for deep-level understanding of STM32 and FPGA-softcores.


---

## ⚡ Das "Magic Script" (`scripts/generate_asm.sh`)
Leg das in dein `scripts/` Verzeichnis, damit du wie ein Profi wirkst. Es nimmt dir die ganze Tipparbeit ab:

```bash
#!/bin/bash
# Usage: ./scripts/generate_asm.sh src/01_module/main.c

FILE=$1
FILENAME=$(basename -- "$FILE")
DIR=$(dirname -- "$FILE")
EXTENSION="${FILENAME##*.}"
NAME="${FILENAME%.*}"

echo "🚀 Dissecting $FILENAME..."

arm-none-eabi-gcc -S \
    -fverbose-asm \
    -Og \
    -g \
    -mcpu=cortex-m4 \
    -mthumb \
    "$FILE" -o "$DIR/$NAME.s"

echo "✅ Assembly generated: $DIR/$NAME.s"
