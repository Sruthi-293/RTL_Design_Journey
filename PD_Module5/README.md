**Module 5: Routing, DRC, Parasitic Extraction & TritonRoute**

**📌 Project Overview:**

This module focuses on the **routing and physical verification stages** of the RTL-to-GDSII physical-design flow.

The module covers:

* Physical routing

* Design Rule Checking (DRC)

* Wire-width rules

* Via-spacing rules

* Signal-short prevention

* Parasitic extraction

* Fast routing

* Detailed routing

* TritonRoute

* Preprocessed route guides

* Intra-layer parallel routing

* Inter-layer sequential routing

* Access points

* Connectivity handling

* Routing topology optimization

**🎯 Objectives**

* Understand the routing stage of physical design.

* Understand Design Rule Checking (DRC).

* Study important routing design rules.

* Understand wire-width and via-spacing requirements.

* Study parasitic extraction.

* Understand fast routing and detailed routing.

* Understand the role of TritonRoute.

* Study preprocessed route guides.

* Understand intra-layer and inter-layer routing.

* Understand routing connectivity.

* Study Access Points and Access Point Clusters.

* Understand routing topology optimization.

* Analyse routing results using terminal outputs.

## 🔧 Tools & Technologies

| **Tool / Technology**    | **Purpose**                                               |
| ------------------------ | --------------------------------------------------------- |
| **OpenLane**             | RTL-to-GDSII physical-design flow                         |
| **OpenROAD**             | Physical implementation and routing                       |
| **TritonRoute**          | Detailed routing                                          |
| **Magic VLSI**           | Layout viewing and physical verification                  |
| **SKY130A PDK**          | CMOS technology and design-rule information               |
| **PicoRV32A**            | RISC-V processor design used as the implementation target |
| **Linux Terminal**       | Flow execution and analysis                               |
| **Tcl**                  | OpenLane/OpenROAD configuration and scripting             |
| **Parasitic Extraction** | Extraction of interconnect resistance and capacitance     |
| **Git & GitHub**         | Version control and documentation                         |

**🔬 Project Workflow**

Placement → Routing → Fast Routing → Route Guides → Detailed Routing → DRC → Parasitic Extraction → Physical Verification

**1. Routing**

<img width="753" height="424" alt="image" src="https://github.com/user-attachments/assets/6d44a2b8-0fd0-4791-b479-f2126f78984b" />

* Shows the routing stage of the physical-design flow.

* The central portion contains the placed standard cells and functional blocks.

* Different colors represent different metal layers and physical routing structures.

* Horizontal and vertical metal tracks are used to establish connections between cells.

* Input and output signals such as Din1–Din4 and DOut1–DOut4 are visible around the design.

* Clock-related signals such as CLK1 and CLK2 are also shown.

* The routing connects the different logic elements according to their netlist connectivity.

* The image demonstrates the transformation from a placed design into a physically interconnected layout.

**2. DRC Clean**

This image shows the routed physical layout after **Design Rule Checking (DRC)**. DRC verifies whether the geometry of the layout follows the manufacturing rules defined by the technology. A DRC-clean result indicates that the demonstrated layout satisfies the applicable physical design rules.

<img width="753" height="424" alt="image" src="https://github.com/user-attachments/assets/8c1efc0d-bf8d-4d94-9a0a-176c7cad9424" />

* Metal spacing and geometry are checked.

* Wire widths are verified against technology requirements.

* Possible shorts between different signals are checked.

* Via-related physical constraints are also considered.

* DRC verification is an important step before final physical verification.

**3. Maze Routing – Lee's Algorithm**

This image explains Maze Routing using Lee's Algorithm. The routing area is represented as a grid containing obstacles, with a source and destination that need to be connected. The algorithm searches through the available grid locations to find a valid path between the two points.

<img width="753" height="424" alt="image" src="https://github.com/user-attachments/assets/7e51a187-1cb4-43ae-ba46-a978db3df926" />

* The routing area is divided into grid cells.

* Obstacles restrict the available routing paths.

* The algorithm searches neighboring grid locations.

* A valid path is established between the source and destination.

* The highlighted path demonstrates how routing can avoid physical obstacles.

* Lee's algorithm is useful for understanding basic automated routing techniques.

**4. DRC – Wire Width**

This image illustrates a wire-width design rule used during physical verification. Metal wires must maintain a minimum width specified by the technology. If the physical width of a routed wire is smaller than the required value, the layout can result in a DRC violation.

<img width="753" height="298" alt="image" src="https://github.com/user-attachments/assets/eda98929-bccf-4985-aa62-d1285e70d550" />

* Minimum metal width must be maintained.

* Wire geometry is compared with technology rules.

