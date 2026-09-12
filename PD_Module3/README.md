**Module 3:CMOS Inverter Design,Simulation,CMOS Fabrication**

**📌 Project Overview:**

This project presents a complete study of CMOS inverter design, beginning with transistor-level circuit construction and SPICE simulation and progressing toward physical layout and CMOS fabrication concepts.

The work covers:

**CMOS Circuit → SPICE Netlist → DC Analysis → VTC → Switching Threshold → Transistor Sizing → Layout → CMOS Fabrication**

The project demonstrates how a simple CMOS inverter can be analyzed from both the electrical/circuit level and the physical/manufacturing level.

**🎯 Objectives:**

The major objectives of this project are:

1.To understand the operation of a CMOS inverter using NMOS and PMOS transistors.
2.To construct and analyze a transistor-level CMOS inverter using SPICE.
3.To study the relationship between transistor dimensions and inverter characteristics.
4.To obtain and analyze the Voltage Transfer Characteristic (VTC).
5.To determine the switching threshold voltage, \(V_M\).
6.To study CMOS inverter robustness and transistor sizing.
7.To understand the influence of \(W/L\) ratios on inverter behavior.
8.To understand the physical implementation of a CMOS standard cell.
9.To study the major stages involved in a 16-mask CMOS fabrication process.
10.To understand active-region formation, well formation, gate formation, LDD implantation, source/drain formation,       contacts, and metallization.
11.To connect circuit-level simulation with semiconductor fabrication technology.

## 🔧 Tools & Technologies

| Tool / Technology | Purpose |
|---|---|
| **SPICE / NGSPICE** | Circuit simulation |
| **CMOS Inverter** | Circuit under study |
| **NMOS & PMOS** | Transistor devices |
| **VTC Analysis** | Static inverter characterization |
| **Magic VLSI** | Physical layout |
| **SKY130A PDK** | CMOS technology and design rules |
| **Linux Terminal** | Simulation and design workflow |
| **Git & GitHub** | Version control and documentation |

**🔬 Project Workflow:**

CMOS Inverter Design
        ↓
SPICE Netlist Creation
        ↓
DC Simulation
        ↓
VTC Generation
        ↓
Switching Threshold Analysis
        ↓
Transistor Sizing
        ↓
Physical Layout
        ↓
16-Mask CMOS Fabrication Study
        ↓
Contacts & Local Interconnect
        ↓
Higher-Level Metal
        ↓
Complete CMOS Structure

**1. SPICE CMOS Inverter Design:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 50 PM (1)" src="https://github.com/user-attachments/assets/35ffc534-a531-4b95-9fac-078436799367" />

The first stage establishes the transistor-level CMOS inverter using a SPICE netlist.
The circuit consists of:

One PMOS transistor connected to \(V_{DD}\)
One NMOS transistor connected to \(V_{SS}\)
Common gate input
Common drain output
A capacitive load at the output
Defined transistor dimensions
CMOS model definitions
DC simulation commands

The initial design uses:

      Wn ​= Wp​ = 0.375μm
​      Ln​ = Lp ​= 0.25μm 
Therefore,
      Wn/Ln = Wp/Lp = 1.5

Building the inverter from the ground up: the SPICE deck defines the transistors, device dimensions, supply conditions, input stimulus, load capacitance, and simulation environment required to electrically characterize the CMOS inverter.      

**2️. SPICE Simulation — Initial Device Configuration:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 50 PM (2)" src="https://github.com/user-attachments/assets/693e88e1-dbf1-4fd1-b974-16b4fdfada23" />

This image represents the simulation environment for the CMOS inverter with equal NMOS and PMOS sizing.

The simulation helps establish the fundamental relationship between:

Input Voltage → Transistor State → Output Voltage

The inverter operates through complementary transistor action:

When the input is LOW, PMOS conducts and NMOS is OFF.
When the input is HIGH, NMOS conducts and PMOS is OFF.
During transition, both devices influence the output voltage.

​From equations to behavior: SPICE converts the transistor-level description into measurable electrical behavior, allowing the inverter response to be examined before physical implementation.

