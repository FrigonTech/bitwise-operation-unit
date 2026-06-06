# Bitwise Operation Unit — Interactive Bit Manipulation Playground

[![Launch Tool](https://img.shields.io/badge/Launch%20Tool-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white)](https://frigontech.github.io/bitwise-operation-unit/)
![HTML](https://img.shields.io/badge/HTML-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![No Dependencies](https://img.shields.io/badge/dependencies-none-brightgreen?style=for-the-badge)

A free, browser-based **bitwise operations visualizer** for learning and testing binary logic in real time. Build chained calculation blocks, flip individual bits, link variables across operations, and watch AND, OR, XOR, NOT, NAND, NOR, XNOR, shift left, and shift right propagate live — no install, no build step, no backend.

> Built by [FrigonTech](https://github.com/frigontech) · [frigontech.github.io/bitwise-operation-unit](https://frigontech.github.io/bitwise-operation-unit/)

---

## What Is This?

Most bitwise calculators give you a box, two inputs, and a result. This tool lets you **build a pipeline** — multiple linked operation blocks where the output of one feeds directly into the input of the next, updating everything downstream in real time.

Designed for:

- **CS students** learning bit manipulation, binary arithmetic, and logic gates
- **Embedded / systems programmers** verifying masking, toggling, and clearing logic before writing it into C or C++
- **Competitive programmers** testing bitmask tricks and shift-based optimizations
- **Anyone** who wants to understand what `x & ~(1 << n)`, `a ^ b`, or `~a & 0xFF` actually does at the bit level

---

## Features

- **9 operators** — AND `&`, OR `|`, XOR `^`, NOT `~`, NAND `~&`, NOR `~|`, XNOR `~^`, Shift Left `<<`, Shift Right `>>`
- **Drag-and-drop operator placement** — drag a logic gate chip onto any operation block
- **Clickable individual bits** — toggle any bit in slot A or B directly; result recalculates instantly
- **1–20 bit width slider** per block — see real truncation and overflow behavior at any precision
- **Variable promotion** — save any input or result as a named variable (`A1`, `B1`, `R1`...) in the sidebar
- **Live variable propagation** — link a variable to multiple blocks; changing one bit updates every block using it simultaneously
- **Chained operations** — promote a result, drag it into the input of the next block, build multi-stage pipelines
- **Anti-loop guard** — blocks reject their own result variable being fed back as an input
- **Tap support** — fully usable on touchscreen; tap an operator to prime it, tap a drop zone to place it
- **Zero dependencies** — single self-contained HTML file, works offline after first load

---

## The Layout

Your workspace is split into two zones:

- **Left Sidebar** — top half holds the **Operators** panel (all 9 logic gate chips). Bottom half is the **Variables Register** — your saved registers displayed with their binary, decimal, and hex values side by side.
- **Main Canvas** — the scrollable workspace where you spawn, configure, and chain your calculation blocks.

---

## How to Use

### Step 1 — Create an Operation Block

- **Quick way:** Click **`+ operation`** in the toolbar. An empty block appears on the canvas.
- **Flex way:** Drag any operator chip (e.g. `& AND`, `^ XOR`) from the sidebar directly onto the canvas — it auto-creates a block with that operator already placed.

### Step 2 — Place a Logic Operator

If your block is empty, it needs an operator before it can calculate:

- **Mouse:** Drag a logic chip from the sidebar and drop it into the **`drop op`** zone in the center of the block.
- **Touchscreen:** Tap an operator chip (it glows to confirm it's primed), then tap the block's **`drop op`** target.
- Changed your mind? Click the placed operator inside the block to clear it.

### Step 3 — Set Your Input Bits

Slot A and Slot B each show a row of individual bit cells:

- **Click or tap any bit cell** to flip it between `0` and `1`
- The decimal and hex values beneath each slot update live as you toggle
- The **RESULT** row at the bottom recalculates instantly on every change

### Step 4 — Adjust Bit Width

- Grab the **`bits` slider** in the block's header ribbon
- Range is **1 to 20 bits** — the layout resizes and arithmetic is masked to fit, so you can observe real truncation and overflow behavior safely at any word size

---

## Variable Promotion & Chaining (Advanced)

This is what separates this tool from a basic bitwise calculator. You can link blocks together into a live data pipeline.

### Promoting a Slot or Result

Configured a useful bit pattern? Save it:

- Click **`↑ promote`** on any input slot, or **`↑ promote result`** at the bottom of a block
- The value is extracted and stored as a named variable in the sidebar (`A1`, `B2`, `R1`, etc.)
- Names are assigned progressively — promoting the same slot twice gives `A1`, then `A2`, never a collision

### Feeding Variables Into Blocks

- **Drag** (or **tap-then-tap**) any variable from the sidebar into the dashed drop zone of any input slot on any block
- Once linked, toggling a bit in that slot updates the variable itself — and **every other block using that variable recalculates instantly**
- To unlink a slot without deleting the variable, click the small **`×`** next to the variable badge in the slot header

### Building a Chain

```
Block 1: A & B  →  promote result as R1
                         ↓
Block 2: R1 ^ C  →  promote result as R2
                         ↓
Block 3: ~R2  →  final output
```

Flip any bit anywhere in the chain — every downstream block updates in the same frame.

---

## Built-In Safeguards

- **Anti-Interlink Loop Guard** — if you attempt to drop a block's own result variable back into one of its own input slots, the block flashes a red outline and rejects the link. Prevents infinite recalculation loops.
- **Drag Isolation** — drag events are intercepted at the root layout level, not on individual elements. This means variable dragging stays stable even while multiple blocks are propagating cascaded updates simultaneously.

---

## Operator Cheat Sheet

| Symbol | Name | How It Works | Type |
|:---:|---|---|:---:|
| `&` | AND | Output `1` only if **both** A and B bits are `1` | Binary |
| `\|` | OR | Output `1` if **either** A or B bit is `1` | Binary |
| `^` | XOR | Output `1` if A and B bits are **different** | Binary |
| `~` | NOT | Inverts **every** bit — `1` becomes `0`, `0` becomes `1` | Unary |
| `~&` | NAND | AND result, then fully inverted | Binary |
| `~\|` | NOR | OR result, then fully inverted | Binary |
| `~^` | XNOR | Output `1` if A and B bits are **identical** | Binary |
| `<<` | Shift Left | Slides all bits left by B positions, fills gaps with `0` | Binary |
| `>>` | Shift Right | Slides all bits right by B positions, discards overflow | Binary |

---

## Running Locally

No build step required — just open the file:

```bash
git clone https://github.com/frigontech/bitwise-operation-unit.git
cd bitwise-operation-unit
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

Or serve it:

```bash
npx serve .
# → http://localhost:3000
```

---

## Deploying to GitHub Pages

```
1. Rename BitOpUnit.html → index.html at the repo root
2. Repo Settings → Pages → Source: Deploy from branch → main → / (root)
3. Save — live at https://<username>.github.io/bitwise-operation-unit/ in ~60 seconds
```

---

## Related Topics

`bit manipulation` · `bitwise operators` · `binary calculator` · `logic gates` · `bitmask` · `bit shifting` · `binary visualization` · `AND OR XOR NOT` · `bitwise AND calculator` · `interactive binary tool` · `low-level programming` · `embedded systems` · `computer science education` · `C bitwise operators` · `bit toggling` · `bit masking`

---

## License

MIT — free to use, modify, and deploy.

---

*Made by [FrigonTech](https://github.com/frigontech) — indie dev tools for programmers who think in bits.*
