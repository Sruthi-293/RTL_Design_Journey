**📘 Physical Design – Module 2**

🚀 Module Overview

Physical Design is the stage where a synthesized digital circuit is converted into a practical physical arrangement suitable for fabrication. In this module, the focus is on understanding how the logical design is transformed into a physical layout using the OpenLane flow.

Along with the Physical Design flow, this module introduces an important concept in VLSI: standard-cell library characterization. A standard cell is not only a physical layout; its timing, power, transition, and electrical behavior must also be represented in a form that EDA tools can understand.

The major concepts covered in this module include:

1. OpenLane configuration

2. Floorplanning and core/die definition

3. Pre-placed cells

4. Power planning

5. Standard-cell placement

6. Placement blockages

7. Placement optimization

8. Routing

9. Standard-cell design flow

10. Library characterization

11.Timing characterization

12.Timing thresholds

13.Propagation delay

14.Transition time

15.Noise margin

16.NLDM and CCS models

This module helped connect the theoretical concepts of Physical Design with the actual information required by EDA tools.

**🎯 Objectives:**

Understand how OpenLane parameters control different stages of the Physical Design flow.

Study the fundamentals of floorplanning, including core area, die area, utilization, and aspect ratio.

Understand the purpose of pre-placed cells and why some blocks need fixed physical locations.

Learn how a Power Distribution Network provides reliable VDD and VSS connections throughout the design.

Understand how standard cells are mapped and positioned during placement.

Study placement blockages and their importance around reserved or critical regions.

Learn how placement optimization improves wirelength, timing, congestion, and signal quality.

Understand the purpose of routing and how physical connections are created between placed cells.

Explore the complete design flow of a standard cell from circuit design to characterization.

Understand how library characterization provides timing, power, and electrical information to EDA tools.

Study timing thresholds, propagation delay, transition time, and noise margins.

Understand the difference between NLDM and CCS timing models.

🗺️ Module Roadmap

        RTL / Netlist
             │
             ▼
      ⚙️ OpenLane Setup
             │
             ▼
       📐 Floorplanning
             │
             ├── Core / Die
             ├── Utilization
             └── Pre-placed Cells
             │
             ▼
       ⚡ Power Planning
             │
             ▼
       📍 Cell Placement
             │
             ├── Blockages
             └── Optimization
             │
             ▼
          🔗 Routing
             │
             ▼
       📚 Standard Cell Characterization
             │
             ├── Timing
             ├── Delay
             ├── Transition
             └── Noise
             │
             ▼
        📊 NLDM / CCS

1️⃣ From Logical Design to Physical Design

A digital circuit initially exists as a logical representation containing gates, flip-flops, connections, and functional blocks. During Physical Design, these logical elements must be transformed into actual physical locations and interconnections.

The complete design can contain multiple data paths, clock networks, functional blocks, and I/O connections. Physical Design determines how these elements are arranged while considering area, timing, power, and routing resources.

📸 Complete Design Representation

<img width="1280" height="590" alt="WhatsApp Image 2026-09-07 at 7 31 57 PM (9)" src="https://github.com/user-attachments/assets/1b4f038e-66e3-4632-a8de-ba9159c8293a" />

Figure: Complete logical design showing multiple functional paths, flip-flops, logic elements, clock connections, and I/O signals.

💡 Key Idea

The logical design describes what the circuit does, while Physical Design determines where the circuit elements are placed and how they are physically connected.

This transition from logical connectivity to physical organization is one of the most important ideas in ASIC implementation.

2️⃣ Breaking the Design into Physical Blocks

Large designs are often easier to manage when they are divided into smaller functional blocks or modules. Important blocks can be treated as separate physical regions so that their locations and interfaces can be controlled more effectively.

Pre-placed or fixed blocks may include memories, special IPs, clock-related structures, or other large and critical components. Defining their locations early gives the remaining placement process a clear physical framework.

📸 Block Partitioning and Pre-placed Cells

<img width="1280" height="590" alt="WhatsApp Image 2026-09-07 at 7 31 56 PM (4)" src="https://github.com/user-attachments/assets/b2f7e7df-9efe-495d-b07d-66578fa70ac5" />

Figure: Logical circuitry divided into physical blocks, illustrating how important regions can be separated and assigned predefined locations.


This concept becomes particularly important when dealing with large macros or fixed IP blocks.