**3️. CMOS Inverter Voltage Transfer Characteristic:**

<img width="1271" height="1124" alt="WhatsApp Image 2026-09-12 at 10 53 11 AM" src="https://github.com/user-attachments/assets/7ff07114-5521-43a7-bedb-70ff02e7a24c" />
   

The simulation produces the characteristic Voltage Transfer Curve of the CMOS inverter.

The VTC illustrates the relationship:

                         Vout = f(Vin)

The curve contains three important operating regions:
	​
HIGH OUTPUT        TRANSITION        LOW OUTPUT

Vout ≈ VDD            ↓              Vout ≈ 0
     ────────────────╲
                       ╲
                        ╲
                         ─────────────

The sharp transition demonstrates the high voltage gain of the CMOS inverter around its switching region.

**The transition point reveals the heart of the inverter:** a small change in input voltage produces a large change in output voltage, demonstrating the regenerative behavior that makes CMOS logic effective.

**4️. Transistor Sizing Comparison:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 50 PM (4)" src="https://github.com/user-attachments/assets/02ba8fb8-10b8-47ef-b8cb-aaadc87d4d95" />

Two inverter configurations are compared:

Configuration 1

                Wn​ = Wp ​= 0.375μm
                
                Wn​​/Ln = Lp/​Wp ​​= 1.5 

Configuration 2

                Wn ​= 0.375μm

                Wp ​= 0.9375μm

                Wn​​/Ln = 1.5

                Wp/Lp ​​= 3.75

Changing the PMOS width changes the relative drive strength of the PMOS and NMOS devices, which consequently shifts the inverter's transition characteristics.


**Sizing changes the balance:** transistor geometry is not merely a physical parameter—it directly influences the electrical operating point of the CMOS inverter.                

**5️. CMOS Inverter Robustness — Switching Threshold:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 50 PM (5)" src="https://github.com/user-attachments/assets/3e1dee5d-0fc6-4085-98c9-3fb39588e681" />

The switching threshold voltage \(V_M\) is the point where:

                        Vin = Vout

The figure compares inverter behavior for different transistor sizing conditions and illustrates how the switching point changes with transistor strength.

The observed values shown in the work include approximately:

V_M ~ 0.98V
V_M ~ 1.2V

depending on the device sizing configuration.

**Finding the balance point:** \(V_M\) marks the voltage where the inverter transitions between its logic states. Transistor sizing determines where this balance occurs.

**6️. Mathematical Analysis of Switching Threshold:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 50 PM (6)" src="https://github.com/user-attachments/assets/f0e9ea18-3be6-481c-b575-4f211a53993b" />

The switching threshold can also be analyzed mathematically using the relative strength of the NMOS and PMOS devices.

The figure introduces the relationship between:

1.Wn/Ln

2.Wp/Lp

3.Kn

4.Kp

5.Saturation voltage

6.Device threshold parameters

The switching threshold is therefore not an arbitrary simulation result—it is strongly related to the drive-strength ratio of the two transistors.

**Connecting simulation with theory:** the analytical model explains why changing transistor dimensions shifts the switching threshold observed in the SPICE VTC.

**7️. Final Switching-Threshold Comparison:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 50 PM (7)" src="https://github.com/user-attachments/assets/40d92205-7ef5-4098-9360-bf3da84021be" />

The final characterization image combines the inverter VTC with sizing information and timing-related results.

It demonstrates how changing transistor dimensions affects the inverter's electrical response.

The analysis emphasizes an important CMOS design principle:

Device sizing determines the balance between NMOS and PMOS strength, which influences switching behavior and timing.

**Characterization closes the loop:** simulation results are interpreted using transistor sizing and device-strength relationships, transforming raw SPICE plots into meaningful CMOS design information.

**8️. Physical CMOS Layout:**

<img width="1262" height="627" alt="image" src="https://github.com/user-attachments/assets/e9d573d3-228a-496b-9a30-9a45b0276100" />

The project then moves from electrical design to physical implementation.

The layout represents the physical arrangement of the CMOS inverter using technology-specific layers.

