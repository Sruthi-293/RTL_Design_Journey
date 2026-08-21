Day 4 — Logic Optimization with Yosys ⚙️

🎯 Objectives

The objective of Day 4 was to understand how synthesis tools optimize RTL designs while preserving their intended functionality.

During this session, I explored different types of combinational and sequential logic optimization using Yosys. I also studied how unnecessary logic, constant values, unused outputs, and redundant sequential elements can be simplified during synthesis.

The main topics covered were:

* Introduction to Logic Optimization
* Combinational Logic Optimization
* Constant Propagation
* Boolean Logic Optimization
* Sequential Logic Optimization
* State Optimization
* Logic Cloning
* Retiming
* Constant Flip-Flop Optimization
* Unused Output Optimization
* RTL-to-Gate-Level Synthesis using Yosys

⸻

1. Introduction to Logic Optimization 🔧

   Logic optimization is an important stage of digital design synthesis. The purpose of optimization is to simplify the hardware implementation while maintaining the same logical behavior.

   A synthesis tool such as Yosys examines the RTL description and identifies unnecessary or redundant logic.

   Optimization can help reduce:

   * Number of logic gates
   * Area of the circuit
   * Switching activity
   * Unnecessary hardware
   * Overall design complexity

   The optimized design can then be mapped to cells available in a standard-cell library such as the SKY130 library.

⸻

2. Combinational Logic Optimization 🔄

   Combinational logic produces outputs based only on the current inputs. During synthesis, Yosys analyzes the logic equations and attempts to find simpler implementations.

   Some common combinational optimization techniques include:

   * Constant propagation
   * Boolean simplification
   * Removing redundant logic
   * Dead-code elimination
   * Common sub-expression simplification

   These optimizations allow the same functionality to be implemented using fewer hardware resources.

⸻

3. Constant Propagation 💡

   Constant propagation is an optimization technique in which known constant values are propagated through the logic.

   For example, if an input is permanently connected to logic 0 or logic 1, Yosys can simplify the surrounding logic based on that known value.

   For example: assign y=a & 1;

   can be simplified to: assign y=a;

   This avoids unnecessary gates in the final implementation

4. Boolean Logic Optimization 🧠

   Yosys also performs Boolean simplification during synthesis.

   Expressions involving AND, OR, NOT, XOR and other logic operations can often be reduced to simpler forms.

   For example:
   A & 1 = A
   A | 0 = A
   A & 0 = 0
   A | 1 = 1

   By applying such transformations, synthesis tools can reduce the amount of hardware required.

⸻

5. Checking Optimization Examples 🔍

   The optimization examples were explored using Yosys and the available SKY130 standard-cell library.

   First, the optimization-related files were identified using:

   ls ***opt***
   
   ls ***opt_check***

   These commands were useful for locating the RTL files related to the optimization experiments.

⸻

5.1 opt_check Optimization

    The first optimization design was synthesized using the following sequence. 

    Step 1-Start Yosys

    yosys

    Step 2-Read the technology library

    read_liberty -lib ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

    Step 3-Read the RTL design

    read_verilog opt_check.v

    Step 4-Synthesize the design

    synth -top opt_check

    Step 5-Remove unused logic

    opt_clean -purge

    Step 6-Technology mapping

    abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

    Step 7-Displaying the optimized design

    show

    Figure 1: Optimized gate-level representation of the opt_check design.

    The synthesized view shows how Yosys simplified the RTL and converted the remaining logic into a gate-level representation.

⸻

5.2 opt_check2 Optimization 🔍

    The second optimization example was analyzed using a similar synthesis flow.
    
    read_verilog opt_check2.v
    
    synth -top opt_check2
    
    opt_clean -purge
    
    abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    
    show
    
    The RTL was synthesized, unnecessary logic was removed, and the remaining logic was mapped using the SKY130 library.
    
    Figure 2: Optimized representation of the opt_check2 design.

    This output helps in understanding how synthesis optimization changes the original RTL structure into a simpler hardware implementation.

⸻

5.3 opt_check3 Optimization 🔍

    The same optimization procedure was applied to opt_check3.v.

    read_verilog opt_check2.v
    
    synth -top opt_check2
    
    opt_clean -purge
    
    abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    
    show

    Figure 3: Optimized gate-level representation of the opt_check3 design.

    The result demonstrates the ability of Yosys to simplify the RTL before mapping it to standard cells.

⸻

5.4 opt_check4 Optimization 🔍

    The fourth optimization example was also synthesized and optimized.

    read_verilog opt_check2.v
    
    synth -top opt_check2
    
    opt_clean -purge
    
    abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
    
    show

    Figure 4: Optimized representation of the opt_check4 design.

    This experiment provided another example of how redundant logic can be identified and removed during synthesis.

⸻

6. Sequential Logic Optimization ⏱️

   Sequential optimization deals with circuits containing memory elements such as flip-flops.

   Unlike combinational logic, sequential circuits depend on previous states as well as current inputs.

   Yosys can optimize sequential circuits by identifying:

   * Constant flip-flops
   * Redundant registers
   * Unused registers
   * Unnecessary state transitions
   * Simplifiable control logic

   Other important sequential optimization concepts include:

   State Optimization

   Unnecessary or unreachable states can be removed or simplified.

   Logic Cloning

   Logic may be duplicated when doing so provides a better implementation for timing or physical design.

   Retiming

   Retiming changes the placement of registers while preserving the overall functionality of the circuit. This can help improve timing performance.

⸻

7. Constant Flip-Flop Optimization 🔄

   The next experiment focused on flip-flops whose values can be determined to be constant.
    
    

    