3️⃣ Power Distribution in the Physical Layout ⚡

After defining the physical organization, the design must have a reliable method of delivering power to all cells.

A Physical Design therefore includes a Power Distribution Network (PDN) that distributes the supply voltage and ground through the chip. The network contains VDD and VSS connections that reach different regions of the design.

Power distribution should be planned carefully because large switching activity can cause voltage variations and unwanted supply disturbances.

📸 Power Distribution Structure

<img width="1280" height="590" alt="WhatsApp Image 2026-09-07 at 7 31 57 PM (8)" src="https://github.com/user-attachments/assets/bcaa0da7-d7a6-4d0c-8133-0e6fd244757c" />

Figure: Power and ground connections distributed across multiple physical cell regions.

This provides the foundation for the later Power Planning stage in OpenLane.

4️⃣ Pin Placement and I/O Organization 📍

Input and output pins provide the interface between the internal circuit and the outside world. Their physical locations have a direct effect on routing and the overall shape of the design.

During floorplanning, pins can be positioned around the die boundary according to design requirements. Clock signals, input signals, output signals, and other important interfaces should be arranged in a way that supports efficient routing.

📸 Pin Placement

<img width="1280" height="590" alt="WhatsApp Image 2026-09-07 at 7 31 57 PM (10)" src="https://github.com/user-attachments/assets/4c34a73c-0ee6-438c-8827-caf483c2be8c" />

Figure: Pin placement around the die boundary showing input, output, clock, core, die, VDD, and VSS regions.

🎯 Why Pin Placement Matters

Good pin placement can help:

Reduce unnecessary wirelength
Simplify routing
Avoid routing congestion
Improve access to internal blocks
Maintain an organized I/O structure

The image also illustrates the distinction between the core and the die, which becomes important during floorplanning.

5️⃣ Logical Cell Placement Blockage 🚧

During automatic placement, the tool should not be allowed to place standard cells everywhere.

Some regions need to remain free because they may be reserved for macros, power structures, special routing, or other physical requirements. These restricted areas are represented using placement blockages.

A blockage therefore acts as a physical constraint that guides the placement engine.

📸 Placement Blockage

<img width="1280" height="590" alt="WhatsApp Image 2026-09-07 at 7 31 57 PM (11)" src="https://github.com/user-attachments/assets/7ee35c04-7c84-40ad-bdb5-e04ae17a76f9" />

Figure: Placement grid showing restricted regions where standard cells are prevented from being automatically placed.

6️⃣ OpenLane Configuration ⚙️

Once the basic Physical Design concepts are understood, the next step is to configure the OpenLane flow.

OpenLane uses configuration parameters to understand the design being implemented and to control different stages of the RTL-to-GDSII process.

The configuration generally specifies information such as:

Design name

RTL / Verilog source files

Clock port

Clock period

Clock network

Standard-cell library

Synthesis options

Floorplan parameters

Placement parameters

Routing parameters

Timing-related settings

The configuration acts as the control panel of the implementation flow. By changing these parameters, different physical-design experiments can be performed and their effects on area, timing, utilization, and routability can be studied.

📸 OpenLane Configuration

<img width="1068" height="643" alt="WhatsApp Image 2026-09-07 at 9 23 36 PM" src="https://github.com/user-attachments/assets/9bbbb61b-fbb2-4319-a032-598edc558ec2" />

Figure: OpenLane configuration containing the design and implementation parameters.


<img width="947" height="572" alt="WhatsApp Image 2026-09-07 at 9 25 49 PM" src="https://github.com/user-attachments/assets/70644296-bc7f-4c48-8fdb-60659ea5e958" />

Figure: Additional OpenLane settings used to control the physical implementation flow.

7️⃣ Physical Design Flow 🔄

After configuring OpenLane, the design moves through a sequence of physical implementation stages. Each stage has a specific purpose, and the output of one stage becomes the input for the next.

The overall flow can be represented as:

RTL / Netlist
     ↓
⚙️ OpenLane Configuration
     ↓
📐 Floorplanning
     ↓
⚡ Power Planning
     ↓
📍 Placement
     ↓
🕒 Clock Tree Synthesis
     ↓
🔗 Routing
     ↓
🧪 Physical Verification
     ↓
📦 GDSII Generation

The main objective is to achieve a layout that satisfies area, timing, power, congestion, and manufacturing requirements.