The major physical elements include:

1.PMOS region
2.NMOS region
3.Polysilicon gate
4.Active regions
5.Contacts
6.Metal interconnections
7.Power and ground connections

This stage demonstrates how the transistor schematic is transformed into an actual geometric representation suitable for fabrication.

**A circuit becomes geometry:** the schematic describes what the circuit does; the layout defines how that circuit physically exists on silicon.

**9. 🏭 CMOS FABRICATION PROCESS**

The following images represent the 16-mask CMOS fabrication sequence included in the project.

**9️.1 - Active Region Formation:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 50 PM (10)" src="https://github.com/user-attachments/assets/cca719e0-878b-4ae3-a0bc-a6119c0954b3" />

The fabrication sequence begins by defining the regions where transistors will be formed.

The figure illustrates:

P-type silicon substrate
Silicon nitride masking
Photoresist
Field oxide
LOCOS isolation
Bird's-beak effect

The process shown is LOCOS — Local Oxidation of Silicon.

The field oxide isolates active transistor regions from surrounding areas.

**Defining where transistors can exist:** before building the transistor itself, the silicon surface must be divided into active and isolation regions. LOCOS provides the isolation required for controlled device formation.

**9.2 - N-Well and P-Well Formation:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 50 PM (11)" src="https://github.com/user-attachments/assets/f38f4f20-bae2-483c-afb3-fd9f699c5acb" />

Complementary MOS technology requires regions with different conductivity types.

The fabrication stage uses ion implantation to create the required wells.

The figure illustrates implantation into the silicon substrate to establish the well regions required for NMOS and PMOS devices.

**Creating complementary homes:** NMOS and PMOS devices require different body regions. Well formation establishes the electrical environment in which each transistor will operate.

**9.3 - Threshold Voltage & Body Effect:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM" src="https://github.com/user-attachments/assets/51815d48-ef40-45e7-8a43-35f061ff3160" />

This image provides the theoretical foundation for MOS threshold voltage and the body effect.

The threshold voltage is represented as:

 <img width="435" height="77" alt="image" src="https://github.com/user-attachments/assets/505045f6-5b93-40a3-91cf-0eb71bd3d063" />

The threshold voltage depends on parameters including:

- **V<sub>T0</sub>** — threshold voltage at zero body bias
- **γ** — body-effect coefficient
- **V<sub>SB</sub>** — source-to-body voltage
- **Φ<sub>F</sub>** — Fermi potential
- **N<sub>A</sub>** — doping concentration
- **C<sub>ox</sub>** — oxide capacitance

**The physics behind the switch:** transistor behavior is controlled not only by the gate voltage but also by substrate doping, oxide properties, and body bias. 

**9.4 - Gate Formation — Initial Stage:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (1)" src="https://github.com/user-attachments/assets/a7ceb243-b1a0-4253-956e-9c25d8fe4f24" />

The next fabrication stage creates the transistor gate structure.

The gate is the control terminal of the MOS transistor and determines whether a conductive channel is formed between source and drain.

The figure shows the processing steps associated with gate formation and implantation.

**Creating the control element:** the gate is where electrical control meets semiconductor physics. Its formation defines the region that ultimately controls channel conduction.

**9.5 - Gate Formation — Completed Structure:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (2)" src="https://github.com/user-attachments/assets/a013bfab-f972-47ab-8ab8-e6889c41196e" />

This image continues the gate-formation stage and shows the resulting physical structure after the required processing steps.

The gate separates the transistor's source and drain regions while controlling the channel underneath.

**The transistor begins to take shape:** once the gate structure is established, the physical geometry required for controlling current through the channel is clearly defined.

**9.6 - LDD Formation — Initial Implantation:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (3)" src="https://github.com/user-attachments/assets/ad56cf79-7c32-45a3-9f5c-a87683e86e31" />

The Lightly Doped Drain (LDD) process introduces lightly doped regions near the transistor source/drain areas.

LDD structures are used to manage the electric-field conditions near the drain and improve device reliability.

