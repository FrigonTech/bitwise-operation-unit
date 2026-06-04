# Bitwise Operation Unit — User Guide & Instruction Manual

Welcome to the **Bitwise Operation Unit**, a visual, interactive simulator designed for prototyping, debugging, and understanding bitwise logic, binary states, and variable registers. This tool supports both desktop hardware (Drag and Drop) and mobile devices (Tap-to-Assign).

---

## 1. Interface Layout Overview

The workspace is divided into two core functional regions:
* **The Utility Control Sidebar (Left Panel):**
    * **Operators Container:** Holds the 9 supported bitwise logic and shift mechanisms.
    * **Variables Register Container:** Displays your globally declared custom registers, showing their binary patterns, decimal totals, and hex equivalents in real-time.
* **The Computation Canvas (Main Workspace):**
    * The scrollable canvas containing all your active operation blocks, control sliders, and numeric readouts.

---

## 2. Core Operation Workflows

### Creating a Computation Block
1. Click the **`+ operation`** button in the top toolbar to instantiate an empty calculator block on the canvas.
2. Alternatively, drag any operator chip directly from the sidebar and drop it onto an empty area of the canvas to create a block with that operator pre-assigned.

### Assigning Operators
* **Desktop:** Drag an operator chip (e.g., `& AND`, `^ XOR`, `<< SHL`) and drop it directly onto the `drop op` container inside a block.
* **Mobile / Touch:** Tap the desired operator chip in the sidebar (it will glow blue to indicate it is active), then tap the target block's `drop op` zone to bind it.
* *Note:* Clicking an already assigned operator inside a block clears it back to an unassigned state.

### Editing Input States (Slot A & Slot B)
* **Direct Bit Manipulation:** Click or tap any individual bit cell inside the interactive binary strip to toggle its state (`0` $\leftrightarrow$ `1`). The decimal and hexadecimal readouts below update instantly.
* **Bit-Width Resolution Tuning:** Use the **`bits`** range slider in the block ribbon to scale the active resolution anywhere between **1-bit** and **20-bits**. Changing the width automatically masks out high bits to prevent overflow errors.

---

## 3. Register Promotion & Interlinking Variables

The architecture allows you to convert temporary slot configurations or raw calculation outputs into persistent, global variables.

### Promoting an Input or Result
1. Click **`↑ promote`** on an input slot header to map its current state out to a global variable.
2. Click **`↑ promote result`** on a block's bottom footer to instantly convert the calculation output into a reactive global variable (automatically named `R1`, `R2`, etc.).
3. Once promoted, the new tracking badge appears in the left **Variables** panel.

### Feeding Variables into Inputs
* **Desktop:** Drag a variable chip from the sidebar and drop it into the dashed `slot dropzone` of **Slot A** or **Slot B**.
* **Mobile / Touch:** Tap the variable chip in the sidebar (it will glow green), then tap any unlinked slot dropzone to connect it.
* *Reactive Propagation:* When an input slot is bound to a variable, toggle-clicking its bit cells writes directly back to that variable's shared memory, instantly forcing all other blocks connected to that variable to recalculate across the workspace.
* **Unlinking:** Click the small **`×`** button next to a linked variable's badge in a slot header to safely sever the connection and return to independent bit editing.

---

## 4. Built-in Failsafe Engines

To maintain absolute stability and prevent layout exceptions, two background guard systems run automatically:

### 1. The Anti-Interlink Loop Guard
To prevent infinite recursive loops (where a block acts as its own grandparent dependency), **the engine prohibits dropping or tapping a block's calculation output back into its own Slot A or Slot B.**
* If an illegal link is attempted, the block's outer border will flash red as a warning signal, and the assignment is instantly rejected.

### 2. Isolated DOM Event Interception
All drag-and-drop operations bypass local node instances and are tracked at the root window level. This ensures that even when calculation results cause instant panel refreshes, your mouse drag focus is never dropped or glitched mid-movement.

---

## 5. Technical Specifications Reference

| Operator | Mathematical Equivalent | Behavior Profile | Unary / Binary |
| :--- | :--- | :--- | :--- |
| **`&` AND** | $A \text{ AND } B$ | Outputs `1` if both matching bits are `1` | Binary |
| **`\|` OR** | $A \text{ OR } B$ | Outputs `1` if at least one matching bit is `1` | Binary |
| **`^` XOR** | $A \oplus B$ | Outputs `1` if matching bits are different | Binary |
| **`~` NOT** | $\text{NOT } A$ | Inverts all active bits within the bit-width resolution | Unary (Disables B) |
| **`~&` NAND** | $\text{NOT } (A \text{ AND } B)$ | Inverted AND logic gate | Binary |
| **`~\|` NOR** | $\text{NOT } (A \text{ OR } B)$ | Inverted OR logic gate | Binary |
| **`~^` XNOR**| $\text{NOT } (A \oplus B)$ | Inverted XOR (Outputs `1` if matching bits are identical) | Binary |
| **`<<` SHL** | $A \times 2^B$ | Shifts bits left by $B$ places, filling gaps with `0` | Binary |
| **`>>` SHR** | $A \gg B$ | Logical right shift, moving bits right while filling with `0` | Binary |