🎯 Design Quality Goals
 Parameter	Objective
 Area	Use silicon efficiently
 Timing	Meet required timing constraints
 Power	Maintain efficient power usage
 Congestion	Avoid excessive routing density
 Routability	Complete all required connections

8️⃣ Floorplanning 📐

Floorplanning is the first major physical implementation step after configuration. It establishes the basic physical boundaries of the design and determines how much space is available for cells and other blocks.

The two important regions are:

Die: Complete physical boundary of the chip.
Core: Inner region where standard cells are primarily placed.

Several parameters influence the floorplan, including:

Core utilization
Aspect ratio
Core dimensions
Die dimensions
I/O arrangement
Macro locations
Power distribution requirements

A balanced floorplan provides sufficient space for placement and routing while avoiding unnecessary silicon area.

📐 Floorplanning Views

<img width="919" height="563" alt="WhatsApp Image 2026-09-07 at 9 51 17 PM" src="https://github.com/user-attachments/assets/0f43b294-53ee-4846-b1c9-c1b8f02b355e" />

Figure: Initial floorplan showing the physical boundaries of the design.


<img width="922" height="563" alt="WhatsApp Image 2026-09-07 at 9 52 31 PM" src="https://github.com/user-attachments/assets/37a7dffe-8da1-4ea7-95e0-0e401186e93a" />

Figure: Core and die regions used to define the usable implementation area.


<img width="900" height="537" alt="WhatsApp Image 2026-09-07 at 9 55 12 PM" src="https://github.com/user-attachments/assets/656cfc93-31f2-4b16-b618-076bd93e1159" />

Figure: Floorplan arrangement showing the organization of the design area.


<img width="929" height="555" alt="WhatsApp Image 2026-09-07 at 9 55 39 PM" src="https://github.com/user-attachments/assets/89498b85-5398-44c9-86ec-d07062a955d8" />

Figure: Physical floorplan view used to examine the available placement region.


<img width="930" height="568" alt="WhatsApp Image 2026-09-07 at 9 57 58 PM" src="https://github.com/user-attachments/assets/f253d56f-c11c-49a3-b97f-895b003d90a8" />

Figure: Floorplanning result showing the physical organization before placement.

💡 Design Insight

Floorplanning creates the framework for everything that follows. A poor floorplan can lead to high congestion, long interconnects, timing problems, and difficult routing later.

9️⃣ Pre-placed Cells 📍

Some components cannot be left entirely to the automatic placement engine. Large or important blocks may need their physical positions to be defined before normal standard-cell placement begins.

Examples include:

🧠 Memory blocks
🧩 Large IP blocks
🕒 Clock-related structures
🔀 Large multiplexing structures
⭐ Critical physical blocks

Pre-placing these elements creates a stable physical structure around which the remaining cells can be arranged.

📸 Pre-placed Cell View

<img width="889" height="513" alt="WhatsApp Image 2026-09-07 at 10 03 50 PM" src="https://github.com/user-attachments/assets/b0ec080a-3f73-4562-9e74-aac2b4625021" />

Figure: Important physical blocks positioned at predefined locations before automatic standard-cell placement.

🔍 Observation

Pre-placement provides better control over the physical design because the placement engine can organize the remaining cells around these fixed regions.

🔟 Power Planning ⚡

Once the physical framework is established, the next requirement is reliable power delivery.

The Power Distribution Network (PDN) distributes power and ground from the chip-level supply network to the individual standard cells.

Important PDN elements include:

VDD
VSS
Power rings
Power straps
Standard-cell power rails
Power connections to different regions

The purpose is to maintain stable supply connections throughout the design and support reliable circuit operation.

⚡ Power Planning View

<img width="944" height="511" alt="WhatsApp Image 2026-09-07 at 10 06 37 PM" src="https://github.com/user-attachments/assets/cd7cca83-cc10-46f5-9ec5-7342864fcfa4" />

Figure: Power distribution network showing the physical delivery of supply and ground across the design.

💡 Design Insight

Power planning has to be considered together with placement and routing because the PDN consumes physical resources that could otherwise be used for signal connections.

1️⃣1️⃣ Placement 📍

After floorplanning and power planning, standard cells are assigned physical locations inside the core.

Placement converts the logical netlist into a physical arrangement of cells while attempting to achieve good:

Wirelength
Timing
Area utilization
Congestion
Routability
Connectivity

