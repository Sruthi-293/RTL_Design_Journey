# RTL-to-GLS Verification of a Sequence Detector

## 📌 Project Overview

This project demonstrates the implementation and verification of a Verilog-based sequence detector. The design is tested through RTL simulation, logic synthesis, and Gate-Level Simulation (GLS). Waveforms are analyzed to check whether the synthesized circuit maintains the expected functionality of the original RTL design.

The project also includes debugging a SKY130 standard-cell model and comparing the results obtained before and after synthesis.

## 🔄 Verification Workflow

RTL Design
↓
Pre-Synthesis Simulation
↓
RTL Waveform Analysis
↓
Logic Synthesis
↓
Gate-Level Netlist Generation
↓
Gate-Level Simulation (GLS)
↓
GLS Waveform Analysis
↓
RTL and GLS Result Comparison

## 1. 📁 Project Structure

The working directory used during this exercise was:

`~/BabySoC_Simulation/assesments/25eg504h50`

Important files used in the workflow:

```text
24eg104d55/
├── rtl/
├── tb/
│   └── tb.v
├── synthesized.v
├── pre_synth_sim.out
└── dump.vcd
```

A separate copy of the SKY130 simulation model was created during debugging:

`sky130_fd_sc_hd_gls.v`

## 2. 💻 RTL Design Description

The sequence detector is implemented using a Finite State Machine (FSM) in Verilog. It receives serial input data and generates an output when the specified bit sequence is detected.

Main module:

```verilog
module sequence_detector(clk, reset, din, detected);
```

### Important Signals

| Signal            | Description                             |
| ----------------- | --------------------------------------- |
| `clk`             | Clock signal for synchronization        |
| `reset`           | Initializes the FSM                     |
| `din`             | Serial input data                       |
| `detected`        | Indicates successful sequence detection |
| `state[2:0]`      | Represents the current FSM state        |
| `next_state[2:0]` | Represents the upcoming FSM state       |

The FSM changes states according to the incoming bits. The detection output indicates when the required sequence has been recognized.

## 3. 🧪 Testbench Implementation

The testbench is available in `tb/tb.v`. It generates the clock, applies input data, controls reset, and monitors the output.

The design is instantiated as follows:

```verilog
sequence_detector dut (
    .clk(clk),
    .reset(reset),
    .din(din),
    .detected(detected)
);
```

### Clock Generation

```verilog
always #4 clk = ~clk;
```

The clock period is 8 ns.

### Input Data and Detection Counter

The testbench applies a sequence of zeros and ones using statements such as:

```verilog
drive_bit(1'b0);
drive_bit(1'b1);
```

A counter is used to record detection events:

```verilog
integer detection_count = 0;
```

The counter increments when reset is inactive and the detection output is high:

```verilog
if (!reset && detected)
    detection_count = detection_count + 1;
```

### Waveform Generation

The simulation records signal transitions in a VCD file using:

```verilog
$dumpfile("dump.vcd");
$dumpvars(0, tb);
```

The generated file, `dump.vcd`, can be opened in GTKWave for waveform analysis.

**Note:** The testbench path is `tb/tb.v`.

## 4. 📊 Pre-Synthesis Simulation

The original RTL design was simulated before synthesis to check its functional behavior.

The simulation generated:

* `pre_synth_sim.out`
* `dump.vcd`

The waveform was examined using GTKWave.

### Signals Observed

* Clock and reset
* Serial input and detection output
* Current and next FSM states
* Detection counter

This stage verifies that the FSM initializes correctly, processes the input sequence, changes states as expected, and produces detection events.

The pre-synthesis waveform is also used as a reference for later comparison.

**Screenshot:** Add the pre-synthesis waveform image here.

## 5. 🌊 RTL Waveform Analysis

GTKWave was used to observe the relationship between the input bits, clock transitions, FSM states, and detection output.

Waveform analysis helps identify whether the circuit responds correctly to the applied testbench inputs. The RTL simulation provides the reference behavior against which the synthesized implementation is evaluated.

## 6. ⚙️ Logic Synthesis

After verifying the RTL simulation, the design was synthesized to generate a gate-level netlist.

The generated file is:

`synthesized.v`

To locate the sequence-detector module in the synthesized file, use:

```bash
grep -n "module sequence_detector" synthesized.v
```

The generated netlist represents the synthesized circuit and is used in the next verification stage.

## 7. 🔬 Gate-Level Simulation (GLS)

Gate-Level Simulation checks the synthesized circuit using the testbench and a standard-cell simulation model.

The files required are:

* `tb/tb.v`
* `synthesized.v`
* SKY130 standard-cell model

The original model used in this environment was located at:

`/home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v`

The objective is to verify that the synthesized implementation continues to exhibit the intended sequence-detection behavior.

## 8. 🛠️ Debugging the SKY130 Model

