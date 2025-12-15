# soc-design-and-planning-nasscom-vsd
A two-week hands-on workshop on Digital VLSI SoC Design and Planning, covering the complete RTL-to-GDSII flow, conducted by VSD in association with NASSCOM, focusing on advanced physical design using OpenLANE and the SKY130 process.

# Day 1: Introduction to RTL to GDSII and Open-Source ASIC Design Overview of the RTL to GDSII Flow

The RTL to GDSII flow represents the complete journey of a digital design, starting from a high-level behavioral description and ending with a manufacturable physical layout. This flow includes major stages such as RTL synthesis, floorplanning, placement, clock tree synthesis, routing, and multiple verification steps. The primary goal is to ensure that the final layout faithfully implements the intended logic, meets timing constraints, and complies with foundry design rules.

Design Abstraction in VLSI and the Y-Chart Model:-

A key theoretical concept introduced was design abstraction in VLSI systems. The Y-Chart model explains how a design evolves across three domains: a.Behavioral domain – functional description of the system b.Structural domain – organization of components and interconnections c.Geometric domain – physical representation of the design

Chip Structure and Major Components:-

The internal structure of an integrated circuit was discussed in detail, covering the following elements: 1.Core The region containing standard cells, IP blocks, combinational and sequential logic, and internal routing. 2.Die The physical silicon area that houses the core along with peripheral structures. Multiple dies are fabricated on a single wafer. 3.I/O Pads Interfaces that connect internal signals to the external package, including input, output, bidirectional, and power pads. 4.IP Blocks Pre-designed modules such as SRAMs, PLLs, ADCs, and DACs, typically provided by foundries due to their design complexity. 5.Process Design Kit (PDK) The PDK serves as the link between EDA tools and fabrication technology. It contains device models, design rule files, layout layers, and standard cell libraries. The workshop used the SkyWater 130 nm PDK (sky130_fd_sc_hd).

# Introduction to RISC-V Architecture:-

RISC-V is an open and extensible Instruction Set Architecture (ISA). The ISA defines how software instructions are executed by hardware. Its open nature makes it widely adopted in both academic research and industrial processor development.

The software toolchain plays a critical role in execution, where high-level programming languages are translated into machine instructions through compilers, assemblers, and the operating system.

Software-to-Hardware Execution Flow:-

An overview of how software interacts with hardware was presented: 1.Application Layer – user-level programs 2.Operating System – manages system resources and hardware interaction 3.Compiler – converts high-level code into machine instructions 4.Assembler – encodes instructions into binary format

This flow establishes a direct link between application software and the processor microarchitecture.

# Open-Source ASIC Design Ecosystem:-

The workshop highlighted the essential components required for a complete ASIC design environment: 1.RTL design files 2.EDA tools such as Yosys, OpenROAD, Magic, Netgen, and KLayout 3.PDK data OpenLane integrates these tools into a unified, automated flow, enabling end-to-end digital ASIC design using open-source resources.

# Simplified RTL to GDSII Design Stages:-

The digital implementation flow was broken down into the following steps: 
1.Synthesis Conversion of RTL code into a gate-level netlist using standard cells provided in multiple formats (Verilog, Liberty, LEF, SPICE, and GDS).

2.Floorplanning and Power Planning Definition of core dimensions, pin locations, macro placement, and power distribution networks including rings, straps, and rails.

3.Placement Arrangement of standard cells within rows: a.Global placement for rough positioning b.Detailed placement for legal and optimized alignment

4.Clock Tree Synthesis (CTS) Creation of a balanced clock network to minimize skew using structures such as H-trees or X-trees.

5.Routing a.Global routing to generate routing guides b.Detailed routing to implement final metal connections based on PDK rules

6.Sign-off Checks Final verification stages include: a.Design Rule Check (DRC) b.Layout vs Schematic (LVS) c.Parasitic extraction and Static Timing Analysis (STA) d.Antenna checks and prevention techniques OpenLane initially inserts fake diodes for antenna prevention and replaces them with real diodes if violations persist after routing.