The placement process normally consists of an initial placement followed by optimization and detailed placement.

During this process, the tool estimates the effects of cell locations on interconnect length and capacitance and adjusts the arrangement accordingly.

📸 Placement Views

<img width="969" height="486" alt="WhatsApp Image 2026-09-07 at 10 07 44 PM" src="https://github.com/user-attachments/assets/6e93d6f9-b23b-48ca-9dd8-478811799f8b" />

Figure: Initial standard-cell placement inside the core region.


<img width="856" height="520" alt="WhatsApp Image 2026-09-07 at 10 08 13 PM" src="https://github.com/user-attachments/assets/9fb1ad4e-c3f5-45a4-ba54-d02c38a788c7" />

Figure: Placement view showing the distribution of standard cells across the design.


<img width="861" height="531" alt="WhatsApp Image 2026-09-07 at 10 08 29 PM" src="https://github.com/user-attachments/assets/70ccde18-e92d-4ebb-84fe-50649fc697b1" />

Figure: Intermediate placement arrangement used for physical optimization.


<img width="818" height="479" alt="WhatsApp Image 2026-09-07 at 10 08 57 PM" src="https://github.com/user-attachments/assets/7baae990-017e-4dd7-8015-ef28d5472866" />

Figure: Improved placement after physical optimization.


<img width="877" height="532" alt="WhatsApp Image 2026-09-07 at 10 09 27 PM" src="https://github.com/user-attachments/assets/b02b4cea-8f2e-4579-906e-d716846432f0" />

Figure: Final placement arrangement before moving toward clock and routing stages.

🎯 Placement Objective

The goal is not simply to minimize distance between cells. The placement must provide a good balance between timing, congestion, area, and future routing requirements.

1️⃣2️⃣ Logical Cell Placement Blockage 🚧

Placement blockages are regions where standard cells are restricted or completely prevented from being placed.

They are useful for protecting areas needed for:

Pre-placed macros
Memory blocks
Power structures
Reserved regions
Critical routing paths
Special physical structures

Blockages provide additional physical constraints to the placement engine and help maintain a controlled layout.

📸 Placement Blockage

<img width="900" height="530" alt="WhatsApp Image 2026-09-07 at 10 16 55 PM" src="https://github.com/user-attachments/assets/096c637e-5f75-4510-b40e-e22bb0707455" />

Figure: Restricted physical region where automatic standard-cell placement is not permitted.

🚧 Simple Understanding
Without Blockage
     ↓
Cells may occupy unwanted regions

With Blockage
     ↓
Reserved region is protected
     ↓
Better physical organization

1️⃣3️⃣ Placement Optimization 🔧

The first placement result may not provide the required timing or routing quality. Placement optimization is therefore used to improve the physical arrangement.

The tool can perform operations such as:

Moving cells
Resizing cells
Inserting buffers
Reducing wirelength
Reducing capacitance
Improving timing
Reducing congestion

Optimization is especially important for critical paths where physical distance and loading can significantly affect timing.

📸 Optimization Results

<img width="974" height="505" alt="WhatsApp Image 2026-09-07 at 10 21 38 PM" src="https://github.com/user-attachments/assets/ea334807-83e6-4110-a240-e6a0967054b6" />

Figure: Placement optimization performed to improve the physical arrangement of cells.

<img width="873" height="531" alt="WhatsApp Image 2026-09-07 at 10 21 54 PM" src="https://github.com/user-attachments/assets/c781e2ef-a875-488f-bdf0-a12d29febcf4" />

Figure: Optimized placement after improving timing, connectivity, and physical distribution.

⚖️ Optimization Trade-off

A change that improves timing may increase area or power. Therefore, optimization is a continuous trade-off between multiple physical-design objectives.

1️⃣4️⃣ Routing 🔗

After placement is completed, the tool creates physical connections between the placed cells.

Routing translates the logical nets into actual metal-layer paths while following manufacturing design rules.

It must establish connections between:

Standard cells
I/O pins
Clock networks
Other physical blocks
Power-related structures

Routing quality is strongly influenced by the earlier floorplan and placement decisions.

🔗 Routing Flow
Placed Cells
     ↓
Global Routing
     ↓
Detailed Routing
     ↓
Physical Connections
     ↓
Design-Rule Checks
💡 Key Point

A design can have correct logical connectivity but still face physical routing problems. Therefore, successful routing requires both connectivity correctness and physical manufacturability.

