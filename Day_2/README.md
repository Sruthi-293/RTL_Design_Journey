🟩 Day 2 — Timing Libraries & RTL Synthesis

🎯 Objective

Day 2 focuses on understanding how RTL designs are synthesized into gate-level representations using Yosys and technology libraries.

⸻

1️⃣ Introduction to Yosys

Yosys is an open-source framework used for RTL synthesis.

It converts RTL descriptions into a synthesized representation.

Basic flow:

RTL → Yosys → Logic → Technology Mapping

⸻

2️⃣ Technology Libraries

Technology libraries contain information about the cells available in a particular semiconductor technology.

The workshop uses the SKY130 technology.

Examples of standard cells include:

* Inverters
* AND gates
* OR gates
* NAND gates
* NOR gates
* Flip-flops

⸻

3️⃣ Timing Libraries

Timing libraries contain information used to describe the timing characteristics of standard cells.

Important information includes:

* Cell delay
* Timing arcs
* Setup time
* Hold time
* Power-related information

⸻

4️⃣ Yosys Synthesis Flow

A typical synthesis flow includes:

Read RTL
   ↓
Elaborate Design
   ↓
Process RTL
   ↓
Optimize
   ↓
Technology Mapping
   ↓
Generate Netlist

⸻

5️⃣ Basic Yosys Commands

Start Yosys:

yosys

Read the Verilog design:

read_verilog design.v

Select the top module:

hierarchy -top design

Perform synthesis:

synth

Display the synthesized design:

show

Exit:

exit

⸻

6️⃣ Hierarchical vs Flattened Synthesis

Hierarchical Synthesis

The design hierarchy is preserved.

Flattened Synthesis

The hierarchy is removed and the design is represented as a flattened structure.

Understanding both approaches helps in analyzing how synthesis tools process RTL designs.

⸻

7️⃣ Practical Experiment

Perform the synthesis experiment using Yosys.

📸 Add your Yosys terminal screenshot here.

📸 Add your synthesized design screenshot here.

⸻

🧠 What I Learned

* Purpose of synthesis
* Basics of Yosys
* Technology libraries
* SKY130 standard cells
* Timing libraries
* Hierarchical synthesis
* Flattened synthesis
* RTL-to-netlist conversion

⸻

✅ Day 2 Conclusion

Day 2 helped me understand how a Verilog RTL design moves from simulation toward actual hardware implementation through synthesis.