**Engineering the electric field:** LDD formation introduces controlled doping near the channel, helping manage high electric fields within the transistor.

**9.7 - LDD Formation — Phosphorus Implantation:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (4)" src="https://github.com/user-attachments/assets/97df6e73-5c37-4085-8402-37623094ef21" />

The figure shows phosphorus implantation associated with the LDD formation process.

Controlled ion implantation modifies the conductivity of selected silicon regions.

The fabrication process therefore uses doping engineering to transform patterned silicon into electrically functional transistor regions.

**Doping defines electrical behavior:** carefully controlled implantation converts selected silicon regions into the conductivity profiles required for transistor operation.

**9.8 - Side-Wall Spacer Formation:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (5)" src="https://github.com/user-attachments/assets/ddb0b612-57ae-4f93-9bd8-bd39c40f7c56" />

Side-wall spacers are formed around the gate structure following the LDD implantation.

These spacers are important because they establish the physical offset between the gate and subsequent heavily doped source/drain regions.

**Precision through spacing:** the side-wall spacer acts as a physical ruler, controlling how closely the heavily doped source and drain regions can approach the transistor gate.

**9.9 - Source & Drain Formation:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (6)" src="https://github.com/user-attachments/assets/63575cad-8e25-416b-b989-52c1c5e1dbab" />

The next stage forms the final source and drain regions using high-temperature processing.

At this point, the essential transistor structure is present:

        Gate
         │
   ┌─────┴─────┐
   │   Channel │
───┴───────────┴───
 Source       Drain

The completed source/drain structure provides the terminals through which current enters and leaves the transistor.

**The transistor becomes functional:** source and drain formation completes the primary semiconductor structure needed for controlled current flow.

**9.10 - Contacts & Local Interconnect — Titanium Deposition:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (7)" src="https://github.com/user-attachments/assets/c4d91001-6edc-473d-96b1-2329b34c935b" />

Once the transistor structures are complete, electrical connections must be created.

The figure shows the deposition of titanium on the wafer surface using sputtering.

This stage prepares the structure for creating low-resistance electrical connections between semiconductor regions and interconnect layers.

**Making silicon accessible:** fabricated transistor terminals cannot remain isolated inside the silicon. Contact technology creates the bridge between the device and the interconnect system.

**9.11 - Contact Formation:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (8)" src="https://github.com/user-attachments/assets/801c2fd8-dd3b-4127-a2ed-aebcd63615bd" />

The next stage defines the contact regions that connect:

Source
Drain
Gate

to the local interconnect structure.

These contacts provide conductive paths between the transistor and higher-level wiring.

**Turning devices into circuits:** contacts establish the first electrical pathways that allow individual transistors to communicate with the outside interconnect network.

**9.12 - Higher-Level Metal Formation:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (9)" src="https://github.com/user-attachments/assets/7e2844f3-871b-43ab-ad3d-0221c34a7dba" />

CMOS fabrication continues by building higher levels of metal interconnect.

These metal layers allow signals, power, and ground to travel across the chip.

The interconnect hierarchy transforms individual fabricated devices into a connected circuit network.

**Building the chip's highway system:** higher-level metal provides the long-range electrical pathways required to connect devices across an integrated circuit.

**9.13 - Complete CMOS Structure:**

<img width="1280" height="590" alt="WhatsApp Image 2026-09-11 at 10 51 51 PM (10)" src="https://github.com/user-attachments/assets/19bd91bc-d229-4742-8d46-a8052377a732" />

The final image represents the completed CMOS fabrication structure.

The different layers collectively represent:

Silicon substrate
Well regions
Active regions
Gate structures
Source/drain regions
Contacts
Local interconnect
Higher-level metal

The result is a multilayer CMOS structure in which semiconductor devices and metal interconnects work together as an integrated system.

**From bare silicon to an integrated circuit:** every layer built during fabrication contributes to the final CMOS structure, demonstrating how circuit concepts ultimately become physical hardware.

**🧩 Complete Fabrication Flow:**

P-Type Silicon Substrate
          ↓
Active Region Formation
          ↓
N-Well / P-Well Formation
          ↓