During the initial GLS compilation, a syntax error was reported at line 67667 of the SKY130 model. Compilation failed, so `gls_sim.out` was not generated.

The model was checked for an invalid declaration using:

```bash
grep -n 'wire 1' /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v | head
```

The search identified declarations written as `wire 1;`. The identifier `1` is not valid as a normal Verilog signal name.

To preserve the original model, a separate copy was created:

```bash
cp /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v ./sky130_fd_sc_hd_gls.v
```

The invalid declarations in the local copy were replaced with a valid identifier:

```bash
sed -i -E 's/^[[:space:]]*wire[[:space:]]+1[[:space:]]*;/ wire one;/' sky130_fd_sc_hd_gls.v
```

The modified file was checked using:

```bash
grep -n 'wire 1|wire one' sky130_fd_sc_hd_gls.v | head
```

The surrounding code was inspected with:

```bash
sed -n '67515,67535p' sky130_fd_sc_hd_gls.v
sed -n '67655,67680p' sky130_fd_sc_hd_gls.v
```

This debugging step produced a local model with `wire one;` replacing the invalid declarations.

## 9. ▶️ Running GLS

The gate-level simulation was compiled using:

```bash
iverilog -g2012 -o gls_sim.out tb/tb.v synthesized.v sky130_fd_sc_hd_gls.v
```

After successful compilation, the simulation was executed with:

```bash
vvp gls_sim.out
```

The testbench generated `dump.vcd`, which was opened in GTKWave:

```bash
gtkwave dump.vcd
```

This allowed the synthesized circuit's signal transitions and detection behavior to be examined.

## 10. 📈 GLS Waveform Results

The GLS waveform was examined using the following signals:

* `clk`
* `reset`
* `din`
* `detected`
* `state[2:0]`
* `next_state[2:0]`
* `detection_count`

The recorded waveform showed four detection events. The first observed detection occurred at approximately 1169 ns, and the detection counter reached 4.

**Screenshot:** Add the GLS waveform image here.

## 11. 🔍 RTL vs GLS Comparison

Both simulations were evaluated using the same testbench input sequence.

| Parameter                    | Observed Result       |
| ---------------------------- | --------------------- |
| RTL detection events         | 4                     |
| GLS detection events         | 4                     |
| First recorded GLS detection | Approximately 1169 ns |

The matching detection counts indicate that the synthesized implementation preserved the expected logical behavior for the tested input sequence.

Some timing differences may occur between RTL and gate-level waveforms because the synthesized circuit is represented using standard cells.

## 12. 🧰 Tools and Technologies

| Tool              | Purpose                                     |
| ----------------- | ------------------------------------------- |
| Verilog           | RTL design and testbench development        |
| Icarus Verilog    | Compiling RTL and GLS simulations           |
| VVP               | Executing compiled simulations              |
| Yosys             | Logic synthesis                             |
| SKY130 cell model | Standard-cell simulation during GLS         |
| GTKWave           | Waveform inspection                         |
| Linux terminal    | Compilation, file management, and debugging |
| Git and GitHub    | Version control and project documentation   |

## 13. 📋 Useful Commands

```bash
# List files
ls

# Inspect the testbench
ls tb
cat tb/tb.v

# Locate the synthesized module
grep -n "module sequence_detector" synthesized.v

# Search for the invalid declaration
grep -n 'wire 1' /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v | head

# Create a local model copy
cp /home/vsduser/BabySoC_Simulation/src/gls_model/sky130_fd_sc_hd.v ./sky130_fd_sc_hd_gls.v

# Correct the invalid identifier
sed -i -E 's/^[[:space:]]*wire[[:space:]]+1[[:space:]]*;/ wire one;/' sky130_fd_sc_hd_gls.v

# Compile the gate-level simulation
iverilog -g2012 -o gls_sim.out tb/tb.v synthesized.v sky130_fd_sc_hd_gls.v

# Run the simulation
vvp gls_sim.out

# View the waveform
gtkwave dump.vcd
```

## 14. ✅ Work Summary

The following activities were completed during this exercise:

* Designed and simulated a Verilog sequence detector.
* Created testbench stimulus and generated waveform data.
* Examined the pre-synthesis waveform in GTKWave.
* Synthesized the design and inspected the resulting netlist.
* Investigated and corrected a syntax issue in a local SKY130 model copy.
* Executed Gate-Level Simulation.
* Analyzed the GLS waveform and detection counter.
* Compared RTL and GLS detection results.

## 🏁 Conclusion

This project demonstrates the verification process from RTL design through synthesis and Gate-Level Simulation. For the tested input sequence, both RTL and GLS produced four detection events, showing consistent logical behavior between the two implementations. The waveform analysis and model-debugging steps provided practical experience with digital design verification, synthesis, and standard-cell simulation.