# Detailed OpenLane Flow:-

The complete OpenLane automation flow consists of: 
1.RTL synthesis using Yosys and ABC 

2.Static timing analysis 

3.Optional DFT insertion using FAULT 

4.Floorplan and powerplan generation 

5.Placement and post-placement optimization 

6.Clock tree synthesis 

7.Routing 

8.Physical verification using Magic and Netgen 

9.Final GDSII generation Each stage ensures both functional correctness and manufacturability.

# Lab Session – Day 1

Hands-on exercises performed during the lab session included:

1.Setting up the OpenLane working environment 

2.Running synthesis on sample RTL designs 

3.Exploring standard cell libraries 

4.Analyzing floorplan parameters 

5.Viewing layouts using Magic 

6.Understanding configuration files used across different design stages

# COMMANDS USED Terminal screenshot

![image alt](https://github.com/Gobika404/NASSCOM-VSD-SoC--design-and--Planning-Program/blob/main/Screenshot%20from%202025-12-12%2011-25-56.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-15%2012-55-47.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-17-47.png?raw=true)

SYNTHESIS SUCCESSFUL Screenshot

# Day 2: Floorplanning Concepts and Standard Cell Placement Overview Day 2 of the workshop focused on chip floorplanning fundamentals, understanding good versus bad floorplans, and learning the basics of library cells and placement. The session combined conceptual learning with hands-on implementation using the OpenLANE ASIC flow and layout visualization through MAGIC.

Good Floorplan vs Bad Floorplan Floorplanning is a critical step in ASIC design as it directly impacts area utilization, routing quality, power distribution, and timing closure. A good floorplan enables smooth routing and scalability, while a bad floorplan can cause congestion, timing violations, and design inefficiencies.

Characteristics of a good floorplan:

Balanced utilization Adequate whitespace for routing Proper aspect ratio Efficient I/O and power structure placement Chip Floorplanning Fundamentals Core The core is the central region of the chip where all logic elements such as standard cells, macros, and IP blocks are placed. This area contains the functional logic of the design.

Die The die surrounds the core and includes I/O pads, power pads, and boundary regions. Multiple dies are fabricated on a single silicon wafer to improve manufacturing efficiency.

The core dimensions depend on the design netlist, while the die dimensions are derived from the core with additional margins.

Utilization Factor The utilization factor represents how much of the core area is occupied by logic. Utilization Factor = (Area occupied by netlist) / (Total core area)

Observations A utilization factor of 1 indicates a poor floorplan. No space is left for routing or future design changes. Practical designs maintain utilization less than 1. Aspect Ratio The aspect ratio defines the shape of the core. Aspect Ratio = (Height of core) / (Width of core)

Interpretation Aspect ratio equal to 1 represents a square core. Aspect ratio not equal to 1 represents a rectangular core. A suitable aspect ratio helps reduce congestion and improves placement efficiency. Floorplanning Examples Case 1: Fully Utilized Core Core area equals netlist area Utilization factor equals 1 Aspect ratio equals 1 Considered a poor floorplan due to lack of routing space Case 2: Optimized Core Area Core area larger than netlist area Utilization factor less than 1 Rectangular core Allows better routing and future expansion Day 2 Labs: Floorplanning Using OpenLANE Running the Floorplan The floorplanning stage was executed using the OpenLANE command:

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-15%2012-56-48.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2011-54-25.png?raw=true)

![image alt](https://github.com/Gobika404/NASSCOM-VSD-SoC--design-and--Planning-Program/blob/main/Screenshot%20from%202025-12-12%2012-52-31.png)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2011-52-15.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2012-11-35.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2012-11-53.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2012-12-26.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2012-13-41.png?raw=true)

# Screenshot of placement run

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2014-47-34.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2015-19-59.png?raw=true)

