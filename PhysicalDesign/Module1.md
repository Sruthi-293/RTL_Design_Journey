 PD Module 1 – Physical Design

📌 Project Overview

Physical Design is the process of converting a synthesized digital circuit into a physical chip layout. It includes floorplanning, power planning, placement, clock tree synthesis, routing, timing analysis, and physical verification.

In this module, I explored the ASIC physical-design environment using open-source EDA tools and the SKY130 technology.


🎯 Objectives
.Understand the ASIC Physical Design flow.
.Learn floorplanning and power planning.
.Study placement and CTS.
.Understand routing and antenna effects.
.Explore STA and parasitic extraction.
.Learn DRC and LVS concepts.
.Understand OpenLane, OpenROAD, and SKY130.
.Analyze important physical-design metrics.


🛠️ Tools & Technologies
Tool     	Purpose
OpenLane	Automated ASIC implementation flow
OpenROAD	Physical implementation
Yosys    	Logic synthesis
OpenSTA  	Timing analysis
Magic	    DRC
Netgen	  LVS
KLayout	  Layout visualization
SKY130	  Process Design Kit

🔄 Physical Design Flow

The overall implementation follows:

RTL
 ↓
Synthesis
 ↓
Floorplanning
 ↓
Power Planning
 ↓
Placement
 ↓
CTS
 ↓
Routing
 ↓
Parasitic Extraction
 ↓
STA
 ↓
Antenna Check
 ↓
DRC / LVS
 ↓
GDSII

1️⃣ Floorplanning 📐

Floorplanning is the first major stage of Physical Design. It decides the size, shape, and basic organization of the chip. The core area, die area, I/O locations, and space available for standard cells are planned during this stage.

A good floorplan is important because it affects later stages such as placement, routing, timing, and power distribution.

<img width="1280" height="590" alt="WhatsApp Image 2026-09-06 at 7 31 57 PM" src="https://github.com/user-attachments/assets/47cfa2b3-f6c8-4cc8-9f92-c85341ff23d6" />


Figure: Floorplan view showing the physical organization of the design.

Important parameters include FP_CORE_UTIL, FP_ASPECT_RATIO, FP_SIZING, and I/O-related settings. Proper selection of these parameters helps achieve better area utilization and routing efficiency.

2️⃣ Power Planning ⚡

Power planning establishes the Power Distribution Network (PDN) required to supply power to the entire design. The network distributes VDD and VSS from the power sources to the standard cells.

<img width="1280" height="590" alt="WhatsApp Image 2026-09-06 at 7 34 03 PM" src="https://github.com/user-attachments/assets/863090ea-2df5-4798-b8d4-3d653db89c3b" />

Figure: Power distribution structure used to provide VDD and VSS across the design.

A reliable PDN helps maintain stable power delivery and reduces problems caused by voltage drop and uneven power distribution. It is therefore an important part of achieving a reliable physical implementation.

3️⃣ Placement 📍

Placement determines the physical position of standard cells inside the core area defined during floorplanning. The cells are arranged while considering wirelength, timing, congestion, and available space.

<img width="1280" height="590" alt="WhatsApp Image 2026-09-06 at 7 34 56 PM" src="https://github.com/user-attachments/assets/db4cb6cd-34da-4ad6-b37b-1f1c38ca6c5d" />

Figure: Standard cells positioned within the core area during the placement stage.

Placement usually involves global placement, optimization, and detailed placement. The objective is to obtain a legal and efficient arrangement that makes subsequent routing easier.

4️⃣ Clock Tree Synthesis 🌳

Clock Tree Synthesis (CTS) creates a clock distribution network between the clock source and sequential elements. Since the clock must reach different parts of the design with controlled delay, CTS plays an important role in timing.

<img width="1280" height="590" alt="WhatsApp Image 2026-09-06 at 7 35 27 PM" src="https://github.com/user-attachments/assets/a23aa363-87d9-4f28-a980-b8cf4cd447d5" />

Figure: Clock distribution network generated during Clock Tree Synthesis.

CTS aims to control clock skew, latency, and transition time. Buffers and other clock cells may be introduced to create a balanced and reliable clock network.

5️⃣ Routing 🔗

Routing establishes the physical metal connections between the placed cells. It converts the logical connections in the netlist into actual paths through the available metal layers.