1️⃣5️⃣ Standard-Cell Design Flow 🏗️

Standard cells are reusable building blocks used throughout digital IC designs. Common examples include:

Inverters
Buffers
AND gates
OR gates
NAND gates
NOR gates
Flip-flops

Before a standard cell can be effectively used by EDA tools, it must go through circuit design, physical layout, verification, and characterization.

The general flow is:

📋 Specifications
       ↓
🔌 Circuit Design
       ↓
📐 Layout Design
       ↓
🧪 Verification
       ↓
📊 Characterization
       ↓
📚 Library Generation

The process uses information such as the PDK, SPICE models, DRC/LVS rules, and library specifications. The resulting library contains physical, timing, power, and functional information.

📸 Standard-Cell Flow

<img width="971" height="498" alt="WhatsApp Image 2026-09-07 at 10 26 45 PM" src="https://github.com/user-attachments/assets/130481f6-dc69-4902-b1e5-e0f96a65656d" />

Figure: Complete standard-cell development process from circuit creation to library generation.

1️⃣6️⃣ Library Characterization 📚

A standard-cell library needs accurate information about how each cell behaves under different operating conditions.

Library characterization is the process of measuring and modeling this behavior.

Important characteristics include:

Propagation delay
Input capacitance
Output capacitance
Signal transition
Power consumption
Timing behavior

This information is stored in library models and later used by EDA tools during synthesis, timing analysis, optimization, and implementation.

📸 Library Characterization

<img width="948" height="468" alt="WhatsApp Image 2026-09-07 at 10 28 03 PM" src="https://github.com/user-attachments/assets/d45be0ce-7f33-4070-ac0c-76f6579af54b" />

Figure: Characterization process used to obtain timing and electrical information for a standard cell.

🧠 Simple View
Standard Cell
     ↓
Apply Input Conditions
     ↓
Observe Output Response
     ↓
Measure Delay / Power / Slew
     ↓
Create Library Data

1️⃣7️⃣ Timing Characterization ⏱️

Timing characterization determines how a standard cell responds to changes at its input and how quickly those changes appear at its output.

The main quantities include:

Input transition
Output transition
Rise delay
Fall delay
Input capacitance
Output load

The cell is evaluated under different combinations of input and output conditions. The resulting measurements are then converted into timing information for library models.

📸 Timing Characterization

📸 INSERT YOUR TIMING CHARACTERIZATION IMAGE HERE

![Timing Characterization](your-timing-characterization.jpeg)

Figure: Input and output waveforms used to analyze the timing behavior of a standard cell.

1️⃣8️⃣ Timing Threshold Definitions 📐

Timing measurements require fixed voltage reference points so that delay and transition values can be measured consistently.

The commonly used thresholds are:

Timing Parameter	Value
slew_low_rise_thr	20%
slew_high_rise_thr	80%
slew_low_fall_thr	20%
slew_high_fall_thr	80%
in_rise_thr	50%
in_fall_thr	50%
out_rise_thr	50%
out_fall_thr	50%

The 20% and 80% levels are used for transition measurements, while the 50% reference is used for input/output delay measurement.

📸 Timing Thresholds

<img width="948" height="468" alt="WhatsApp Image 2026-09-07 at 10 28 03 PM" src="https://github.com/user-attachments/assets/ecad37d4-a2e9-4da4-8114-047b157ebebc" />

Figure: Voltage threshold levels used to measure signal transition and propagation delay.

1️⃣9️⃣ Propagation Delay ⏳

Propagation delay describes the time difference between a change occurring at the input and the corresponding change appearing at the output.

For timing characterization, the delay is measured using defined voltage threshold points.

Factors that can affect propagation delay include:

Input slew
Output load
Cell architecture
Drive strength
Interconnect capacitance

📸 Propagation Delay

<img width="964" height="537" alt="WhatsApp Image 2026-09-07 at 10 30 15 PM" src="https://github.com/user-attachments/assets/4e4e9ba1-f532-448c-89e7-c17a617e6962" />

Figure: Measurement of the time difference between input and output transitions.

⏱️ Simple Representation
Input Transition
      │
      │<---- Propagation Delay ---->│
      │                             │
      ▼                             ▼
Input Waveform                Output Waveform


2️⃣0️⃣ Transition Time / Slew 📈