# Day 3: Inverter Characterization, Library Cells, and Routing Basics Overview Day 3 of the workshop focused on standard cell design and characterization using Sky130 model files. The session covered CMOS inverter simulation using ngspice, extraction of static and dynamic parameters, creation of layout views using MAGIC, and an introduction to LEF files, routing tracks, and DRC debugging.

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

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2018-48-29.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2018-49-09.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2010-52-12.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2010-54-22.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2010-54-47.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-07-35.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-08-17.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-34-26.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-46-37.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-46-41.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-46-56.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-10-08.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-13-00.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-28-07.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-48-31.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-58-43.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-59-20.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-59-57.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2013-11-35.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2013-14-10.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2013-17-20.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2020-09-16.png?raw=true)

Day 4: Timing-Aware Physical Design and Custom Cell Integration Session Summary The fourth day of the workshop concentrated on understanding timing behavior before routing, aligning standard cell layouts with routing tracks, and integrating a custom-designed inverter into the OpenLANE flow. The lab sessions emphasized timing optimization, LEF generation, synthesis tuning, and post-synthesis timing verification.

Pre-Routing Timing Perspective Before detailed routing begins, it is critical to evaluate timing to prevent late-stage violations. Pre-layout timing analysis allows designers to identify long paths, improper buffering, and clock-related issues early in the flow.

A well-structured clock distribution is necessary to:

Control clock skew Reduce timing uncertainty Improve overall design reliability Delay-Based Timing Representation Concept of Delay Tables Delay tables capture how much time signals take to propagate through logic cells and interconnects under different conditions. These values form the basis for estimating path delays during synthesis and placement.

Application in Design Flow Used by synthesis tools to calculate arrival and required times Helps tools choose optimal cell sizes and buffering Assists in meeting timing targets before physical routing From Layout Grids to Routing Tracks Why Track Alignment Matters Physical layouts are drawn on grids, while routing follows predefined tracks provided by the technology. Converting grid-based layouts to track-aligned designs ensures compatibility with automated routing.

Cell Layout Constraints Pins should lie on valid routing intersections Cell width must align with horizontal track pitch Cell height must match vertical track spacing Track Configuration Details Track definitions are provided through the tracks.info file, which includes:

Track pitch values Layer-specific routing directions Spacing constraints This information guides both cell layout and routing feasibility.

Day 4 Lab Work: Custom Inverter Preparation Loading the Inverter Layout The inverter layout was opened in MAGIC for inspection and modification.

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-03-25.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-05-02.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-08-18.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-17-23.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-18-58.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-21-26.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-35-16.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-39-37.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-40-12.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-40-47.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-59-30.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-01-07.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-01-13.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-03-24.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-03-59.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-04-52.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-06-32.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-07-16.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-08-14.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-11-56.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-12-32.png?raw=true)

