**🔧 RTL Design & Synthesis Workshop**

Welcome to my **RTL Design, Logic Synthesis, and Physical Design Workshop** repository! 🚀

This repository documents my hands-on learning journey in Verilog RTL Design, Digital Design Verification, Logic Synthesis, RTL Optimization, Gate-Level Simulation, and Physical Design using open-source EDA tools.

Through practical experiments, I explore how a digital design moves from RTL code to a synthesized gate-level netlist and further into the physical design flow.

The main goal of this workshop is to understand the complete journey of digital hardware design:

**RTL Design → Simulation → Waveform Analysis → Logic Synthesis → Optimization → Gate-Level Simulation → Physical Design**

**📚 Workshop Contents
🟦 Day 1 — RTL Design Through Simulation**

Topics covered:

Introduction to Verilog RTL Design
Introduction to Icarus Verilog
Design and testbench concepts
RTL compilation and simulation
GTKWave waveform analysis
Basic RTL design experiments
Understanding simulation results

📂 Explore: Day_1/

**🟩 Day 2 — Timing Libraries & RTL Synthesis**

Topics covered:

Introduction to the SKY130 technology
Timing libraries and standard-cell libraries
Understanding technology library files
Hierarchical synthesis
Flattened synthesis
RTL-to-gate-level synthesis
Yosys synthesis flow
Technology mapping

📂 Explore: Day_2/

**🟨 Day 3 — Flip-Flop Coding & RTL Optimization**

Topics covered:

Flip-flop coding styles
Sequential RTL design
Synthesis comparison
RTL optimization techniques
Yosys synthesis analysis
Understanding synthesized logic
Gate-level hardware interpretation
Practical synthesis experiments

📂 Explore: Day_3/

**🟧 Day 4 — Logic Optimization & Design Efficiency**

Topics covered:

Introduction to logic optimization
Combinational logic optimization
Constant propagation
Boolean logic optimization
Sequential logic optimization
Constant flip-flop optimization
State optimization
Logic cloning
Retiming
Unused output optimization
RTL optimization using Yosys
SKY130 technology mapping
Analysis of optimized gate-level representations

📂 Explore: Day_4/

**🟥 Day 5 — Gate-Level Simulation & Synthesis Mismatches**

Topics covered:

Introduction to Gate-Level Simulation (GLS)
RTL simulation versus gate-level simulation
Synthesis-simulation mismatches
Missing sensitivity lists
Blocking and non-blocking assignments
Common issues with blocking assignments
Ternary-operator-based multiplexer design
RTL-to-gate-level netlist generation
SKY130 standard-cell Verilog models
Gate-Level Simulation using Icarus Verilog
Verification of Yosys-synthesized netlists
Waveform comparison and analysis

📂 Explore: Day_5/

**🟪 Day 6 — Synthesis Optimization & Efficient RTL Design**

Topics covered:

Introduction to synthesis optimization
Incomplete if statements
Latch inference in combinational logic
RTL schematic analysis using Yosys
RTL simulation and waveform analysis
Incomplete if-else statements
Incomplete and complete case statements
Partial case assignments and coding pitfalls
Multiplexer (MUX) verification
Demultiplexer (DEMUX) verification
Ripple carry adder design
Combinational logic optimization
Redundant logic removal
Resource optimization
RTL-to-gate-level synthesis
SKY130 standard-cell technology mapping
GTKWave waveform verification
Comparison of RTL and synthesized hardware

📂 Explore: Day_6/

**🏗️ Physical Design Modules**

The Physical Design modules extend my learning from RTL synthesis toward the implementation of digital circuits. Each module contains its own documentation and practical work.

**🔹 PD Module 1 — Introduction to Physical Design**

Focus areas:

Introduction to the physical design flow
Understanding the stages between synthesis and chip implementation
Exploring the physical design tool environment
Learning the basic concepts of digital implementation

📂 Explore: PD_Module1/

**🔹 PD Module 2 — Physical Design Flow**

Focus areas:

Understanding the physical design implementation process
Exploring design inputs and implementation stages
Studying the relationship between synthesis and physical design
Learning the fundamentals of physical implementation

📂 Explore: PD_Module2/

**🔹 PD Module 3 — CMOS Inverter**

Focus areas:

CMOS inverter fundamentals
Pull-up and pull-down networks
CMOS logic operation
Understanding inverter characteristics
Relating transistor-level design to digital circuit implementation

📂 Explore: PD_Module3/

**🔹 PD Module 4 — Timing Analysis**

Focus areas:

Introduction to timing analysis
Understanding timing constraints
Setup and hold timing concepts
Propagation delay and timing paths
Importance of timing analysis in digital design

📂 Explore: PD_Module4/

**🔹 PD Module 5 — Routing**

Focus areas:

Introduction to routing in physical design
Understanding signal interconnections
Placement-to-routing implementation concepts
Routing considerations in digital circuits
The role of routing in physical design closure