* Narrow wires can cause physical-design violations.

* Proper wire width supports manufacturability and reliable interconnection.

* Detailed routing tools must consider these restrictions.

**5. DRC – Via Spacing**

The fifth image demonstrates the via-spacing design rule. Vias provide electrical connections between different metal layers, and their physical placement must satisfy minimum spacing requirements. This rule becomes particularly important in dense routing regions where many vias are placed close together.

<img width="753" height="299" alt="image" src="https://github.com/user-attachments/assets/dc139f51-62ce-452d-ade3-6abed71f6765" />

* Vias connect different metal layers.

* Minimum spacing must be maintained between neighboring vias.

* Incorrect via spacing can result in a DRC violation.

* Detailed routing must consider via geometry and spacing.

* Proper via placement helps maintain manufacturable physical layouts.

**6. DRC – Signal Short**

This image explains the signal-short DRC condition. Different electrical nets must remain physically isolated unless they are intentionally connected. Incorrect routing or insufficient spacing between metal structures can create an unwanted electrical connection between two signals.

<img width="753" height="300" alt="image" src="https://github.com/user-attachments/assets/9e3a7635-74cc-43d3-9932-bef76867b5df" />

* Different signal nets must not accidentally touch.

* Metal tracks require appropriate separation.

* Unintended connections can create signal shorts.

* DRC detects such physical connectivity problems.

* Correct routing must preserve the original logical connectivity of the design.

**7. Routing Terminal Output**

This image shows the terminal output generated during routing. The Linux terminal displays commands and tool-generated messages associated with the physical-design process. Such outputs provide information about the execution and progress of routing operations.

<img width="753" height="308" alt="image" src="https://github.com/user-attachments/assets/6b18c00f-b7b2-4e5b-931b-54e7b6f4db1a" />

* The terminal contains routing-related processing information.

* Tool commands and their outputs are displayed.

* Logs can be used to monitor the routing process.

* Warnings and errors can be identified from the terminal.

* Terminal output complements the graphical layout generated by the tools.

**8. Physical Layout View**

The eighth image provides a larger **physical layout view** of the implemented design. Different functional regions are connected using several layers of physical interconnects. This view helps visualize how the circuit is organized after placement and routing.

<img width="753" height="429" alt="image" src="https://github.com/user-attachments/assets/b63f7614-b4be-46b6-b14a-d8dbb89d87c0" />

* Functional blocks are physically arranged inside the design.

* Multiple metal layers are visible.

* Routing structures connect different physical regions.

* Different colors indicate different physical layers or objects.

* The layout provides a graphical representation of the implemented circuit.

* Physical inspection can be performed using this type of layout view.

**9. Routing Terminal Output**

This image presents another section of the routing terminal output. The displayed messages represent additional processing performed by the physical-design tools during the routing stage. These command-line results provide information that cannot always be seen directly from the graphical layout.

<img width="753" height="322" alt="image" src="https://github.com/user-attachments/assets/68d0a4aa-b784-45a4-a7ac-8bed70377a90" />

* Multiple routing-related operations are displayed.

* The terminal provides intermediate processing information.

* Tool execution can be monitored through the generated logs.

* Errors or warnings can be identified during execution.

* The output forms part of the routing-process record.

**10. Routing Flow**

This image presents the two major stages of the routing process: **Fast Route** and **Detailed Route**. Fast routing generates an initial routing solution, while detailed routing further refines the connections by considering more detailed physical constraints.

<img width="753" height="308" alt="image" src="https://github.com/user-attachments/assets/a4184687-e86a-44b0-bbd3-d7c143e2e432" />

* Fast Route generates initial routing information.

* Detailed Route creates more precise physical connections.

* Fast routing provides a starting point for detailed routing.

* Detailed routing considers connectivity and physical constraints.

* The two-stage approach helps manage the complexity of routing.

**11. TritonRoute**

This image introduces TritonRoute, which is used for the detailed-routing stage of the physical-design flow. TritonRoute works with routing information generated by previous stages and converts the routing guides into detailed physical connections while considering routing constraints.

<img width="753" height="311" alt="image" src="https://github.com/user-attachments/assets/86b391fd-992d-4c1b-aa39-773310849e49" />

* TritonRoute performs detailed routing.

* It uses preprocessed route guides.

* Route guides restrict the regions in which nets can be routed.

* Connectivity must be maintained during detailed routing.

* Physical design rules must also be considered.

* TritonRoute forms an important part of the final routing stage.

**12. Preprocessed Route Guides**

The twelfth image shows preprocessed route guides used by the detailed-routing stage. These guides define the regions in which individual nets are expected to be routed. They provide important constraints to the detailed-routing engine.

