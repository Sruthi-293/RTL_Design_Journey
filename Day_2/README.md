🟩 Day 2 — Timing Libraries & RTL Synthesis

🎯 Objective

The main objective of Day 2 was to understand logic synthesis using Yosys and learn how Verilog RTL code is converted into a synthesized hardware representation.

During this session, I worked with a 2:1 Multiplexer and explored the synthesis process, standard-cell libraries, graphical representation, and the generated netlist.

⸻

1️⃣ Introduction to Yosys

Yosys is an open-source synthesis tool used for processing Verilog RTL designs. It analyzes the RTL description and transforms it into a lower-level hardware representation called a netlist.

Instead of manually designing the corresponding gates, Yosys performs the conversion and optimization automatically.

Main activities performed by Yosys:

* Reading the Verilog RTL design
* Understanding the design hierarchy
* Converting RTL constructs into logic
* Optimizing the logic
* Simplifying the design
* Mapping logic to available cells
* Generating the final synthesized netlist

  
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

*5️ Basic Yosys Commands:*

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


5️⃣ Graphical Representation of the Synthesized Design

After completing synthesis, I generated a graphical view of the circuit using Yosys.

The graphical representation makes it easier to observe how the RTL design has been transformed into internal logic and how different signals are connected.

image

The above image shows the synthesized structure of the 2:1 multiplexer. It displays the input signals i0, i1, and sel, along with the output y. This visualization helped me understand the internal structure produced by the synthesis process.

6️⃣ Understanding the Synthesized Netlist

The synthesis process also produces a Verilog netlist. Unlike the original RTL code, the synthesized netlist describes the design using lower-level logic structures and cell connections.

I inspected the generated netlist to understand how Yosys represented the multiplexer after synthesis.

image 

The image shows the Verilog code generated after synthesis. It contains the module ports, internal wires, and synthesized cell connections. By examining this output, I understood how the original RTL description is transformed into a hardware-oriented representation.

7️⃣Hierarchical vs Flattened Synthesis

Hierarchical Synthesis

The design hierarchy is preserved.

Flattened Synthesis

The hierarchy is removed and the design is represented as a flattened structure.

Understanding both approaches helps in analyzing how synthesis tools process RTL designs.

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