<img width="1280" height="590" alt="WhatsApp Image 2026-09-06 at 7 36 57 PM" src="https://github.com/user-attachments/assets/5f56e106-caf1-479d-876c-a775e6291615" />

Figure: Routed physical design showing metal interconnections between cells.

Routing consists mainly of global routing and detailed routing. Global routing determines suitable paths, while detailed routing creates the final connections while following the technology's design rules.

6️⃣ Antenna Rule Checking 🛡️

The antenna effect occurs during semiconductor manufacturing when charge accumulates on metal structures connected to transistor gates. Excessive charge can potentially damage the gate oxide.

<img width="1280" height="590" alt="WhatsApp Image 2026-09-06 at 7 46 39 PM" src="https://github.com/user-attachments/assets/a772b412-38e4-40a2-a9d4-46c4c06c1ba5" />

Figure: Antenna-rule checking performed on the routed design.

Antenna checking identifies structures that may cause fabrication-related problems. These checks are especially important after routing because the final metal geometry is available at this stage.

7️⃣ Antenna Violation Repair 🔧

If antenna violations are detected, the design needs to be modified to remove them. Repair techniques can include routing changes or the insertion of suitable antenna protection cells.

<img width="1280" height="590" alt="WhatsApp Image 2026-09-06 at 7 47 13 PM" src="https://github.com/user-attachments/assets/ce6e7c81-af71-4dfe-9009-52ab998345f7" />

Figure: Physical-design result after applying an antenna-violation repair technique.

After applying the repair, the design is checked again to confirm that the violation has been removed without creating new physical problems.

8️⃣ Static Timing Analysis ⏱️

Static Timing Analysis (STA) checks whether the design can operate within its specified timing constraints. It analyzes the timing paths between different points in the circuit.

<img width="1179" height="563" alt="WhatsApp Image 2026-09-06 at 7 49 27 PM" src="https://github.com/user-attachments/assets/29de08e8-c932-476c-8cb6-ef65a223ea90" />

Figure: Timing analysis results used to evaluate the performance of the implemented design.

Important timing parameters include setup, hold, clock latency, arrival time, required time, and slack. Positive slack generally indicates that a timing requirement is satisfied, while negative slack indicates a violation.

9️⃣ Parasitic Extraction 📊

Physical wires introduce parasitic resistance and capacitance into the circuit. These parasitic effects can influence signal delay and therefore need to be considered in post-route timing analysis.

The extracted information can be stored in SPEF (Standard Parasitic Exchange Format). This data can then be used by timing-analysis tools to obtain more realistic post-route timing results.

After routing, the physical interconnects introduce parasitic resistance and capacitance.

These parasitic effects are extracted from the routed design and represented using a Standard Parasitic Exchange Format (SPEF) file.

The extracted parasitic information is used during post-route timing analysis to obtain more realistic timing results.

Routed Design
     ↓
Parasitic Extraction
     ↓
SPEF
     ↓
OpenSTA
     ↓
Post-route Timing Analysis


🔟 Logic Equivalence Check 🔍

Logic Equivalence Checking (LEC) verifies that the implemented netlist maintains the same logical functionality as the reference design.

This check is useful because optimization and physical implementation can modify the structure of the netlist. LEC ensures that these changes have not altered the intended functionality.

Physical design stages such as optimization and Clock Tree Synthesis can modify the netlist.

LEC compares the reference design with the modified implementation to ensure functional equivalence.

Reference Netlist
       |
       |  LEC
       |
Implemented Netlist
       ↓
Functional Equivalence


1️⃣1️⃣ Physical Verification 🧪

Physical verification ensures that the final layout satisfies the required manufacturing and connectivity rules.

<img width="1179" height="537" alt="WhatsApp Image 2026-09-06 at 9 34 56 PM" src="https://github.com/user-attachments/assets/85404411-67c7-4e12-bfea-8f7afb0534e4" />

Figure: Physical verification results for the implemented layout.

DRC (Design Rule Check) verifies physical rules such as metal width, spacing, and via requirements. LVS (Layout Versus Schematic) checks whether the connectivity extracted from the layout matches the intended netlist.
A successful LVS indicates that the physical implementation represents the intended circuit correctly.

1️⃣2️⃣ OpenLane Design Exploration 📈

OpenLane can be used to experiment with different physical-design configurations. Parameters such as core utilization and aspect ratio can be changed to observe their effect on implementation quality.