<img width="753" height="408" alt="image" src="https://github.com/user-attachments/assets/6a800b62-b3bb-4372-bc13-97c17754b50a" />

* Route guides define permitted routing regions.

* Multiple guide structures are shown in the image.

* The guides provide routing information for different nets.

* They follow the required routing-layer information.

* Preferred routing directions are considered.

* TritonRoute uses these guides during detailed routing.

**13. Intra-Layer Parallel & Inter-Layer Sequential Panel Routing**

This image explains the concept of intra-layer parallel and inter-layer sequential panel routing. The routing problem is divided into panels so that different sections of the design can be processed systematically across routing layers.

<img width="753" height="433" alt="image" src="https://github.com/user-attachments/assets/940001cb-ef05-439a-aad7-90bfa450abdd" />

* Intra-layer routing can process multiple routing operations within a layer.

* Parallel processing can improve routing efficiency.

* Inter-layer routing handles connections between different metal layers.

* Routing panels divide the problem into manageable regions.

* Preferred routing directions are associated with different layers.

* This approach is part of the detailed-routing methodology.

**14. TritonRoute – Problem Statement**

The fourteenth image describes the **TritonRoute problem statement**. The detailed-routing engine receives physical-design information and route guides as input and produces a detailed routing solution. The routing process must satisfy several physical and connectivity constraints.

<img width="753" height="398" alt="image" src="https://github.com/user-attachments/assets/485ef699-1c0a-46e2-8fe5-d844ac61455c" />

* Inputs include LEF, DEF, and preprocessed route guides.

* The output is a detailed routing solution.

* Wire length is one of the routing optimization considerations.

* The number of vias is also considered.

* Route-guide constraints must be respected.

* Connectivity constraints must be satisfied.

* Design-rule requirements must also be maintained.

**15. TritonRoute – Handling Connectivity**

This image explains how TritonRoute handles connectivity using Access Points and Access Point Clusters. Access Points provide valid locations through which routing segments can establish connections between different layers, pins, and I/O structures.

<img width="753" height="417" alt="image" src="https://github.com/user-attachments/assets/348d4529-bddc-4e66-9110-273736d2b5dc" />

* Access Point (AP) represents a valid routing connection location.

* Access Points can connect different routing-layer segments.

* They can also be associated with pins and I/O ports.

* Access Point Clusters (APCs) group related access points.

* Selecting suitable access points is important for legal routing.

* Connectivity must be maintained throughout detailed routing.

**16. Routing Topology Algorithm**

The sixteenth image presents the Routing Topology Algorithm. Routing topology determines how multiple connection points are organized and interconnected before the detailed physical routes are generated. The algorithm provides a structured representation of the required connections.

<img width="753" height="416" alt="image" src="https://github.com/user-attachments/assets/64a66825-cdef-4d95-ad10-443e85a5c575" />

* The algorithm works with routing and connectivity information.

* Multiple routing points need to be interconnected.

* Distance information can be considered when constructing the topology.

* The generated topology provides a structure for detailed routing.

* The objective is to maintain connectivity while obtaining an efficient routing structure.

**17. Routing Terminal Output**

This image shows another set of routing terminal results generated during physical implementation. The terminal contains tool-generated messages that provide information about the execution of routing-related operations.

<img width="753" height="421" alt="image" src="https://github.com/user-attachments/assets/e268b352-414d-4681-a647-9847f75f2622" />

* Routing operations are displayed through command-line messages.

* The output provides intermediate processing information.

* Tool execution can be monitored through these logs.

* The results can help identify routing-related issues.

* Terminal information complements the physical layout representation.

**18. Routing Connectivity Output**

This image shows terminal information associated with routing connectivity. Connectivity is a critical requirement because every required net must connect its intended terminals without introducing unwanted electrical connections.

<img width="753" height="411" alt="image" src="https://github.com/user-attachments/assets/10661055-edfc-447e-b351-6ac2c1cf3df0" />

* The terminal contains routing and connectivity information.

* Required source and destination points must remain connected.

* Unrelated nets must remain electrically separated.

* Connectivity information is processed during detailed routing.

* The output provides intermediate information about the routing process.

* These results can be considered together with DRC verification.

**19. Detailed Routing Output**

The nineteenth image contains a more extensive detailed-routing terminal output. A large number of routing-related entries are displayed, indicating processing of multiple physical connections within the design.

<img width="753" height="375" alt="image" src="https://github.com/user-attachments/assets/48a97304-026c-489e-9b63-2a93b0509568" />

* Detailed routing processes the individual design nets.

* Route-guide constraints must be followed.

* Required connectivity must be maintained.

* Physical design rules must be satisfied.

* The terminal output provides information about routing progress.

