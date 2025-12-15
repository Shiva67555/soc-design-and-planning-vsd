# soc-design-and-planning-nasscom-vsd
A two-week hands-on workshop on Digital VLSI SoC Design and Planning, covering the complete RTL-to-GDSII flow, conducted by VSD in association with NASSCOM, focusing on advanced physical design using OpenLANE and the SKY130 process.

Day 1: Introduction to RTL to GDSII and Open-Source ASIC Design Overview of the RTL to GDSII Flow

The RTL to GDSII flow represents the complete journey of a digital design, starting from a high-level behavioral description and ending with a manufacturable physical layout. This flow includes major stages such as RTL synthesis, floorplanning, placement, clock tree synthesis, routing, and multiple verification steps. The primary goal is to ensure that the final layout faithfully implements the intended logic, meets timing constraints, and complies with foundry design rules.

Design Abstraction in VLSI and the Y-Chart Model:-

A key theoretical concept introduced was design abstraction in VLSI systems. The Y-Chart model explains how a design evolves across three domains: a.Behavioral domain – functional description of the system b.Structural domain – organization of components and interconnections c.Geometric domain – physical representation of the design

Chip Structure and Major Components:-

The internal structure of an integrated circuit was discussed in detail, covering the following elements: 1.Core The region containing standard cells, IP blocks, combinational and sequential logic, and internal routing. 2.Die The physical silicon area that houses the core along with peripheral structures. Multiple dies are fabricated on a single wafer. 3.I/O Pads Interfaces that connect internal signals to the external package, including input, output, bidirectional, and power pads. 4.IP Blocks Pre-designed modules such as SRAMs, PLLs, ADCs, and DACs, typically provided by foundries due to their design complexity. 5.Process Design Kit (PDK) The PDK serves as the link between EDA tools and fabrication technology. It contains device models, design rule files, layout layers, and standard cell libraries. The workshop used the SkyWater 130 nm PDK (sky130_fd_sc_hd).

Introduction to RISC-V Architecture:-

RISC-V is an open and extensible Instruction Set Architecture (ISA). The ISA defines how software instructions are executed by hardware. Its open nature makes it widely adopted in both academic research and industrial processor development.

The software toolchain plays a critical role in execution, where high-level programming languages are translated into machine instructions through compilers, assemblers, and the operating system.

Software-to-Hardware Execution Flow:-

An overview of how software interacts with hardware was presented: 1.Application Layer – user-level programs 2.Operating System – manages system resources and hardware interaction 3.Compiler – converts high-level code into machine instructions 4.Assembler – encodes instructions into binary format

This flow establishes a direct link between application software and the processor microarchitecture.

Open-Source ASIC Design Ecosystem:-

The workshop highlighted the essential components required for a complete ASIC design environment: 1.RTL design files 2.EDA tools such as Yosys, OpenROAD, Magic, Netgen, and KLayout 3.PDK data OpenLane integrates these tools into a unified, automated flow, enabling end-to-end digital ASIC design using open-source resources.

Simplified RTL to GDSII Design Stages:-

The digital implementation flow was broken down into the following steps: 1.Synthesis Conversion of RTL code into a gate-level netlist using standard cells provided in multiple formats (Verilog, Liberty, LEF, SPICE, and GDS).

2.Floorplanning and Power Planning Definition of core dimensions, pin locations, macro placement, and power distribution networks including rings, straps, and rails.

3.Placement Arrangement of standard cells within rows: a.Global placement for rough positioning b.Detailed placement for legal and optimized alignment

4.Clock Tree Synthesis (CTS) Creation of a balanced clock network to minimize skew using structures such as H-trees or X-trees.

5.Routing a.Global routing to generate routing guides b.Detailed routing to implement final metal connections based on PDK rules

6.Sign-off Checks Final verification stages include: a.Design Rule Check (DRC) b.Layout vs Schematic (LVS) c.Parasitic extraction and Static Timing Analysis (STA) d.Antenna checks and prevention techniques OpenLane initially inserts fake diodes for antenna prevention and replaces them with real diodes if violations persist after routing.

Detailed OpenLane Flow:-

The complete OpenLane automation flow consists of: 1.RTL synthesis using Yosys and ABC 2.Static timing analysis 3.Optional DFT insertion using FAULT 4.Floorplan and powerplan generation 5.Placement and post-placement optimization 6.Clock tree synthesis 7.Routing 8.Physical verification using Magic and Netgen 9.Final GDSII generation Each stage ensures both functional correctness and manufacturability.

Lab Session – Day 1

Hands-on exercises performed during the lab session included:

1.Setting up the OpenLane working environment 2.Running synthesis on sample RTL designs 3.Exploring standard cell libraries 4.Analyzing floorplan parameters 5.Viewing layouts using Magic 6.Understanding configuration files used across different design stages