📂 Explore: PD_Module5/

Note: The module descriptions above are introductory summaries. Refer to the README and files inside each module for the exact experiments and topics covered.

**🔄 RTL-to-GLS — RTL to Gate-Level Simulation**

This section focuses on connecting RTL design, synthesis, and gate-level verification.

Key areas:

Writing and simulating RTL designs
Synthesizing RTL using Yosys
Generating a gate-level netlist
Mapping logic to standard cells
Using SKY130 standard-cell models
Compiling and simulating synthesized netlists
Comparing RTL and gate-level simulation results
Analyzing waveforms using GTKWave
Identifying synthesis-simulation mismatches

Typical workflow:

Write the RTL design in Verilog.
Create a testbench.
Simulate the RTL using Icarus Verilog.
Inspect simulation waveforms using GTKWave.
Synthesize the RTL using Yosys.
Generate the gate-level netlist.
Simulate the synthesized netlist using the appropriate cell models.
Compare RTL and gate-level behavior.

📂 Explore: RTL-to-GLS/

**🛠️ Tools & Technologies**

Tool / Technology	Purpose
Verilog HDL	RTL design and digital hardware description
Icarus Verilog	RTL and gate-level simulation
GTKWave	Waveform visualization and analysis
Yosys	Logic synthesis and RTL optimization
SKY130 PDK	Open-source process design kit and standard-cell technology
Standard-cell libraries	Technology mapping and cell-level implementation
Linux Terminal	Running EDA tools and design commands
Git	Version control
GitHub	Source-code hosting and documentation

**📂 Repository Structure**

RTL_Design_Journey/
│
├── Day_1/
│   ├── README.md
│   ├── images/
│   └── RTL design and simulation files
│
├── Day_2/
│   ├── README.md
│   ├── images/
│   └── Timing libraries and synthesis experiments
│
├── Day_3/
│   ├── README.md
│   ├── images/
│   └── Flip-flop coding and optimization experiments
│
├── Day_4/
│   ├── README.md
│   ├── images/
│   └── Logic optimization experiments
│
├── Day_5/
│   ├── README.md
│   ├── images/
│   └── Gate-level simulation experiments
│
├── Day_6/
│   ├── README.md
│   ├── images/
│   └── Synthesis optimization experiments
│
├── PD_Module1/
│   └── Physical Design learning materials
│
├── PD_Module2/
│   └── Physical Design learning materials
│
├── PD_Module3/
│   └── CMOS inverter experiments
│
├── PD_Module4/
│   └── Timing analysis experiments
│
├── PD_Module5/
│   └── Routing experiments
│
├── RTL-to-GLS/
│   └── RTL synthesis and gate-level simulation files
│
├── .gitattributes
├── README.md
└── Training_video.mp4


The directory tree is illustrative. Actual files and subdirectories may differ based on the contents of each module.

**🎯 Learning Outcomes:**

Through this hands-on workshop, I aim to develop a practical understanding of:

Writing synthesizable Verilog RTL code
Developing testbenches for functional verification
Compiling and simulating digital designs
Analyzing waveforms using GTKWave
Understanding sequential and combinational logic
Understanding standard-cell and timing libraries
Performing RTL synthesis using Yosys
Converting RTL into a gate-level netlist
Understanding technology mapping with SKY130
Applying combinational and sequential logic optimization
Identifying latch inference and incomplete assignments
Understanding synthesis-simulation mismatches
Performing gate-level simulation and netlist verification
Learning the fundamentals of physical design
Understanding CMOS inverter operation
Exploring timing analysis and routing concepts
Building a foundation in digital VLSI design and implementation

**🚀 Overall Design Flow**

        RTL Design
            |
            v
     Testbench Creation
            |
            v
      RTL Simulation
      (Icarus Verilog)
            |
            v
    Waveform Analysis
        (GTKWave)
            |
            v
      Logic Synthesis
         (Yosys)
            |
            v
    RTL Optimization
            |
            v
    Technology Mapping
         (SKY130)
            |
            v
   Gate-Level Netlist
            |
            v
   Gate-Level Simulation
            |
            v
  Functional Verification
            |
            v
      Physical Design
   Timing Analysis / Routing

**👩‍💻 Author**

**Name:** B. Sruthi
**University:** Anurag University
**Branch:** Electronics and Communication Engineering (ECE)

**🌱 My Learning Journey**

My learning approach is based on understanding concepts through practical implementation and analysis.

**Learn the concept → Write the RTL → Simulate → Analyze the waveform → Synthesize → Optimize → Verify → Explore Physical Design → Document**

This repository represents my ongoing journey into RTL Design, Digital Verification, Logic Synthesis, and VLSI Physical Design.

I believe that hands-on experimentation, systematic debugging, and understanding the hardware behind the code are essential to becoming a skilled VLSI design engineer.

Thanks for visiting my repository! ⭐
