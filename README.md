#  Bitwise Operation Unit: The Ultimate Field Manual 

Welcome to the command center of binary wizardry! Whether you are a hardcore low-level engineer or a curious developer trying to visualize how computers compute under the hood, this interactive workspace is your sandbox.

[![Use It](https://img.shields.io/badge/Visit%20Demo-4285F4?style=for-the-badge&logo=googlechrome&logoColor=white)](https://frigontech.github.io/bitwise-operation-unit/)

---

##  The Land Map: What's on Your Screen?

Your digital workshop is split into two power zones:
* **The Left Control Deck (Sidebar):** Your toolbox. The top half holds the heavy-hitters—the **Operators**. The bottom half is your **Variables Register**, your scoreboard where your saved registers live alongside their binary, decimal, and hex conversions.
* **The Main Workspace Canvas:** The giant scrollable field where the magic happens. This is where you spawn, edit, and link your custom calculation blocks.

---

##  Phase 1: Building Your First Operation Block

Ready to see some math in action? Let's cook:

### Step 1: Drop a Block on the Canvas
* **The Quick Way:** Click the **`+ operation`** button in the top toolbar. BOOM. An empty calculation block appears on your workspace.
* **The Flex Way:** Grab an operator chip (like `& AND` or `^ XOR`) from the left panel, drag it onto the canvas, and drop it anywhere. It will auto-generate a block with that operator locked in!

### Step 2: Inject the Logic Gate
If you created an empty block, it's currently waiting for an operator. 
* **Using a Mouse:** Drag your chosen logic chip from the left panel and slam-dunk it into the **`drop op`** box right in the middle of your block.
* **Using a Touchscreen:** Tap the operator chip in the sidebar (it will glow to show it's primed) and then tap the target block's **`drop op`** box.
* *Regret your choice?* Just click an assigned operator inside a block to clear it out and start over.

### Step 3: Play with the Bits!
Look at **Slot A** and **Slot B** inside your block. See those little grid cells? Those are individual bits.
* **Click or Tap any cell** to flip it instantly from `0` to `1` or back again. 
* Watch the numbers underneath update live in decimal and hex as you toggle!

### Step 4: Change the Reality Matrix (Bit-Width Resolution)
Want to see how an 8-bit overflow looks compared to a 4-bit space? 
* Grab the **`bits` slider** on the block's header ribbon. 
* Slide it anywhere from **1-bit** all the way up to **20-bits**. The system instantly adjusts the layout and masks the arithmetic so you can witness real-world truncation bugs safely!

---

##  Phase 2: Variable Promotion & Interlinking (Advanced Mode)

This is where things get incredibly powerful. You aren't just limited to isolated blocks; you can link them together to build complex data pipelines.

### The "↑ Promote" Superpower
Did you just configure a perfect binary pattern in Slot A, or did your block just calculate a brilliant result? **Save it!**
* Click **`↑ promote`** on any input slot or **`↑ promote result`** on the bottom of a block.
* The system immediately extracts that data and creates a permanent global variable register in your left panel (named `A1`, `B1`, `R1`, etc.).

### Building a Chain Reaction (Feeding Variables to Inputs)
Now that you have variables in your sidebar, you can use them as inputs for *other* blocks:
* **Drag & Drop** (or **Tap & Target**) a variable from your sidebar straight into the dashed dropzone of an input slot on *any* block.
* **The Chain Reaction:** When a slot is linked to a variable, toggling a bit inside that slot changes the variable itself. Because that variable is shared, **every other block on your canvas using that variable will recalculate and flash its new value instantly!**
* **The Break Up:** Want to unlock a slot and go back to standalone editing? Click the small **`×`** button next to the variable's name badge in the slot header.

---

##  Built-In Failsafes:

We built two invisible guard-dogs into the background script so you can break the math without breaking the application:

* **The Anti-Interlink Loop Guard:** To prevent an infinite logic loop (e.g., a block trying to calculate its own result as an input, which would crash your browser), **the system will aggressively deny you from dropping or tapping a block's own calculation result back into itself.** If you try, the block will flash a red warning outline and reject the link.
* **Dynamic Drag Isolation:** Because the system renders data at hyper-speed, standard drag listeners can glitch. Our drag engine intercepts movements globally at the root layout level, meaning your variable dragging stays buttery smooth even when multiple blocks are cascading calculations at the exact same millisecond.

---

##  Operator Cheat Sheet

Quick refresher on the logic brains available in your deck:

| Gate Symbol | Name | How it Thinks | Type |
| :---: | :--- | :--- | :--- |
| **`&`** | **AND** | Outputs `1` *only* if both Input A and Input B are `1`. | Binary |
| **`\|`** | **OR** | Outputs `1` if *either* Input A or Input B (or both) are `1`. | Binary |
| **`^`** | **XOR** | Outputs `1` if Input A and Input B are *different* from each other. | Binary |
| **`~`** | **NOT** | The ultimate flipper. It inverts all your bits (`1` becomes `0`, `0` becomes `1`). | Unary (Disables Slot B) |
| **`~&`** | **NAND** | Calculates an AND gate, then completely inverts the output. | Binary |
| **`~\|`** | **NOR** | Calculates an OR gate, then completely inverts the output. | Binary |
| **`~^`** | **XNOR** | Outputs `1` if Input A and Input B are *perfectly identical*. | Binary |
| **`<<`** | **Shift Left** | Slides all bits to the left by the amount specified in Slot B, filling trailing gaps with `0`. | Binary |
| **`>>`** | **Shift Right** | Slides all bits to the right by the amount specified in Slot B, discarding trailing drop-offs. | Binary |

---

Now go create some blocks, chain some registers together, and watch the binary code come alive! 🚀