Threshold / Body Engineering
          ↓
Gate Formation
          ↓
LDD Implantation
          ↓
Side-Wall Spacer Formation
          ↓
Source / Drain Formation
          ↓
Contact Formation
          ↓
Local Interconnect
          ↓
Higher-Level Metal
          ↓
Complete CMOS Structure

**10. Layout and Abstract View:**

The journey from a circuit diagram to a physical silicon implementation begins with the standard-cell layout. Using the SKY130A technology, the CMOS inverter is translated into an arrangement of physical layers that represents how the circuit would actually exist on silicon.

The layout is constructed using essential layers such as:

Metal layers – provide electrical routing between different regions.
Polysilicon – forms the transistor gate structures.
Diffusion – defines the active source and drain regions.
Contacts – establish connections between different layers.
Well regions – provide the required transistor body structures.
Power and ground rails – distribute VDD and GND throughout the cell.

Alongside the detailed layout, an abstract view provides a simplified representation of the cell that contains the physical information required by the digital implementation flow.

Together, the layout and abstract representation form the physical identity of the standard cell. They are inspected to ensure that the geometry, layers, and connectivity are properly established.

<img width="1252" height="555" alt="image" src="https://github.com/user-attachments/assets/5f71c7ef-30ad-4a39-8b3b-58dd9a90fb2c" />

**Figure : Layout and abstract representation of the standard cell**

The circuit takes its first physical form here — transforming transistor-level logic into a structured silicon layout while keeping both detailed geometry and implementation-ready abstraction in view.

**11. Defining the Cell Boundary:**

A standard cell needs a clearly defined physical home. After completing the layout, a cell boundary is established to specify the exact region occupied by the circuit.

The boundary defines the usable width and height of the cell and provides a fixed framework within which the transistor and routing structures are arranged.

A properly defined boundary helps maintain:

Uniform cell dimensions
Accurate placement
Alignment with neighbouring cells
Correct VDD and GND rail positions
Compatibility with the standard-cell library

This regular structure allows multiple cells to be placed side-by-side or stacked within a larger physical-design environment without disrupting their alignment.

<img width="1262" height="627" alt="image" src="https://github.com/user-attachments/assets/816d5884-dcb0-4a83-ae8a-7ad37f07b8b7" />

**Figure : Defined standard-cell boundary**

The boundary acts as the cell’s physical frame, giving the layout a disciplined structure that allows it to become part of a larger digital system.

**12. Power and Ground Connectivity:**

Once the cell structure is established, the next critical task is connecting its power and ground network.

The CMOS cell relies on two fundamental supply connections:

VDD – supplies the positive operating voltage.
GND – provides the ground/reference potential.

These supply rails are connected to the appropriate transistor regions and routed through the required physical layers.

For a CMOS inverter, the PMOS network is associated with the supply side, while the NMOS network is connected towards ground. Correct routing ensures that the complementary transistor networks can perform their intended switching operation.

Reliable power connectivity is essential not only for circuit functionality but also for maintaining the standard physical structure expected by the cell library.

<img width="1359" height="712" alt="Screenshot (182)" src="https://github.com/user-attachments/assets/e56ddad5-d321-4234-af24-3577a3d52301" />

**Figure : Power and ground connections in the layout**

Power gives the cell its operating energy, while ground completes the electrical path — together forming the foundation for reliable CMOS switching.

**13. Layout Extraction:**

A physical layout contains geometry, but simulation requires an electrical circuit. Layout extraction forms the bridge between these two worlds.

Once the layout is complete, the extraction process interprets the physical shapes and converts them into an electrical representation.

The extraction identifies important information such as:

Transistors present in the layout
Electrical nodes
Device-to-device connections
Physical device dimensions
Power and ground paths
Parasitic elements

This information is used to create a SPICE-compatible representation of the implemented circuit.

Unlike an ideal schematic, the extracted representation carries information originating from the actual physical implementation. This makes it valuable for evaluating the behaviour of the circuit after layout.