* Such logs are useful for monitoring and debugging the detailed-routing stage.

**20. Routing Results**

This image shows additional routing results generated by the physical-design tools. The terminal output represents further processing of routing information and physical design objects. These results provide command-line evidence of the routing stage.

<img width="753" height="369" alt="image" src="https://github.com/user-attachments/assets/87246e0c-af41-46e0-9531-698503ec08fb" />

* Routing information is displayed in the terminal.

* Multiple physical design objects are processed.

* The output helps track routing operations.

* Routing results can be correlated with the generated layout.

* The information is useful for debugging and verification.

* Successful routing must preserve the required circuit connectivity.

**21. Detailed Routing Results**

The twenty-first image provides further detailed-routing results from the physical-design flow. The terminal output represents additional processing performed by the routing engine and provides information about the progress of detailed physical interconnection.

<img width="753" height="346" alt="image" src="https://github.com/user-attachments/assets/5e7bdcb2-97aa-4604-94d2-d0cc85569513" />

* Detailed routing processes multiple design nets.

* Logical connectivity must be preserved.

* Route-guide constraints must be satisfied.

* Physical design rules must be respected.

* The terminal provides intermediate routing information.

* These results complement graphical layout and DRC verification.

**22. Final Routing / Verification Output**

The final image shows the later-stage routing and verification output from the physical-design flow. At this stage, the routing information can be considered together with the physical layout and DRC results. The completed routed design can then proceed toward parasitic extraction and post-route analysis.

<img width="753" height="361" alt="image" src="https://github.com/user-attachments/assets/e0d6a240-eb35-45f8-af09-b3ddfc5ab07d" />

* Final routing information is displayed in the terminal.

* Routing results are considered together with physical-layout results.

* DRC results help verify physical correctness.

* The routed design provides the interconnect information required for parasitic extraction.

* Extracted parasitics can be used for post-route timing analysis.

* This completes the routing and physical-verification portion of Module 5.

**Routing Concepts**

* Routing – Establishes physical connections between circuit components.

* Maze Routing – Finds a valid path between source and destination through a routing grid.

* DRC – Checks whether the physical layout satisfies manufacturing design rules.

*Parasitic Extraction – Extracts resistance and capacitance associated with physical interconnects.

* Fast Routing – Generates initial routing information and route guides.

* Detailed Routing – Creates detailed physical connections for the nets.

* Route Guides – Define the permitted regions for routing.

* Access Point – An on-grid point used to establish routing connectivity.

* Access Point Cluster – A group of related access points.

* Routing Topology – Defines the structure used to connect routing points efficiently.

* TritonRoute – Performs detailed routing while considering connectivity and design-rule constraints.

**🔍 DRC Rules**

* **Wire Width** – Ensures that metal wires satisfy the required minimum width.

* **Via Spacing** – Ensures that vias maintain the required minimum spacing.

* **Signal Short Prevention** – Prevents physically unrelated signals from becoming electrically connected.

* **Connectivity** – Ensures that required source and destination points are properly connected.

**Fast Route vs Detailed Route**

| **Parameter** | **Fast Route**                    | **Detailed Route**             |
| ------------- | --------------------------------- | ------------------------------ |
| Purpose       | Generates initial routing         | Creates detailed final routing |
| Route Guides  | Generates route-guide information | Uses preprocessed route guides |
| Speed         | Faster                            | More detailed                  |
| Design Rules  | Preliminary consideration         | Detailed consideration         |
| Connectivity  | Initial routing connectivity      | Final routing connectivity     |

**DRC and Parasitic Extraction**

Routing → DRC Verification → Parasitic Extraction → Post-Route Analysis

* Routing creates the physical interconnections.

* DRC checks whether the layout satisfies physical design rules.

* Parasitic extraction identifies interconnect resistance and capacitance.

* Extracted parasitics can be used for more accurate post-route timing analysis.

**Conclusion**

Module 5 focuses on the **routing, DRC, parasitic extraction, and detailed-routing stages** of the physical-design flow. It demonstrates how the placed design is converted into a physically connected layout through **Fast Routing and Detailed Routing**. The module also introduces Maze Routing, route guides, access points, access point clusters, routing topology, and panel-based routing concepts used to handle complex interconnections.

The module further explains the role of **TritonRoute** in detailed routing and shows how routing must satisfy **connectivity, wire-width, via-spacing, signal-short, and other physical design constraints**. The terminal outputs and layout views provide evidence of the routing process and physical verification stages.

Overall, Module 5 demonstrates how routing information is progressively refined into a detailed physical implementation while maintaining logical connectivity and manufacturability. The completed routed layout can subsequently be used for **parasitic extraction and post-route timing analysis**, forming an important step toward the final physical-design implementation.