Transition time, commonly called slew, describes how quickly a digital signal changes between logic levels.

For a rising waveform, the transition is measured from approximately 20% to 80% of the signal voltage.

For a falling waveform, the measurement is taken from 80% down to 20%.

Rise Slew → 20% to 80%

Fall Slew → 80% to 20%

A smaller transition time generally represents a sharper and faster signal edge.

📸 Transition Time

<img width="963" height="473" alt="WhatsApp Image 2026-09-07 at 10 31 19 PM" src="https://github.com/user-attachments/assets/376744c7-f462-4829-8e59-0ec7e6dea5ac" />

Figure: Rise and fall transition regions used to determine signal slew.

2️⃣1️⃣ Noise Margin 🛡️

Noise margin indicates how much unwanted voltage disturbance a digital circuit can tolerate while still correctly recognizing logic HIGH and LOW levels.

The two important quantities are:

NMH — Noise Margin High
NML — Noise Margin Low

A sufficient noise margin improves the reliability of digital circuits in the presence of electrical disturbances.

📸 Noise Margin

<img width="1138" height="668" alt="WhatsApp Image 2026-09-07 at 10 32 16 PM" src="https://github.com/user-attachments/assets/1e8b3c11-bb78-4310-9e66-ee04a4d4817a" />

Figure: High and low noise-margin regions illustrating the tolerance of a digital circuit to unwanted voltage variations.

🛡️ Why It Matters

Noise can arise from switching activity, coupling, supply fluctuations, and interconnect effects. A circuit with adequate noise margin is more resistant to such disturbances.

2️⃣2️⃣ NLDM vs CCS 📊

Timing models provide EDA tools with a way to represent the behavior of standard cells.

Two important models are NLDM and CCS.

🔹 NLDM — Non-Linear Delay Model

NLDM represents cell timing using lookup tables.

The table values are generally based on:

Input transition
Output load

The tool uses these values to estimate cell delay and output transition.

🔹 CCS — Composite Current Source

CCS provides a more detailed representation of the electrical behavior of a cell by using current-source-based modeling.

It can represent cell behavior more accurately for advanced timing and power analysis.

🆚 Comparison
Characteristic	NLDM	CCS

Model	Lookup tables	Current-source based

Main focus	Delay & transition	Detailed electrical behavior

Complexity	Relatively simple	More detailed

Timing analysis	Widely used	More advanced modeling

Data representation	Table-based	Current waveform/behavior based

💡 Easy Way to Remember
NLDM
↓
Input Slew + Output Load
↓
Delay / Transition

CCS
↓
Detailed Current Behavior
↓
More Detailed Cell Modeling


**🧠 Key Learnings:**

Understood how OpenLane configuration controls the physical implementation process.

Learned how floorplanning establishes the physical framework of the chip.

Understood the difference between core and die dimensions.

Learned why pre-placed blocks are important for physical organization.

Understood how the PDN distributes VDD and VSS throughout the design.

Learned how standard cells are physically positioned during placement.

Understood the purpose of placement blockages and reserved regions.

Learned how placement optimization improves timing, wirelength, and congestion.

Understood how routing converts logical connections into physical metal connections.

Explored the complete development flow of a standard cell.

Learned why library characterization is required before cells can be effectively modeled by EDA tools.

Understood timing characterization and the importance of input/output conditions.

Learned how timing thresholds are used for consistent measurements.

Understood propagation delay and transition/slew measurements.

Learned the importance of noise margin for reliable digital operation.

Understood the basic differences between NLDM and CCS timing models.


🌟 Module Perspective

Physical Structure
       +
Power & Placement
       +
Routing
       +
Cell Characterization
       ↓
Better Understanding of
ASIC Physical Implementation

The module therefore connects chip-level physical implementation with cell-level timing and electrical modeling, giving a broader view of the RTL-to-GDSII process.

**🏁 Conclusion:**

Physical Design Module 2 provided a deeper look into how a synthesized design is organized, placed, powered, optimized, and connected physically.

The module also introduced standard-cell characterization, showing how important parameters such as delay, transition, power, and noise behavior are measured and represented in library models.

By studying both physical implementation and library characterization, it becomes easier to understand the relationship between cell behavior and chip-level design quality.

Overall, this module strengthened the understanding of the Physical Design flow and demonstrated how floorplanning, placement, power planning, routing, and accurate cell models work together toward a reliable ASIC implementation.