COMMANDS USED Terminal screenshot

Screenshot 11-28-13

Screenshot 11-34-17

Screenshot 11-38-33

Screenshot 11-38-57

SYNTHESIS SUCCESSFUL Screenshot 11-39-03

Day 2: Floorplanning Concepts and Standard Cell Placement Overview Day 2 of the workshop focused on chip floorplanning fundamentals, understanding good versus bad floorplans, and learning the basics of library cells and placement. The session combined conceptual learning with hands-on implementation using the OpenLANE ASIC flow and layout visualization through MAGIC.

Good Floorplan vs Bad Floorplan Floorplanning is a critical step in ASIC design as it directly impacts area utilization, routing quality, power distribution, and timing closure. A good floorplan enables smooth routing and scalability, while a bad floorplan can cause congestion, timing violations, and design inefficiencies.

Characteristics of a good floorplan:

Balanced utilization Adequate whitespace for routing Proper aspect ratio Efficient I/O and power structure placement Chip Floorplanning Fundamentals Core The core is the central region of the chip where all logic elements such as standard cells, macros, and IP blocks are placed. This area contains the functional logic of the design.

Die The die surrounds the core and includes I/O pads, power pads, and boundary regions. Multiple dies are fabricated on a single silicon wafer to improve manufacturing efficiency.

The core dimensions depend on the design netlist, while the die dimensions are derived from the core with additional margins.

Utilization Factor The utilization factor represents how much of the core area is occupied by logic. Utilization Factor = (Area occupied by netlist) / (Total core area)

Observations A utilization factor of 1 indicates a poor floorplan. No space is left for routing or future design changes. Practical designs maintain utilization less than 1. Aspect Ratio The aspect ratio defines the shape of the core. Aspect Ratio = (Height of core) / (Width of core)

Interpretation Aspect ratio equal to 1 represents a square core. Aspect ratio not equal to 1 represents a rectangular core. A suitable aspect ratio helps reduce congestion and improves placement efficiency. Floorplanning Examples Case 1: Fully Utilized Core Core area equals netlist area Utilization factor equals 1 Aspect ratio equals 1 Considered a poor floorplan due to lack of routing space Case 2: Optimized Core Area Core area larger than netlist area Utilization factor less than 1 Rectangular core Allows better routing and future expansion Day 2 Labs: Floorplanning Using OpenLANE Running the Floorplan The floorplanning stage was executed using the OpenLANE command:

Screenshot 11-40-00

Screenshot 11-40-42

Screenshot 11-56-00

Screenshot 12-26-48

Screenshot 12-51-14

Screenshot 12-51-31

Screenshot 12-52-31

Screenshot 13-25-45

Screenshot 13-28-41

Day 3: Inverter Characterization, Library Cells, and Routing Basics Overview Day 3 of the workshop focused on standard cell design and characterization using Sky130 model files. The session covered CMOS inverter simulation using ngspice, extraction of static and dynamic parameters, creation of layout views using MAGIC, and an introduction to LEF files, routing tracks, and DRC debugging.

CMOS Inverter Simulation Using ngspice A CMOS inverter was simulated using Sky130 device models to understand both static and dynamic behavior. DC and transient analyses were performed using ngspice.

Static Characteristics of CMOS Inverter Switching Threshold The input voltage at which the inverter output switches from logic high to logic low.

Input Low Voltage The maximum input voltage interpreted as logic 0.

Input High Voltage The minimum input voltage interpreted as logic 1.

Output Low Voltage The output voltage level corresponding to logic 0.

Output High Voltage The output voltage level corresponding to logic 1.

Noise Margins Noise margins represent the tolerance of the inverter to noise and are defined for both logic high and logic low regions.

Dynamic Characteristics of CMOS Inverter Propagation Delay The delay between a change in input and the corresponding change in output.

Rise Time The time taken by the output to transition from low to high.

Fall Time The time taken by the output to transition from high to low.

Standard Cell Design Using MAGIC Inverter Layout Creation The CMOS inverter layout was created using the MAGIC layout editor following Sky130 design rules. Proper placement of transistors, diffusion, poly, and metal layers was ensured based on the schematic.

Parasitic Extraction Extraction Process Once the layout was completed, parasitic extraction was performed to capture resistive and capacitive effects.

Day 3 Labs: Inverter Characterization Screenshot 16-02-46

Screenshot 16-02-55

Screenshot 16-06-20

Screenshot 16-18-34

Screenshot 16-18-38

Screenshot 11-44-09

Screenshot 11-49-39

Screenshot 12-16-57

Screenshot 12-54-55

Screenshot 12-57-06

Screenshot 12-58-36

Screenshot 13-02-54

Screenshot 17-08-58

Screenshot 17-16-53

Screenshot 17-16-58

Screenshot 19-52-06

Screenshot 19-52-14