<img width="958" height="934" alt="extracting 5th image" src="https://github.com/user-attachments/assets/9281895a-cdaf-43b5-bd97-fe5652ed2a41" />

**Figure : Extraction of the layout**

Extraction turns silicon geometry back into electrical meaning — allowing the physical design to speak the language of circuit simulation.

**14. Generating the Extracted Netlist:**

After extraction, the generated files are examined to confirm that the physical layout has been successfully converted into electrical connectivity.

The extracted netlist acts as a textual description of the devices and connections discovered within the layout.

It contains the information required to reconstruct the physical implementation for further simulation and analysis.

Before moving forward, the generated files are verified to ensure that the required device and connectivity information is available.

Typical outputs from this stage include extracted layout data and SPICE-compatible netlist information.

<img width="958" height="934" alt="commands for 5th image" src="https://github.com/user-attachments/assets/6e2a0e14-19a6-499c-8211-922763a2d024" />

**Figure : Generated extracted files and netlist**

The netlist is the electrical blueprint recovered from the physical layout — a compact description of how every device and connection comes together.

**15. Creating the SPICE File:**

The extracted information is now transformed into a simulation-ready SPICE file.

This file brings together the device models, circuit connections, and simulation information required by NGSPICE.

The SPICE representation includes:

Technology and device model information
Standard-cell subcircuit definition
Input and output nodes
VDD connection
GND connection
Extracted transistor information
Simulation parameters

The extracted transistor and connectivity information is organized into a suitable subcircuit so that the physical CMOS implementation can be electrically evaluated.

<img width="958" height="934" alt="6th spice file" src="https://github.com/user-attachments/assets/71584479-2934-46cf-a0fa-99bd6f1ad115" />
**Figure : SPICE file generated for simulation**

The extracted layout is given a simulation identity here — converting physical device information into a SPICE environment ready for electrical analysis.

**16 .Transient Simulation using NGSPICE:**

With the SPICE representation ready, the extracted CMOS inverter is brought into the simulation environment using NGSPICE.

Transient analysis is performed by applying a time-varying input signal and observing how the output responds over time.

The circuit is operated with the required supply conditions while important nodes are monitored:

**Input
 Output
 VDD
 GND**

The changing input allows the simulator to capture the inverter’s switching behaviour and verify whether the extracted circuit is electrically connected and capable of successful simulation.

This stage marks the transition from physical implementation back to measurable electrical behaviour.

<img width="958" height="934" alt="7th image" src="https://github.com/user-attachments/assets/156adb31-de86-4f91-95b1-6b047d725ae7" />
**Figure : NGSPICE transient analysis**

The extracted circuit is now put to the test — NGSPICE observes the cell as it switches, revealing whether the physical implementation behaves like the intended CMOS inverter.

**17 .Input and Output Waveforms:**

The transient simulation produces the most direct visual evidence of inverter operation: the input and output waveforms.

As the input alternates between LOW and HIGH, the output responds in the complementary manner expected from a CMOS inverter.

Input	             Output
LOW	                HIGH
HIGH	              LOW

The resulting waveform confirms the fundamental inverter relationship:

**Output = NOT(Input)**

The output also approaches the expected supply and ground levels, demonstrating that the extracted standard cell maintains the required digital logic behaviour.

<img width="958" height="934" alt="8th" src="https://github.com/user-attachments/assets/462635ce-8158-4138-8edb-8b8db8b45fa1" />
**Figure : Simulated input and output transient waveforms**

The waveforms reveal the inverter’s true character — every input transition is answered by a complementary output response.

GitHub Description:
Transistor dimensions are more than physical measurements — they directly shape how strongly, quickly, and efficiently the inverter switches.

**18. Physical Verification and Layout Analysis**

Once the layout is created, the physical structure is carefully inspected to confirm that the CMOS cell has been implemented correctly.

Every important layer and connection is examined, including transistor regions, diffusion, polysilicon, contacts, metal interconnects, and the power network. This ensures that the physical layout remains faithful to the intended CMOS circuit.

The verification process focuses on:

Correct electrical connectivity
Reliable VDD and GND distribution
Properly defined cell boundary
Appropriate use of technology layers
Correct PMOS and NMOS arrangement

A successful physical layout should not only look structurally correct but should also preserve the electrical intent of the original circuit.

**19. Standard Cell Layout Structure:**

The CMOS inverter follows the familiar structure used in standard-cell design.

The PMOS network occupies the upper section of the cell and connects towards the VDD rail, whereas the NMOS network is positioned below and connects towards GND.

The input signal is routed to the transistor gates, while the output is taken from the shared node between the pull-up and pull-down networks.

This organized arrangement creates a compact and repeatable cell structure that can be easily integrated with other standard cells in a larger digital design.

The physical layout reflects the logic architecture — PMOS pulls upward, NMOS pulls downward, and the common output node completes the inverter.

**20. Extraction and Parasitic Information:**

The completed layout contains more than just ideal transistor connections. Its physical dimensions and interconnect geometry introduce additional electrical effects.

During layout extraction, the physical shapes are translated into an electrical representation, allowing these real-world effects to be considered during simulation.

The extracted parasitic information can affect:

Propagation delay
Rise time
Fall time
Output transition speed
Dynamic switching behaviour

Because of these effects, post-layout simulation can provide a more realistic picture of circuit performance than an ideal schematic simulation.

**21. SPICE Model and Device Parameters**

The extracted CMOS inverter is represented using the device and technology information provided by the SKY130A PDK.

The corresponding transistor models supply NGSPICE with the electrical parameters needed to reproduce MOS-device behaviour during simulation.

By combining the extracted layout information with these technology-specific models, the resulting simulation becomes a closer representation of the physically implemented circuit rather than an ideal transistor-level abstraction.

This provides a stronger basis for evaluating the standard cell before integrating it into a larger digital system.

Technology models bring the extracted transistors to life, allowing the simulator to interpret their behaviour under realistic operating conditions.

**22. Simulation Setup:**

Before starting transient analysis, the extracted circuit must be provided with the appropriate operating conditions and input stimulus.

The supply is connected between VDD and GND, while the inverter input receives a time-dependent digital signal. The simulator then tracks how the output node responds to these changes.

The simulation is primarily used to examine:

Correct logical operation
Expected HIGH and LOW voltage levels
Output switching transitions
Timing characteristics
Stable circuit response

These conditions establish the foundation for analysing the behaviour of the extracted CMOS inverter.

**23. CMOS Inverter Operation:**

The CMOS inverter performs its logic function through the complementary switching action of PMOS and NMOS transistors.

Input LOW

When the input is at a LOW level:

The PMOS transistor turns ON.
The NMOS transistor turns OFF.
The output is pulled towards VDD.
The output therefore becomes HIGH.

Input HIGH

When the input changes to HIGH:

The PMOS transistor turns OFF.
The NMOS transistor turns ON.
The output is pulled towards GND.
The output therefore becomes LOW.

Thus, the inverter continuously produces the logical opposite of its input.

Two complementary devices, one simple rule — when one path rises, the other falls, producing the fundamental NOT operation of CMOS logic.

**24. Rise and Fall Behaviour:**

The output of a CMOS inverter does not switch between logic levels instantaneously.

When the input changes from LOW to HIGH, the output moves from HIGH to LOW. Conversely, when the input changes from HIGH to LOW, the output transitions from LOW to HIGH.

The gradual slope observed during these transitions is influenced by the charging and discharging of capacitances present in the circuit.

Physical interconnects and extracted parasitic components can further modify these transition characteristics.

Therefore, the rise and fall portions of the waveform provide useful information about the dynamic behaviour of the implemented cell.

Logic may be binary, but real switching is not instantaneous — capacitance and parasitics shape every rise and fall of the output waveform.

**25. Timing Behaviour:**

The transient response provides valuable information about how quickly the standard cell reacts to changes at its input.

Important timing quantities include:

Rise time
Fall time
Propagation delay
Input transition time
Output transition time

These characteristics become especially important when several standard cells are connected to form larger digital systems.

The physical layout, transistor dimensions, load conditions, and parasitic effects can all influence the resulting timing performance.