<img width="1179" height="512" alt="WhatsApp Image 2026-09-06 at 9 36 52 PM" src="https://github.com/user-attachments/assets/7de083a8-6ab8-4fda-860e-46705ef03859" />

Figure: OpenLane environment used to explore different implementation configurations.

The results can be compared using metrics such as area, utilization, timing, cell density, and routing congestion. This helps identify configurations that provide a better overall design balance.

1️⃣3️⃣ OpenLane ASIC Flow 🚀

OpenLane provides an automated flow for implementing a digital design from RTL toward the final physical layout. It coordinates multiple stages and tools involved in ASIC implementation.

<img width="1179" height="486" alt="WhatsApp Image 2026-09-06 at 9 38 33 PM" src="https://github.com/user-attachments/assets/b053ad51-cdc5-46f5-92a7-cb6f64452e59" />


Figure: OpenLane-based flow used for ASIC physical implementation.

The major stages include synthesis, floorplanning, placement, CTS, routing, parasitic extraction, timing analysis, and physical verification. Automation makes the flow easier to reproduce and experiment with.

1️⃣4️⃣ OpenLane and OpenROAD 🛠️

OpenLane manages the overall ASIC implementation process, while OpenROAD performs many of the major physical-design operations.

OpenROAD provides capabilities for:

.Floorplanning
.Power planning
.Placement
.Optimization
.Clock Tree Synthesis
.Routing
.Physical implementation

OpenROAD is involved in operations such as floorplanning, placement, optimization, CTS, and routing. The integration of these tools provides an open-source environment for learning ASIC Physical Design.

1️⃣5️⃣ SKY130 PDK 🧬

The SKY130 PDK provides the technology-specific information required to implement a design using the SkyWater 130 nm process.

The PDK provides the technology-specific information required by the ASIC implementation tools, including:

.Standard-cell libraries
.Technology LEF files
.Liberty timing libraries
.Design rules
.Layer information
.Physical abstracts


<img width="1179" height="540" alt="WhatsApp Image 2026-09-06 at 9 43 57 PM" src="https://github.com/user-attachments/assets/251c66c8-b307-4131-ba7e-896050a48c1d" />

Figure: SKY130 technology files and libraries used by the Physical Design flow.

The PDK includes standard-cell libraries, LEF files, Liberty timing libraries, design rules, and information about physical layers. These resources allow EDA tools to perform technology-aware implementation.

1️⃣6️⃣ OpenLane Design Configuration ⚙️

OpenLane uses configuration parameters to control how the design passes through different implementation stages.

Important configuration categories include:

.Design and source configuration
.Clock configuration
.Floorplan configuration
.Placement configuration
.Routing configuration
.Timing constraints
.Power planning parameters

Configuration settings can define the design source, clock information, floorplan parameters, placement options, routing settings, and timing constraints. Proper configuration helps produce consistent and reproducible results.

1️⃣7️⃣ Floorplan Configuration Parameters 📐

Floorplan parameters control important aspects of the physical organization of the design.

Parameter	              Description
FP_CORE_UTIL	      Controls target core utilization
FP_ASPECT_RATIO	    Defines the core shape
FP_SIZING         	Controls floorplan sizing
FP_IO_MODE	        Controls I/O arrangement
FP_IO_HMETAL       	Horizontal I/O metal
FP_IO_VMETAL      	Vertical I/O metal
FP_PDN_*	          Power-network settings

1️⃣8️⃣ Design for Test (DFT) 🧪

Design for Testability improves the ability to test an integrated circuit after manufacturing. One common approach is scan-based testing.

Scan-based testing is commonly used to provide controllability and observability of internal sequential elements.

DFT is considered as part of the ASIC implementation flow before final verification.

<img width="1179" height="528" alt="WhatsApp Image 2026-09-06 at 9 48 37 PM" src="https://github.com/user-attachments/assets/d46d0c87-e62f-437d-8045-d54fa9666199" />

Figure: Design-for-test concept used to improve circuit testability.

DFT improves controllability and observability of internal circuit elements. It helps increase fault-detection capability and supports effective manufacturing testing.

1️⃣9️⃣ Physical Implementation 🏗️

Physical implementation combines the major stages required to transform the synthesized design into a physical layout.

The main operations include:

.Floorplanning
.Power planning
.Placement
.Clock Tree Synthesis
.Routing
.Physical optimization

The major steps include floorplanning, power planning, placement, CTS, routing, and optimization. Each stage contributes to the final area, timing, congestion, and reliability of the design.

2️⃣0️⃣ Project Execution 💻

The physical-design project is executed using RTL sources, configuration files, technology libraries, and required constraints.

The generated run directory generally contains results, reports, logs, and temporary files. These outputs help analyze the progress and quality of each implementation run.

The flow was run through the OpenLane flow script, which automatically invokes the required tools for each stage of physical implementation.

The execution generates intermediate files, logs, reports, and final physical design outputs.

A typical OpenLane run contains:

Design
 ├── src/
 ├── config.tcl
 └── runs/
      └── <run_directory>/
           ├── results/
           ├── reports/
           ├── logs/
           └── tmp/

           
2️⃣1️⃣ Physical Design Results 📊

After completing the implementation flow, different metrics are examined to evaluate the quality of the design.

The important implementation metrics include:

Metric	            Purpose
Area      	  Measures the physical size of the implemented design
Cell Count	  Number of standard cells used
Utilization	  Percentage of the core occupied by cells
Timing	      Determines whether timing constraints are satisfied
Slack       	Indicates the available timing margin
Routing     	Confirms successful physical connectivity
DRC	          Checks manufacturing design rules
LVS	          Checks layout-to-netlist connectivity
Antenna     	Checks fabrication-related antenna violations

These metrics are used to evaluate the quality and correctness of the final physical implementation.

Important metrics include area, cell count, utilization, timing, slack, routing completion, DRC status, LVS status, and antenna results. These values help compare different implementation runs.

2️⃣2️⃣ Verification Summary 🔍

The final design undergoes several verification checks to ensure that it is logically correct, physically valid, and timing compliant.

Verification	       Objective
STA	              Verify timing constraints
LEC	              Verify logical equivalence
DRC	              Verify physical design rules
LVS             	Verify layout connectivity
Antenna Check	    Identify antenna rule violations
The major checks include STA, LEC, DRC, LVS, and antenna verification. Each check examines a different aspect of the design and contributes to overall confidence in the final layout.

2️⃣3️⃣ Design Space Exploration 🔄

Design Space Exploration involves changing implementation parameters and comparing the resulting physical-design metrics.

<img width="1179" height="481" alt="WhatsApp Image 2026-09-06 at 9 57 19 PM" src="https://github.com/user-attachments/assets/ec61ca96-1119-4a2b-a7a3-97015f30ccef" />

Figure: Comparison of different physical-design configurations.

Changing parameters can affect area, utilization, timing, wirelength, and routing congestion. Exploring these trade-offs helps identify a configuration that provides a suitable balance between performance and physical resources.

2️⃣4️⃣ OpenLane Regression Testing 🔁

Regression testing checks whether modifications to the design, configuration, or flow produce unexpected failures.

<img width="1179" height="537" alt="WhatsApp Image 2026-09-06 at 9 58 29 PM" src="https://github.com/user-attachments/assets/4eeeebbe-7211-4de8-8dda-ca7be740d811" />

Figure: Regression-testing results used to verify the consistency of the implementation flow.

Regular regression testing improves reproducibility, reliability, and flow stability, especially when multiple experiments are performed.

2️⃣5️⃣ Final Physical Design Flow 🏁

The complete Physical Design process can be summarized as:

RTL
 ↓
Synthesis
 ↓
Floorplanning
 ↓
Power Planning
 ↓
Placement
 ↓
Clock Tree Synthesis
 ↓
Routing
 ↓
Parasitic Extraction
 ↓
Static Timing Analysis
 ↓
Antenna Check
 ↓
DRC / LVS
 ↓
Final Layout
 ↓
GDSII

This flow demonstrates the transformation of a logical RTL design into a physical and manufacturable chip layout.

2️⃣6️⃣Terminal Execution and Command Evidence

The following terminal screenshots provide evidence of the commands executed during the physical design setup and OpenLane flow.


26.1 PDK Directory and Library Setup

<img width="1179" height="580" alt="WhatsApp Image 2026-09-06 at 10 03 30 PM" src="https://github.com/user-attachments/assets/b3c53183-ddb6-4927-b143-0deba34e3a86" />