Screenshot 19-52-21

Screenshot 19-52-26

Screenshot 19-53-20

Screenshot 19-53-30

Day 4: Timing-Aware Physical Design and Custom Cell Integration Session Summary The fourth day of the workshop concentrated on understanding timing behavior before routing, aligning standard cell layouts with routing tracks, and integrating a custom-designed inverter into the OpenLANE flow. The lab sessions emphasized timing optimization, LEF generation, synthesis tuning, and post-synthesis timing verification.

Pre-Routing Timing Perspective Before detailed routing begins, it is critical to evaluate timing to prevent late-stage violations. Pre-layout timing analysis allows designers to identify long paths, improper buffering, and clock-related issues early in the flow.

A well-structured clock distribution is necessary to:

Control clock skew Reduce timing uncertainty Improve overall design reliability Delay-Based Timing Representation Concept of Delay Tables Delay tables capture how much time signals take to propagate through logic cells and interconnects under different conditions. These values form the basis for estimating path delays during synthesis and placement.

Application in Design Flow Used by synthesis tools to calculate arrival and required times Helps tools choose optimal cell sizes and buffering Assists in meeting timing targets before physical routing From Layout Grids to Routing Tracks Why Track Alignment Matters Physical layouts are drawn on grids, while routing follows predefined tracks provided by the technology. Converting grid-based layouts to track-aligned designs ensures compatibility with automated routing.

Cell Layout Constraints Pins should lie on valid routing intersections Cell width must align with horizontal track pitch Cell height must match vertical track spacing Track Configuration Details Track definitions are provided through the tracks.info file, which includes:

Track pitch values Layer-specific routing directions Spacing constraints This information guides both cell layout and routing feasibility.

Day 4 Lab Work: Custom Inverter Preparation Loading the Inverter Layout The inverter layout was opened in MAGIC for inspection and modification.

Screenshot from 2025-12-14 06-42-46

Screenshot from 2025-12-14 06-43-28

Screenshot from 2025-12-14 06-46-17

Screenshot from 2025-12-14 06-52-26

Screenshot from 2025-12-14 13-17-16

Screenshot from 2025-12-14 13-33-02

Screenshot from 2025-12-14 13-33-05

Screenshot from 2025-12-14 13-35-53

Screenshot from 2025-12-14 13-52-48

Screenshot from 2025-12-14 14-00-31

Screenshot from 2025-12-14 14-22-58

Screenshot from 2025-12-14 14-23-39

Screenshot from 2025-12-14 14-28-17

Screenshot from 2025-12-14 14-28-25

Screenshot from 2025-12-14 14-32-37

Screenshot from 2025-12-14 14-32-45

Screenshot from 2025-12-14 19-48-14

Screenshot from 2025-12-14 20-34-20

Screenshot from 2025-12-14 20-34-13

Screenshot from 2025-12-14 19-50-02

Screenshot from 2025-12-14 19-49-57

Screenshot from 2025-12-14 19-49-52

Screenshot from 2025-12-14 19-49-45

Screenshot from 2025-12-14 19-49-39

Screenshot from 2025-12-14 19-49-32

Screenshot from 2025-12-14 19-49-13

Screenshot from 2025-12-14 19-48-29

Screenshot from 2025-12-14 19-48-23

Screenshot 2025-12-14 21-02-32

Day 5: Power Planning, Routing, and GDSII Generation Overview The final day of the workshop focused on completing the physical design flow by generating the Power Distribution Network (PDN), performing routing, validating timing after routing, and producing the final GDSII file for fabrication. This stage marks the transition from design implementation to tape-out readiness.

Power Distribution Network in OpenLANE Role of PDN A Power Distribution Network ensures reliable delivery of power and ground to every standard cell and macro within the chip. A well-designed PDN minimizes voltage drop, improves signal integrity, and enhances overall chip stability.

The PDN primarily distributes:

VDD (power) VSS (ground) across the core using rails and straps.

PDN Generation Flow gen_pdn Execution OpenLANE provides the gen_pdn procedure to automatically generate the power grid. This step constructs horizontal and vertical power rails and connects them to all power pins in the design.

The PDN stage relies on predefined technology and library information to maintain compatibility with the routing and placement stages.

PDN Configuration Dependencies Required Variables Before executing PDN generation, certain configuration variables must be correctly defined.

LIB_SYNTH_COMPLETE This variable must be present in the config.tcl file. It is internally referenced by the PDN scripts to access complete synthesis libraries.

LEF_MERGED_UNPADDED This variable points to the merged LEF file without padding. It provides structural information required for power grid creation.

Improper configuration of these variables may cause PDN generation to fail.

Routing Stage Preparing for Routing Before initiating routing, key routing-related variables were inspected to confirm the current design state.

Screenshot from 2025-12-14 22-34-31
