# ⚡ Industrial Motor Protection Controller Using Verilog HDL

### RTL Design • Simulation • Synthesis • Physical Design • RTL-to-GDS Flow

## 📌 Project Overview

The **Industrial Motor Protection Controller Using Verilog HDL** is a digital system designed to protect industrial motors from problems such as overcurrent, overheating, and power supply faults.

The controller monitors fault signals and controls the motor accordingly. When a fault is detected, it switches off the motor and stores the fault information using a fault code.

This project demonstrates the process of designing, testing, and converting Verilog HDL code into a physical chip layout using tools such as Icarus Verilog, GTKWave, Yosys, OpenLane, and the Sky130A technology.


## 📌 Project at a Glance

| Property           | Description                                      |
| ------------------ | ------------------------------------------------ |
| Project Name       | Industrial Motor Protection Controller           |
| Design Language    | Verilog HDL                                      |
| Top Module         | `motor_protection_controller`                    |
| Design Type        | FSM-based digital controller                     |
| Simulation         | Icarus Verilog, GTKWave                          |
| Synthesis          | Yosys                                            |
| Timing Analysis    | OpenSTA                                          |
| Physical Design    | OpenLane                                         |
| Technology         | Sky130A                                          |
| Layout Tools       | Magic, KLayout                                   |
| Verification Tools | Netgen and available physical-verification tools |
| OpenLane Run       | `run16`                                          |

## 🧭 Project Contents:

- **01** — [The Problem & Our Solution](#-01-the-problem--our-solution)
- **02** — [Project Objectives](#-02-project-objectives)
- **03** — [Inputs and Outputs](#-03-inputs-and-outputs)
- **04** — [System Architecture](#-04-system-architecture)
- **05** — [FSM and Sequential Logic](#-05-fsm-and-sequential-logic)
- **06** — [Tools and Technologies](#-06-tools-and-technologies)
- **07** — [Project Structure](#-07-project-structure)
- **08** — [Functional Test Cases](#-08-functional-test-cases)
- **09** — [RTL Design](#-09-rtl-design)
- **10** — [Simulation](#-10-functional-simulation)
- **11** — [Waveform Analysis](#-11-waveform-analysis)
- **12** — [Logic Synthesis](#-12-logic-synthesis)
- **13** — [Pre-Layout STA](#-13-pre-layout-static-timing-analysis)
- **14** — [RTL-to-GDS Physical Design Flow](#-14-rtl-to-gds-physical-design-flow)
- **15** — [Floorplanning](#-15-floorplanning)
- **16** — [Standard Cell Placement](#-16-standard-cell-placement)
- **17** — [Clock Tree Synthesis](#-17-clock-tree-synthesis)
- **18** — [Routing](#-18-routing)
- **19** — [Post-Route STA: Min & Max](#-19-post-route-sta-minimum--maximum-timing)
- **20** — [SPICE Analysis](#-20-spice-analysis)
- **21** — [Final GDS Layout](#-21-final-gds-layout)
- **22** — [Physical Verification & Signoff](#-22-physical-verification--signoff)
- **23** — [Results Summary](#-23-results-summary)
- **24** — [Conclusion](#-24-conclusion)
- **25** — [Author](#-25-author)

---

## 🔍 01. The Problem & Our Solution

### The Problem

Industrial motors are essential in pumps, conveyors, fans, and manufacturing equipment. Abnormal current, excessive temperature, or unstable supply conditions can cause equipment damage and unsafe operation.

A protection system must detect faults, disable motor operation, and retain fault information even when the fault input returns to normal.

### Our Solution

We designed a dedicated digital controller using Verilog HDL.

The controller:

- Accepts motor start and stop requests.
- Monitors overcurrent, overtemperature, and supply-fault inputs.
- Disables the motor when a fault is detected.
- Latches fault information.
- Reports the detected fault using a 2-bit fault code.
- Requires reset to clear the latched fault, according to the intended design behaviour.

### Real-World Applications

- Industrial motor drives
- Water pumps and conveyor belts
- Cooling and ventilation fans
- Factory automation systems
- Embedded motor-control applications

> **Design goal:** Simple, predictable digital fault handling with a clearly defined control sequence.

*Project concept illustration:*



---

## 🎯 02. Project Objectives

- Implement a synthesizable FSM using Verilog HDL.
- Develop motor start and stop control logic.
- Detect and latch multiple fault conditions.
- Verify functionality using Icarus Verilog.
- Inspect signal behaviour using GTKWave.
- Synthesize the design using Yosys.
- Analyse timing using OpenSTA.
- Perform physical implementation using OpenLane and Sky130A.
- Examine floorplanning, placement, CTS, and routing.
- Review minimum-delay and maximum-delay STA reports.
- Document SPICE analysis and final GDS results where available.

---

## 🔌 03. Inputs and Outputs

| Signal            | Direction | Function                        |
| ----------------- | --------- | ------------------------------- |
| `clk`             | Input     | System clock                    |
| `reset_n`         | Input     | Active-low reset                |
| `start_req`       | Input     | Requests motor startup          |
| `stop_req`        | Input     | Requests motor shutdown         |
| `overcurrent`     | Input     | Indicates excessive current     |
| `overtemp`        | Input     | Indicates excessive temperature |
| `supply_fault`    | Input     | Indicates a supply abnormality  |
| `motor_enable`    | Output    | Enables motor operation         |
| `fault_latched`   | Output    | Indicates a stored fault        |
| `fault_code[1:0]` | Output    | Identifies the fault condition  |

### Fault Code

| Code | Meaning                                         |
| ---- | ----------------------------------------------- |
| `00` | No fault                                        |
| `01` | Overcurrent                                     |
| `10` | Overtemperature                                 |
| `11` | Confirm against RTL; may represent supply fault |

The actual encoding, fault priority, and simultaneous-fault behaviour must match the implemented RTL.

---

## 🏗️ 04. System Architecture

The design is organised around motor-control logic, fault detection, and fault storage.

```text
       START / STOP REQUESTS
                |
                v
      +---------------------+
      |    FSM CONTROLLER   |
      +---------------------+
                |
                v
      +---------------------+
      |    MOTOR CONTROL    |
      +---------------------+
                |
                v
          motor_enable


  OVERCURRENT / OVERTEMP /
        SUPPLY FAULT
                |
                v
      +---------------------+
      |   FAULT DETECTION   |
      +---------------------+
                |
                v
      +---------------------+
      |  FAULT LATCH & CODE |
      +---------------------+
                |
                v
       fault_latched
       fault_code[1:0]
```

**Architecture highlights**

- The FSM controls the operating state.
- Fault inputs influence the controller's transitions.
- Fault information is stored in registers.
- The outputs indicate motor permission and fault status.



---

## 🔄 05. FSM and Sequential Logic

The controller uses a Finite State Machine to determine motor behaviour.

The intended operating states are:

| State | Purpose                                   |
| ----- | ----------------------------------------- |
| IDLE  | Motor remains disabled                    |
| RUN   | Motor is allowed to operate               |
| FAULT | Motor is disabled and a fault is retained |

### Operating Sequence

1. Reset initialises the controller.
2. A valid start request moves the controller towards RUN.
3. A stop request disables the motor.
4. A fault condition causes shutdown and fault recording.
5. A start request during a latched fault should not restart the motor.
6. Reset clears the fault and restores the initial condition.

The exact transition logic depends on the RTL implementation.

---

## 🧰 06. Tools and Technologies

| Stage                   | Tool                          |
| ----------------------- | ----------------------------- |
| RTL coding              | Verilog HDL                   |
| Functional simulation   | Icarus Verilog                |
| Waveform inspection     | GTKWave                       |
| Logic synthesis         | Yosys                         |
| Static timing analysis  | OpenSTA                       |
| Physical implementation | OpenLane                      |
| Process design kit      | Sky130A                       |
| Layout inspection       | Magic, KLayout                |
| LVS                     | Netgen                        |
| Circuit simulation      | SPICE simulator actually used |

**Environment:** Ubuntu/Linux with the required EDA tools and Sky130A PDK.

---

## 📁 07. Project Structure

Recommended GitHub repository organisation:

```text
Industrial_Motor_Protection_Controller/
├── README.md
├── rtl/
│   └── motor_protection_controller.v
├── tb/
│   └── tb_motor_protection_controller.v
├── physical_design/
│   ├── config.json
│   └── reports/
│       ├── sta_min/
│       ├── sta_max/
│       └── signoff/
├── spice/
│   ├── netlist/
│   ├── testbench/
│   └── results/
├── gds/
│   └── motor_protection_controller.gds
└── images/
    ├── design_architecture.png
    ├── rtl_code.png
    ├── simulation.png
    ├── waveform.png
    ├── synthesis.png
    ├── prelayout_sta.png
    ├── floorplan.png
    ├── placement.png
    ├── cts.png
    ├── routing.png
    ├── sta_min.png
    ├── sta_max.png
    ├── spice_waveform.png
    └── final_gds.png
```

*Include only files that actually exist in your repository. OpenLane run outputs can be kept in their generated directories or copied into the report folders.*

---

## 🧪 08. Functional Test Cases

| Test Case          | Expected Result                         |
| ------------------ | --------------------------------------- |
| Reset              | Motor disabled, fault cleared           |
| Start request      | Motor starts if no fault is active      |
| Stop request       | Motor stops                             |
| Overcurrent        | Motor disabled; fault recorded          |
| Overtemperature    | Motor disabled; fault recorded          |
| Supply fault       | Motor disabled; fault recorded          |
| Fault input clears | Latched fault remains active            |
| Start during fault | Motor remains disabled                  |
| Reset after fault  | Controller returns to its initial state |

**Verification status:** Add the actual PASS/FAIL results produced by your testbench.

---

## 💻 09. RTL Design

**Source file:** `rtl/motor_protection_controller.v`

**RTL CODE:**

<img width="992" height="875" alt="rtlcode1" src="https://github.com/user-attachments/assets/893b6290-6d78-442b-a8b1-467da6cd3414" />
<img width="977" height="536" alt="rtlcode2" src="https://github.com/user-attachments/assets/15313494-8f1f-4179-a229-3463a7d98c70" />

The RTL describes the FSM, motor-enable logic, fault detection, fault latching, reset handling, and fault-code generation.

**TESTBENCH CODE:**

<img width="982" height="856" alt="tb1" src="https://github.com/user-attachments/assets/63f590bb-76c9-4dd9-b3ff-ffd6c313dac9" />
<img width="966" height="851" alt="tb2" src="https://github.com/user-attachments/assets/cf58b070-2935-4dbf-a7ab-99759b42f1de" />
<img width="821" height="887" alt="tb3" src="https://github.com/user-attachments/assets/96761fd7-f515-404d-b31b-e9a4cf6611b8" />

The design is used as the input to simulation and synthesis.

<img width="1777" height="811" alt="image" src="https://github.com/user-attachments/assets/6d60abaa-9c10-4660-b950-78f168b6774f" />


---

## ▶️ 10. Functional Simulation

Icarus Verilog is used to compile and simulate the RTL with its testbench.

### Commands

```bash
iverilog -o sim.out rtl/motor_protection_controller.v tb/tb_motor_protection_controller.v
vvp sim.out
```

### What Is Verified?

- Reset operation
- Start and stop behaviour
- Fault detection
- Fault latching
- Fault-code output
- Restart prevention during a latched fault



---

## 📈 11. Waveform Analysis

GTKWave helps visualise how the input and output signals change during simulation.

### Command

```bash
gtkwave dump.vcd
```

### Signals to Observe

`clk`, `reset_n`, `start_req`, `stop_req`, `overcurrent`, `overtemp`, `supply_fault`, `motor_enable`, `fault_latched`, and `fault_code`.

The waveform should illustrate motor startup, shutdown following a fault, fault retention, and reset recovery.

<img width="1082" height="947" alt="Gtkwave" src="https://github.com/user-attachments/assets/e046e435-c967-4df2-8180-fb7d8c0629be" />


---

## ⚙️ 12. Logic Synthesis

Yosys synthesizes the Verilog RTL into a logic representation suitable for implementation.

### Commands

```bash
yosys
read_verilog rtl/motor_protection_controller.v
synth -top motor_protection_controller
stat
```

<img width="861" height="652" alt="stat_result" src="https://github.com/user-attachments/assets/0ad7b919-db4b-496d-b3d1-048aa8e1619c" />

### Synthesis Analysis

The synthesis report provides information about:

- Sequential cells
- Combinational cells
- Flip-flop usage
- Logic structure
- Cell statistics

Previously observed design statistics were approximately 25 cells at one synthesis stage and 35 cells after a different mapping stage. Use these values only with the corresponding reports and commands, since synthesis results can vary with mapping and optimization.


---

## ⏱️ 13. Pre-Layout Static Timing Analysis

Pre-layout STA evaluates timing paths using the available timing constraints and standard-cell libraries before final routed parasitics are incorporated.

### Parameters Analysed

- Clock period
- Setup slack
- Hold slack
- Critical path delay
- Worst Negative Slack (WNS)
- Total Negative Slack (TNS)

The analysis depends on the configured SDC constraints and selected process, voltage, and temperature corner.


<img width="802" height="837" alt="pre layout" src="https://github.com/user-attachments/assets/ccfbd381-743b-41ad-9684-05342c6075b5" />


---

## 🏭 14. RTL-to-GDS Physical Design Flow

The physical implementation flow converts the synthesised digital design into a physical chip layout.

```text
       Verilog RTL
           |
           v
      Simulation
           |
           v
      Synthesis
           |
           v
      Floorplanning
           |
           v
        Placement
           |
           v
          CTS
           |
           v
         Routing
           |
           v
    Post-Route STA
           |
           v
     Physical Checks
           |
           v
        Final GDS
```

**Physical-design configuration**

- Design: `motor_protection`
- Top module: `motor_protection_controller`
- Run tag: `run16`
- PDK: Sky130A
- Flow: OpenLane

The results for the run are expected under:

```text
~/OpenLane/designs/motor_protection/runs/run16/
```

The exact output directories depend on the installed OpenLane version and configuration.

---

## 🟦 15. Floorplanning

Floorplanning establishes the chip's core and die regions and prepares the design for placement.

### Magic Setup

Open Magic with the Sky130A technology file:

```bash
magic -T $PDK_ROOT/sky130A/libs.tech/magic/sky130A.tech
```

### Commands — Magic TkCon Console

Enter the following commands in the Magic console:

```tcl
lef read tmp/merged.nom.lef
def read results/floorplan/motor_protection_controller.def
```

<img width="822" height="805" alt="Floorplanning final" src="https://github.com/user-attachments/assets/7601389f-0429-432b-a41e-e2afb225c78c" />


### What the Layout Shows

- Core and die regions
- Placement rows
- Initial physical organisation
- Power structures, if present in the loaded layout

---

## 🟩 16. Standard Cell Placement

Placement assigns physical positions to the standard cells inside the core area.

### Commands — Magic TkCon Console

```tcl
lef read tmp/merged.nom.lef
def read results/placement/motor_protection_controller.def
```

<img width="862" height="602" alt="placement" src="https://github.com/user-attachments/assets/0f90b6d2-2bcb-418c-8ed1-c4e9301e2bdd" />


### What the Layout Shows

- Standard-cell positions
- Placement rows
- Cell distribution within the core
- Physical organisation before subsequent routing stages



---

## 🟨 17. Clock Tree Synthesis (CTS)

Clock Tree Synthesis builds the clock distribution network and inserts clock buffers where required.

### Commands — Magic TkCon Console

```tcl
lef read tmp/merged.nom.lef
def read results/cts/motor_protection_controller.def
```

<img width="775" height="642" alt="cts" src="https://github.com/user-attachments/assets/e3ed3374-fc9f-4419-8dcd-9314884fe54e" />


### What the Layout Shows

- The design after clock-tree implementation
- Clock-related buffers and cells, where present
- The physical organisation used for subsequent routing



---

## 🟥 18. Routing

Routing creates the metal interconnections and vias needed to connect the standard cells.

### Commands — Magic TkCon Console

```tcl
lef read tmp/merged.nom.lef
def read results/routing/motor_protection_controller.def
```

<img width="820" height="661" alt="routing final" src="https://github.com/user-attachments/assets/6f7076c5-913a-4a6e-80c2-1636da4bd732" />

### What the Layout Shows

- Routed signal interconnects
- Metal layers and vias
- Connections between placed cells
- The design after the routing stage



### Important Notes for Stage Visualisation

The commands above assume Magic is running from the appropriate OpenLane run directory, where `tmp/merged.nom.lef` and the `results/` paths are valid.

If Magic reports that a file cannot be found, check the actual run directory and the filenames before loading the next stage. Start a fresh Magic session for each stage when necessary to avoid confusing an already-loaded layout with a new one.

Each screenshot must come from the corresponding stage's DEF layout. Opening the final GDS repeatedly will show the final layout rather than four different physical-design stages.

---

## 📊 19. Post-Route STA: Minimum & Maximum Timing

Post-route Static Timing Analysis checks the timing behaviour after physical implementation, using extracted or estimated interconnect parasitics according to the flow configuration.

### Maximum-Delay Analysis

Maximum-delay analysis primarily checks setup timing. It determines whether data arrives before the required capture time.

<img width="667" height="892" alt="max final" src="https://github.com/user-attachments/assets/a7a50d67-3daa-4671-af29-3ba87af7653e" />

Important metrics:

- Worst setup slack / WNS
- Total Negative Slack (TNS)
- Critical path delay
- Startpoint and endpoint
- Timing analysis corner

### Minimum-Delay Analysis

Minimum-delay analysis primarily checks hold timing. It determines whether data arrives late enough to satisfy the minimum-delay requirement.

<img width="716" height="900" alt="min final" src="https://github.com/user-attachments/assets/750b29c4-e666-42fb-a8c9-e9d552ecec43" />

Important metrics:

- Worst hold slack
- Hold violations
- Critical path
- Timing analysis corner

### STA Results

| Parameter                 | Measured Value       |
| ------------------------- | -------------------- |
| Minimum-delay corner      | Add actual corner    |
| Minimum-delay slack       | Add value and unit   |
| Maximum-delay corner      | Add actual corner    |
| Maximum-delay slack / WNS | Add value and unit   |
| TNS                       | Add value and unit   |
| Clock period              | Add configured value |
| Critical path delay       | Add value and unit   |

If several PVT corners were analysed, report each corner separately. Preserve the actual values and signs from your STA reports.





---

## 🔬 20. SPICE Analysis

SPICE analysis is used for circuit-level simulation when a suitable transistor-level netlist and device models are available.

### Analysis Objectives

- Observe transient circuit behaviour.
- Inspect voltage and current waveforms.
- Measure propagation delay where applicable.
- Evaluate switching behaviour under the specified test conditions.

### SPICE Results

| Item          | Project Details              |
| ------------- | ---------------------------- |
| Simulator     | Add the actual simulator     |
| Netlist       | Add the actual filename      |
| Testbench     | Add the actual filename      |
| Device model  | Add the actual model/library |
| Analysis type | Add the analysis performed   |
| Measurement   | Add the measured result      |

<img width="867" height="702" alt="spice final" src="https://github.com/user-attachments/assets/fb387e99-f626-4fb0-b8ac-f497a28583b4" />

---

## 🧩 21. Final GDS Layout

The final GDSII file represents the physical layout produced by the implementation flow.

**Expected filename:** `motor_protection_controller.gds`

**Run-specific output path:**

```text
~/OpenLane/designs/motor_protection/runs/run16/results/final/gds/motor_protection_controller.gds
```

### View Using Magic

```bash
magic -d OGL -T $PDK_ROOT/sky130A/libs.tech/magic/sky130A.tech /path/to/motor_protection_controller.gds
```

Replace the example path with the actual GDS path.

### View Using KLayout

```bash
klayout /path/to/motor_protection_controller.gds
```

### Final Layout Inspection

Inspect the layout for:

- Overall chip geometry
- Standard-cell regions
- Metal interconnects
- Power structures, where present
- The physical design generated by the flow

<img width="810" height="632" alt="gds final" src="https://github.com/user-attachments/assets/8424428e-481e-47d5-adf9-fc0dd4426113" />

---

## 🛡️ 22. Physical Verification & Signoff

Physical verification evaluates the layout against applicable manufacturing rules and connectivity requirements.

| Check          | Purpose                                                 | Actual Status      |
| -------------- | ------------------------------------------------------- | ------------------ |
| DRC            | Checks geometric design rules                           | Add report result  |
| LVS            | Compares layout connectivity with the reference netlist | Add report result  |
| Antenna        | Checks applicable antenna rules                         | Add report result  |
| Setup timing   | Evaluates maximum-delay constraints                     | Add report result  |
| Hold timing    | Evaluates minimum-delay constraints                     | Add report result  |
| GDS generation | Confirms physical layout output                         | Verify file exists |

### Report Location

OpenLane run reports are generally stored beneath the run directory, for example:

```text
~/OpenLane/designs/motor_protection/runs/run16/reports/
```

Check the actual report filenames for your OpenLane version. Do not mark DRC, LVS, antenna, or timing as passed unless the corresponding reports establish that result.

---

## 📋 23. Results Summary

| Stage                 | Evidence                                       |
| --------------------- | ---------------------------------------------- |
| RTL Design            | Verilog source code                            |
| Functional Simulation | Testbench output                               |
| Waveform Analysis     | GTKWave waveform                               |
| Synthesis             | Yosys statistics                               |
| Pre-Layout STA        | Timing report                                  |
| Floorplanning         | Floorplan DEF view                             |
| Placement             | Placement DEF view                             |
| CTS                   | CTS DEF view                                   |
| Routing               | Routing DEF view                               |
| Post-Route STA        | Minimum- and maximum-delay reports             |
| SPICE                 | Netlist and circuit simulation results         |
| Final Layout          | GDSII file                                     |
| Signoff               | Available DRC, LVS, antenna and timing reports |

This project brings together digital design, simulation, synthesis, timing analysis, physical implementation, and layout inspection in a single workflow.

---

## 🏁 24. Conclusion

The Industrial Motor Protection Controller demonstrates the design and implementation of a fault-monitoring digital controller using Verilog HDL.

The project covers FSM-based motor control, fault detection and latching, functional simulation, logic synthesis, minimum- and maximum-delay timing analysis, and physical implementation through OpenLane and the Sky130A technology.

By studying the floorplan, placement, clock tree, routing, SPICE results, and final GDS layout, the project provides practical exposure to the digital VLSI design flow from RTL to physical implementation.

---

## 👩‍💻 25. Author

**B. Sruthi**
B.Tech — Electronics and Communication Engineering

**Project:** Industrial Motor Protection Controller Using Verilog HDL

**Technologies:** Verilog HDL · Icarus Verilog · GTKWave · Yosys · OpenSTA · OpenLane · Sky130A · Magic · KLayout · Netgen · SPICE

---

*Designed to demonstrate a complete digital VLSI workflow — from RTL logic to physical layout.*