26.2 Sky130 Standard Cell Library Verification

<img width="1179" height="582" alt="WhatsApp Image 2026-09-06 at 10 05 26 PM" src="https://github.com/user-attachments/assets/733374d2-f870-4c8e-8dbf-d34ef364a05e" />


26.3 OpenLane Environment Setup

<img width="958" height="934" alt="WhatsApp Image 2026-09-06 at 5 50 58 PM" src="https://github.com/user-attachments/assets/2036ba41-2522-4a35-8cff-386d6d0d7c20" />


26.4 LEF and Library File Verification

<img width="958" height="934" alt="WhatsApp Image 2026-09-06 at 5 50 58 PM (1)" src="https://github.com/user-attachments/assets/7199d4e9-3132-4da7-a000-c93c82b9c2a8" />


26.5 OpenLane Flow Execution

<img width="958" height="934" alt="WhatsApp Image 2026-09-06 at 5 50 59 PM" src="https://github.com/user-attachments/assets/b452c5ee-6cd4-46d2-a1ba-ef27963c6e4b" />


26.6 OpenLane Configuration

<img width="958" height="934" alt="WhatsApp Image 2026-09-06 at 5 50 59 PM (1)" src="https://github.com/user-attachments/assets/ad82859b-318a-4afc-93f6-c636eaf3b0b9" />


26.7 Floorplan Configuration

<img width="958" height="934" alt="WhatsApp Image 2026-09-06 at 5 50 59 PM (2)" src="https://github.com/user-attachments/assets/a13a595c-cf47-4339-a2b3-251abf91bb35" />


🧠 Key Learnings

Floorplanning: Learned how core utilization, aspect ratio, die/core dimensions, and I/O placement influence the overall chip area and routability.
Power Planning: Understood the importance of creating a reliable VDD/VSS power distribution network (PDN) to supply power uniformly to standard cells and reduce voltage-drop issues.

Placement: Learned how standard cells are positioned within the core and how placement optimization helps reduce congestion, wirelength, and timing problems.
Clock Tree Synthesis (CTS): Understood how a balanced clock network is created using buffers to control clock skew, latency, and transition, ensuring reliable sequential operation.

Routing: Learned the difference between global routing and detailed routing, and how physical connections are created while following technology design rules.
Antenna Checking & Repair: Understood how long metal connections can create antenna violations during fabrication and how techniques such as diode insertion can help prevent gate-oxide damage.

Static Timing Analysis (STA): Learned how setup time, hold time, clock latency, arrival time, required time, and slack are analyzed to verify whether timing constraints are satisfied.

Parasitic Extraction: Understood that routed wires introduce resistance and capacitance, which are extracted as parasitic information and used for accurate post-route timing analysis.

Physical Verification: Learned the purpose of DRC and LVS—DRC checks whether layout follows manufacturing rules, while LVS verifies that the layout connectivity matches the intended circuit.

Open-Source EDA Flow: Gained practical understanding of tools such as OpenLane, OpenROAD, Yosys, OpenSTA, Magic, and Netgen and their roles in the RTL-to-GDSII flow.

SKY130 PDK: Learned how the SkyWater SKY130 PDK provides technology information, standard-cell libraries, timing data, and physical design rules required for implementation.

Design Space Exploration: Understood that changing physical-design parameters can affect area, utilization, timing, congestion, and overall design quality, making parameter selection an important part of optimization.


📝 Conclusion

PD Module 1 provided a practical introduction to the complete ASIC Physical Design methodology, starting from floorplanning and continuing through power planning, placement, clock tree synthesis, routing, timing analysis, and physical verification.

Through this module, I understood how a synthesized design is gradually converted into a physically organized and manufacturable layout. Each stage has its own purpose, but all the stages are closely connected. For example, floorplan decisions can influence placement and routing, while routing can affect parasitic delay and final timing.

The module also provided an understanding of important verification activities such as STA, antenna checking, DRC, LVS, and logic equivalence checking. These checks are essential for ensuring that the final implementation is logically correct, physically valid, and capable of meeting its required constraints.

Working with OpenLane, OpenROAD, SKY130, OpenSTA, Magic, Netgen, and KLayout also helped connect theoretical Physical Design concepts with practical EDA workflows.

🚀 Final Takeaway

RTL defines what the circuit should do; Physical Design determines how that circuit is physically realized on silicon.