Functionality tells us what the cell does; timing tells us how quickly it does it — making delay and transition behaviour essential for real digital systems.

**26. Voltage Levels:**

The simulated waveform is also examined to confirm that the inverter reaches the expected logic voltage levels.

For a valid CMOS response:

The HIGH output should approach the supply voltage.
The LOW output should approach the ground potential.

These voltage levels demonstrate that the pull-up and pull-down networks are operating correctly.

Consequently, the waveform serves as an important check of both the inverter's logical functionality and its electrical behaviour.

The waveform is not just a shape on a graph — its voltage levels reveal whether the CMOS cell is successfully reaching the intended logic states.

**27. Transistor Sizing and Performance:**

The physical dimensions of the PMOS and NMOS transistors play an important role in determining the performance of the CMOS inverter.

Changing device dimensions can influence:

Drive strength
Rise time
Fall time
Propagation delay
Power consumption
Switching characteristics

Proper transistor sizing is therefore important for achieving a balanced response between the pull-up and pull-down networks.

The dimensions selected during layout are reflected in the extracted circuit, allowing their influence to be observed during post-layout simulation.

**28. Layout-to-Simulation Correlation:**

A major goal of the project is to connect the physical implementation of the circuit with its electrical simulation behaviour.

The complete relationship can be represented as:

Layout → Extraction → SPICE Netlist → NGSPICE Simulation → Waveform Analysis

The layout establishes the physical geometry of the standard cell.

The extraction stage interprets this geometry and generates its corresponding electrical representation.

The resulting SPICE netlist is then prepared for NGSPICE simulation, where the circuit is subjected to the required input and supply conditions.

Finally, the simulated waveforms are examined to determine whether the physically implemented inverter behaves according to its intended logic.

## 🔑 Key Learnings

* Understood the **working principle of CMOS inverter** using complementary PMOS and NMOS transistors.

* Learned to perform **SPICE and NGSPICE simulations** for analysing CMOS circuit behaviour.

* Analysed **input/output waveforms, voltage levels, rise time, fall time, and propagation delay**.

* Studied how **transistor sizing** affects drive strength, switching speed, delay, and power consumption.

* Learned to convert a circuit schematic into a **physical CMOS standard-cell layout**.

* Understood the importance of **cell boundaries, layer organization, and standard-cell structure**.

* Implemented and verified **VDD and GND connectivity** within the physical layout.

* Learned how **layout extraction** converts physical geometry into an electrical netlist.

* Understood the role of **parasitic effects** in post-layout circuit behaviour.

* Gained practical exposure to the **SKY130A PDK, Magic VLSI, SPICE, and NGSPICE** design flow.

* Learned how to correlate **physical layout with simulated electrical behaviour**.

* Studied the **16-mask CMOS fabrication process**, from well formation to metallization.

* Understood the complete semiconductor design flow:

  **Circuit Design → Simulation → Characterization → Layout → Extraction → Post-Layout Simulation → Fabrication**

* 🚀 Developed a broader understanding of how a **transistor-level concept is transformed into a verified physical silicon implementation**.

**🎯 Conclusion:**

This project provided a complete view of the **CMOS inverter**, starting from its transistor-level operation and extending all the way to physical layout, post-layout simulation, and semiconductor fabrication.

The inverter was first studied as a circuit to understand its logic and electrical behaviour. Through SPICE and NGSPICE simulations, the relationship between input and output, switching transitions, voltage levels, timing behaviour, and transistor sizing was explored.

The design was then transformed into a **SKY130A standard-cell layout**, where the abstract circuit became a physical structure made from diffusion, polysilicon, contacts, metal interconnects, wells, and power rails.

The physical layout was subsequently extracted into an electrical representation. This created the important connection between **what is drawn on silicon** and **what is observed in simulation**. Post-layout analysis demonstrated how physical effects and parasitics can influence real circuit behaviour.

The study of the **16-mask CMOS fabrication process** completed the journey by showing how these carefully designed structures can ultimately be translated into physical devices on a silicon wafer.
