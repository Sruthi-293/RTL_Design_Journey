Day 3 — Flip-Flop Coding Styles and Optimization

Objectives

The objective of Day 3 was to understand different ways of describing flip-flops in Verilog, simulate their behavior, and study how synthesis tools optimize RTL designs. The experiments also helped in understanding how Yosys converts RTL code into a gate-level representation using standard-cell libraries.

⸻

1. Flip-Flop Coding Styles

Flip-flops are sequential digital circuits used to store one bit of information. Their output changes according to the clock and the control signals used in the design.

During this session, three different D flip-flop coding styles were studied:

* Asynchronous Reset D Flip-Flop
* Asynchronous Set D Flip-Flop
* Synchronous Reset D Flip-Flop

⸻

1.1 Asynchronous Reset D Flip-Flop

An asynchronous reset can change the output immediately when the reset signal is activated. The reset operation does not have to wait for a clock edge.

Verilog Code
module dff_asyncres (
    input clk,
    input async_reset,
    input d,
    output reg q
);

always @(posedge clk, posedge async_reset)
    if (async_reset)
        q <= 1'b0;
    else
        q <= d;

endmodule

Working:

When async_reset is high, the output q is immediately forced to 0. When the reset is inactive, the input d is transferred to q on the rising edge of the clock.

The waveform was examined in GTKWave to verify the relationship between the clock, reset, input, and output signals.

Figure 1: Simulation waveform of the asynchronous-reset D flip-flop.

1.2 Asynchronous Set D Flip-Flop

An asynchronous set forces the output to logic 1 as soon as the set signal becomes active. Similar to asynchronous reset, it operates independently of the clock edge.

Verilog Code

module dff_async_set (
    input clk,
    input async_set,
    input d,
    output reg q
);

always @(posedge clk, posedge async_set)
    if (async_set)
        q <= 1'b1;
    else
        q <= d;

endmodule

Working

When async_set is active, the output q becomes 1 immediately. When the set signal is inactive, the input d is captured at the rising edge of the clock.

The simulation waveform was used to observe the asynchronous set behavior and normal data transfer.

Figure 2: Simulation waveform of the asynchronous-set D flip-flop.

1.3 Synchronous Reset D Flip-Flop

A synchronous reset works only at the active clock edge. Unlike an asynchronous reset, activating the reset signal alone does not immediately change the output.
module dff_syncres (
    input clk,
    input sync_reset,
    input d,
    output reg q
);

always @(posedge clk)
    if (sync_reset)
        q <= 1'b0;
    else
        q <= d;

endmodule
Working

When sync_reset is high at the rising edge of the clock, the output q is set to 0. Otherwise, the input d is transferred to the output at the clock edge.

The simulation was used to verify that the reset affects the output only in synchronization with the clock.

Figure 3: Simulation waveform of the synchronous-reset D flip-flop.

⸻

1.4 Flip-Flop Synthesis Using Yosys

After verifying the flip-flop designs through simulation, the RTL was synthesized using Yosys. Synthesis converts the behavioral Verilog description into a hardware representation that can be implemented using standard cells.

The SKY130 standard-cell library was used for technology mapping.

 yosys
read_liberty -lib /address/to/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog dff_asyncres.v
synth -top dff_asyncres
dfflibmap -liberty /address/to/sky130_fd_sc_hd__tt_025C_1v80.lib
abc -liberty /address/to/sky130_fd_sc_hd__tt_025C_1v80.lib
show
The synthesized design was then viewed using the Yosys graphical representation.

Figure 4: Synthesized gate-level representation of the flip-flop design.

⸻

2. Logic Optimization Using Yosys

An important part of synthesis is optimization. Yosys can identify simple arithmetic operations and transform them into more efficient hardware structures while maintaining the same functionality.

To understand this process, constant multiplication examples were studied.

⸻

2.1 Constant Multiplication by 2

The first experiment used a 3-bit input and multiplied it by the constant value 2.

Verilog Code:

module mul2 (
    input [2:0] a,
    output [3:0] y
);

assign y = a * 2;

endmodule

The expression a * 2 represents multiplication by a constant. During synthesis, Yosys analyzes the operation and produces an optimized hardware implementation instead of treating it as a general-purpose multiplier.
yosys
read_verilog mul2.v
prep -top mul2
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mul2_net.v
gvim mul2_net.v
The synthesized circuit was viewed using the Yosys show command.

Figure 5: Synthesized representation of the mul2 design after optimization.

⸻

2.2 Constant Multiplication by 9

The second experiment used a constant multiplication by 9.

module mult8 (
    input [2:0] a,
    output [5:0] y
);

assign y = a * 9;

endmodule
Here, the input a is multiplied by 9. Yosys analyzes the arithmetic expression and generates an optimized hardware structure during synthesis.
yosys
read_verilog mult8.v
prep -top mult8
abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
write_verilog -noattr mult8_net.v
gvim mult8_net.v
The resulting schematic was examined to understand how the original arithmetic operation was represented after synthesis.

Figure 6: Synthesized representation of the mult8 design after optimization.

⸻

2.3 Generated Synthesized Netlist

After synthesis, Yosys can generate a new Verilog file containing the synthesized version of the RTL design. This file is called a netlist and represents the hardware after synthesis and optimization.

For the two multiplication examples:

write_verilog -noattr mul2_net.v
write_verilog -noattr mult8_net.v
The generated netlists can be inspected using:
gvim mul2_net.v
gvim mult8_net.v

Examining the synthesized Verilog helps in understanding how the original RTL description is transformed into a lower-level hardware representation.

Figure 7: Generated synthesized Verilog netlist obtained from Yosys.

⸻

Key Learnings:

Through Day 3, I learned how different flip-flop coding styles affect the behavior of sequential circuits. I also understood the difference between asynchronous and synchronous control signals.

The synthesis experiments showed how Yosys converts RTL into a hardware representation and performs optimization on arithmetic expressions. Viewing the synthesized schematics and netlists helped me understand the connection between Verilog RTL and the final hardware structure.