![image alt](https://private-user-images.githubusercontent.com/63997454/316688036-8c917d87-5507-4079-ba6b-facbf18c238f.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY2ODgwMzYtOGM5MTdkODctNTUwNy00MDc5LWJhNmItZmFjYmYxOGMyMzhmLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQ1N2MyM2Q2ODU5NmUyN2I1NGQ0ZWNhOTBkZjk2ZThjODJjOGI1Y2UyMjg2MGQ2ZmY4NWNkMWE0ZWExZGY2MjUmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.w9fnbrDrfn5CGRk5HFECG6xc1X73FH6z_WPx3y_AI8U)

![image alt](https://private-user-images.githubusercontent.com/63997454/316692010-32def177-5173-4dd7-ba3b-44e37846644c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY2OTIwMTAtMzJkZWYxNzctNTE3My00ZGQ3LWJhM2ItNDRlMzc4NDY2NDRjLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWM5ZTNhM2I2MzcxODQ0Y2RkYTI4MjQzZmVhZTFkY2FhNTBhNmIyMjc3MGY0ZjQ4ZWI5YTNiZDM0YjMwMzk0MjgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.YBGEkEPC2dF9saluJ8eD2qpmo2PR6NsOoFzKPb6dpwQ)

![image alt](https://private-user-images.githubusercontent.com/63997454/316692048-aa1d50b0-9cb1-45bf-a641-b64842166b48.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY2OTIwNDgtYWExZDUwYjAtOWNiMS00NWJmLWE2NDEtYjY0ODQyMTY2YjQ4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTc4NjdjMTVmNDdjMGIwOTJjODQzOTg5MDc5ZGUwN2QxYzJhMjFlZjg1Y2Q3NDgyMTA3NGMwZGIzNTBjNjY1MTcmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.xPcWVCwy30mM8R_jIS55ze9YhCBy1jT01bLBgPQeAp0)

![image alt](https://private-user-images.githubusercontent.com/63997454/316691659-0f3247fc-aaad-4e98-b23e-bdc9a361d08c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY2OTE2NTktMGYzMjQ3ZmMtYWFhZC00ZTk4LWIyM2UtYmRjOWEzNjFkMDhjLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWUzNzZlMGNjOWQyMDM5ZGJmNDdmZTM1NTZmOTQ4ZDkwOGFmOWUyZDFhOWEzMjQwNGUwYWY0ZWFkZmUxNGNmZmYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.EwXkh-xSC_kW96OLHOFoEE1UlaBC_09p73DzV-ujb5A)

![image alt](https://private-user-images.githubusercontent.com/63997454/316696607-73c58332-a212-4a24-b853-e8cae3b385a6.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY2OTY2MDctNzNjNTgzMzItYTIxMi00YTI0LWI4NTMtZThjYWUzYjM4NWE2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTZiOTY0MWQ1ODZlNWQ1YzFkZmQ3OTY1MzkxODYwZjljMzc4YTdiZWZhYTYxZDg2NmEyMTRhYTM4NDIyNzRlMDgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.fqaQ5IEbwhPRQTyWsA3iSwJGM6SSVSJeR3E_laOovKA)

![image alt](https://private-user-images.githubusercontent.com/63997454/316697619-c50c6023-1836-468d-a8c3-955b02e4224c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY2OTc2MTktYzUwYzYwMjMtMTgzNi00NjhkLWE4YzMtOTU1YjAyZTQyMjRjLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWFlNjIyMGZkYTMxMzgxOWY0YTFhNThiMGQxNTM5ZWMwMGZkMTk2MzQ1Y2IwZWJjNGEwODE3NWU1ZWZlYzEwOGYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.eH_vg9-3-2IUeDTvRFANVH2ItndDpLo0KNqel4qSfwg)

![image alt](https://private-user-images.githubusercontent.com/63997454/316726528-df3dba3c-9445-4d51-9842-bf4410f05cf5.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY3MjY1MjgtZGYzZGJhM2MtOTQ0NS00ZDUxLTk4NDItYmY0NDEwZjA1Y2Y1LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPThiY2MyZDQxOGZlODAzZjI0ODkzNDJhOWM5OTBlODc0NDQ5ZTJiMTU0NjNhYjc0OTNkMGRkZmVkOTViMTg3ZTEmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.4kDGlylEpVGAd5RIqYE1pZjfcLqBO69WqRy3Spm-aBQ)

![image alt](https://private-user-images.githubusercontent.com/63997454/316727221-3f66eed9-c43d-483e-ab85-21d70452b81f.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY3MjcyMjEtM2Y2NmVlZDktYzQzZC00ODNlLWFiODUtMjFkNzA0NTJiODFmLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTgyMTZjNzFlMTg1ZjU5OTE5ZjM0MWFmN2U3ZDc2Yjk1N2E5OWRmM2YzZTE3MWU5YjdhZDRjYzJkMGE5ZjA3Y2ImWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.2qI3o7SDPPPOJDB7Y8mhGsPcD7uRuqNoc5x2HuFR9tc)

![image alt](https://private-user-images.githubusercontent.com/63997454/316733398-7669eeef-7b93-4cfd-a152-17eec772496a.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY3MzMzOTgtNzY2OWVlZWYtN2I5My00Y2ZkLWExNTItMTdlZWM3NzI0OTZhLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTM3NTc3N2NlMTJmNWE3ODU4N2FjZjQ5NjU0MDZjYTc1NWMxY2YzMDU4YTVmMTZlZjk4ZDAxMWQyY2JmMjUxZDMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.miwrbqTLOuIHrBt7W8xEl9MtvGXzP_HWGv8go-y1e6A)

![image alt](https://private-user-images.githubusercontent.com/63997454/316798241-b13997fd-296c-4213-b4f9-8f66a7375e47.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY3OTgyNDEtYjEzOTk3ZmQtMjk2Yy00MjEzLWI0ZjktOGY2NmE3Mzc1ZTQ3LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWViZmYzYzYwMGQ3NTM0OGNhNmViYWMwOGJjNWQ1NmMzMjQxODc2OGVjOTExMjRkZTlhNTBmNTdiZDI0ZjE2ZmQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.RNFlom4B5yvdQTuawLzbv-5_kW0S7S0XifYmvifM7-Q)

![image alt](https://private-user-images.githubusercontent.com/63997454/316798674-79b5f158-acf4-4065-a0ec-61007ab465d0.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY3OTg2NzQtNzliNWYxNTgtYWNmNC00MDY1LWEwZWMtNjEwMDdhYjQ2NWQwLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWViY2JhOGZlM2RjNWVkYjFjM2UxYjg5NDU0ZGE4NDAxOThlMTJjN2ZiOTM0ZjgzMDYyNGY2NzViZWViNTk1ZWUmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.5wIwqKyUnxW4-yMHXZnK63ZYybtEipAB2CqOObvbc_o)

![image alt](https://private-user-images.githubusercontent.com/63997454/316799666-bee921ce-03d5-49fb-a9fc-bcc6e3402f8c.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY3OTk2NjYtYmVlOTIxY2UtMDNkNS00OWZiLWE5ZmMtYmNjNmUzNDAyZjhjLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWExZDE3MTBkNWI1ZGJmN2E1NjA5MWI2NDU5OTJhYTEzYzY2NmIyMTc5Y2NmMzkwMTU2M2IyYjA2ZmRmMThiZmMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.ZE3LG3HwXMXy06GP0mjy_Dzq_3hGbeQrRd5K150esx8)

![image alt](https://private-user-images.githubusercontent.com/63997454/316819803-6eade230-eb96-4d7b-b7a9-7a7db9c2c8b7.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY4MTk4MDMtNmVhZGUyMzAtZWI5Ni00ZDdiLWI3YTktN2E3ZGI5YzJjOGI3LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTU2OGIxMzQ4MmEyMWI3NWNkYTc4MDdkNjFjOGQ5YjEwZWExNzY3YjUyYmM2ZjNhZjlmYTNiZTgzNzYzMDI0OWMmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.CVYpNUyOVX2KTZK1tnGlgEDon5ymA4hRhPJ-3s3uaXw)

![image alt](https://private-user-images.githubusercontent.com/63997454/316819525-b1900c55-7470-41b2-8b4f-3af871494d99.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3NjU3OTA2MjYsIm5iZiI6MTc2NTc5MDMyNiwicGF0aCI6Ii82Mzk5NzQ1NC8zMTY4MTk1MjUtYjE5MDBjNTUtNzQ3MC00MWIyLThiNGYtM2FmODcxNDk0ZDk5LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNTEyMTUlMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjUxMjE1VDA5MTg0NlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWMyYzgyODEwYzVlZTk1ODQxZmUwZWI3NDM0NTE2ZmM0N2I1NjkwZjcwYmE0ZjZmZWU0NDU2MTJkMjZjMjViODUmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.MD8jYuns8Seos4TzmvxbJ3AudrluLBd-vMPKF6ZyOQw)

# Day 5: Power Planning, Routing, and GDSII Generation Overview The final day of the workshop focused on completing the physical design flow by generating the Power Distribution Network (PDN), performing routing, validating timing after routing, and producing the final GDSII file for fabrication. This stage marks the transition from design implementation to tape-out readiness.

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

![image alt](https://github.com/Gobika404/NASSCOM-VSD-SoC--design-and--Planning-Program/raw/main/Screenshot%20from%202025-12-14%2022-34-31.png)
