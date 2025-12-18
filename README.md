# soc-design-and-planning-nasscom-vsd
A two-week hands-on workshop on Digital VLSI SoC Design and Planning, covering the complete RTL-to-GDSII flow, conducted by VSD in association with NASSCOM, focusing on advanced physical design using OpenLANE and the SKY130 process.

# Day 1: Introduction to RTL to GDSII and Open-Source ASIC Design Overview of the RTL to GDSII Flow

The RTL to GDSII flow represents the complete journey of a digital design, starting from a high-level behavioral description and ending with a manufacturable physical layout. This flow includes major stages such as RTL synthesis, floorplanning, placement, clock tree synthesis, routing, and multiple verification steps. The primary goal is to ensure that the final layout faithfully implements the intended logic, meets timing constraints, and complies with foundry design rules.

# How to talk to computers

Talking to a computer means giving some set of instructions in a form that hardware understands and whose hardware is based on RISC-V core. If you want to run a software/ Programming code like C,C++ or java it can be easily understandable by humans, but the hardware cannot understand it. So the compiler converts high level code to RISC-V instructions which processor can decode.

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%202025-12-18%20125429.png?raw=true)

# SoC Design and Openlane

A System-on-Chip (SoC) integrates multiple components of a computer or electronic system into a single silicon die. A typical SoC contains, Processor, Memory Subsystem, Pheripherals, Bus architecture. To design the ASIC, it requires ASIC flow. The objective of this ASIC flow is to convert RTL to GDSII for the final layout. The whole ASIC flow is automated using EDA tools which is a software automatically does place & Route.

# RTL to GDSII flow

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%202025-12-18%20124752.png?raw=true)

1. Synthesis: The code written by the RTL designers cannot be directly Physically implemented on the chip, so synthesis is a process where the RTL code is converted into gate-level netlist using standard cell libraries which can be easily understandable by EDA tools

2. Floor Planning: It’s the process of creating the area of chip using aspect ratio and utilization factor, placement of macro cells, creating power grids and adding decap cells/ physical cells

3. Placement: Placement is process where the standard cells are placed in optimal positions basically in assigned floor plan and ensures to reduce congestion. Placement is done in two stages

a.Global Placement: Cells are placed at optimal positions, there might be overlapps

b.Detailed Placement: Cells are placed at legal positions with no overlaps

4. Routing: Routing is making connections between the standard cells. It done in two phases one is

a.Global Routing

b.Detailed Routing

5. Sign off: Sign off is the last stage of Physical design flow where it verifies layout satisfies the rules for manufacturing process like DRC, LVS and Timing verifications.

# OpenLane ASIC flow

The openLane ASIC flow is as follows:

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%202025-12-18%20124726.png?raw=true)

# Get familiar to Open-source EDA

Before mastering opensource EDA tools, the first and foremost thing is to get familiar with basic linux commands to communicate with the open source software on Linux environment. Some of the basic commands are mentioned below

    cd file name: takes to the directory “filename:

    ls -ltr: list the files/ directories

    cd ../: exits from the directory

    pwd: prints the current directory

    cp: copy files to the active directory

    Command --help: shows the use of the command

     clear: clears the screen

In our design flow, we use the Sky130_fd_sc_hd PDK variant. This naming convention describes important details about the process and the type of standard-cell library included.

1.sky130 → Refers to the SkyWater 130 nm technology node.

2.fd → Indicates the foundry designation, meaning this PDK is released by SkyWater Foundry.

3.sc → Stands for standard cell library, which provides the logic cells required for digital design.

4.hd → Represents the high-density variant of the standard-cell library. This library prioritizes smaller cell area, enabling higher logic density at the cost of drive strength.

The Sky130_fd_sc_hd PDK contains a wide range of technology files used at different stages of the digital ASIC flow. Some important file types are Verilog files, lef lifes, tech files, lib files. The Sky130_fd_sc_hd library provides all the necessary functional, timing, and physical data required for RTL-to-GDSII implementation.

# Design Abstraction in VLSI and the Y-Chart Model:-

A key theoretical concept introduced was design abstraction in VLSI systems. The Y-Chart model explains how a design evolves across three domains: a.Behavioral domain – functional description of the system b.Structural domain – organization of components and interconnections c.Geometric domain – physical representation of the design

# Chip Structure and Major Components:-

The internal structure of an integrated circuit was discussed in detail, covering the following elements: 

1.Core The region containing standard cells, IP blocks, combinational and sequential logic, and internal routing. 

2.Die The physical silicon area that houses the core along with peripheral structures. Multiple dies are fabricated on a single wafer. 

3.I/O Pads Interfaces that connect internal signals to the external package, including input, output, bidirectional, and power pads. 

4.IP Blocks Pre-designed modules such as SRAMs, PLLs, ADCs, and DACs, typically provided by foundries due to their design complexity. 

5.Process Design Kit (PDK) The PDK serves as the link between EDA tools and fabrication technology. 
It contains device models, design rule files, layout layers, and standard cell libraries. The workshop used the SkyWater 130 nm PDK (sky130_fd_sc_hd).

# Introduction to RISC-V Architecture:-

RISC-V is an open and extensible Instruction Set Architecture (ISA). The ISA defines how software instructions are executed by hardware. Its open nature makes it widely adopted in both academic research and industrial processor development.

The software toolchain plays a critical role in execution, where high-level programming languages are translated into machine instructions through compilers, assemblers, and the operating system.

# Software-to-Hardware Execution Flow:-

An overview of how software interacts with hardware was presented: 

1.Application Layer – user-level programs

2.Operating System – manages system resources and hardware interaction

3.Compiler – converts high-level code into machine instructions

4.Assembler – encodes instructions into binary format

This flow establishes a direct link between application software and the processor microarchitecture.

# Open-Source ASIC Design Ecosystem:-

The workshop highlighted the essential components required for a complete ASIC design environment: 

1.RTL design files 

2.EDA tools such as Yosys, OpenROAD, Magic, Netgen, and KLayout 

3.PDK data OpenLane integrates these tools into a unified, automated flow, enabling end-to-end digital ASIC design using open-source resources.

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

Design preparation steps to invoke openlane

To invoke open lane, first the terminal should be opened in openlane working directory. Once the path is created the openlane can be invoked by the following commands

  Step 1: Navigate to OpenLANE Directory
  
    cd Desktop/work/tools/openlane_working_dir/openlane
 
 Step 2: Start OpenLANE in Interactive Mode
       
       ./flow.tcl -interactive

Step 3: Load OpenLANE Package

     package require openlane 0.9

Step 4: Prepare the picorv32a Design

        prep -design picorv32a

![image alt](https://github.com/Gobika404/NASSCOM-VSD-SoC--design-and--Planning-Program/blob/main/Screenshot%20from%202025-12-12%2011-25-56.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-15%2012-55-47.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-17-47.png?raw=true)

SYNTHESIS SUCCESSFUL Screenshot

# Day 2 of the workshop explored the fundamentals of chip floorplanning. 

Highlighting the characteristics of effective and ineffective floorplans. The session also introduced standard cell libraries and the basics of placement, combining theoretical concepts with practical experience using the OpenLANE ASIC flow and layout visualization in MAGIC.

# Good Floorplan vs Bad Floorplan 

Floorplanning is a critical step in ASIC design as it directly impacts area utilization, routing quality, power distribution, and timing closure. A good floorplan enables smooth routing and scalability, while a bad floorplan can cause congestion, timing violations, and design inefficiencies.

# Characteristics of a good floorplan:

Balanced utilization Adequate whitespace for routing Proper aspect ratio Efficient I/O and power structure placement Chip Floorplanning Fundamentals Core The core is the central region of the chip where all logic elements such as standard cells, macros, and IP blocks are placed. This area contains the functional logic of the design.

Die The die surrounds the core and includes I/O pads, power pads, and boundary regions. Multiple dies are fabricated on a single silicon wafer to improve manufacturing efficiency.

The core dimensions depend on the design netlist, while the die dimensions are derived from the core with additional margins.

# Utilization Factor 

The utilization factor represents how much of the core area is occupied by logic. Utilization Factor = (Area occupied by netlist) / (Total core area)

Observations A utilization factor of 1 indicates a poor floorplan. No space is left for routing or future design changes. Practical designs maintain utilization less than 1. Aspect Ratio The aspect ratio defines the shape of the core. Aspect Ratio = (Height of core) / (Width of core)

# Interpretation 
Aspect ratio equal to 1 represents a square core. 

Aspect ratio not equal to 1 represents a rectangular core. 

A suitable aspect ratio helps reduce congestion and improves placement efficiency. 

# Floorplanning Examples 

# Case 1: Fully Utilized Core 

1.Core area equals netlist area 

2.Utilization factor equals 1 

3.Aspect ratio equals 1 

4.Considered a poor floorplan due to lack of routing space 

# Case 2: Optimized Core Area 

1.Core area larger than netlist area 

2.Utilization factor less than 1 

3.Rectangular core 

4.Allows better routing and future expansion 

# Day 2 Labs: Floorplanning Using OpenLANE Running the Floorplan The floorplanning stage was executed using the OpenLANE command:

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

# Day 3 of the workshop concentrated on standard cell design and characterization using Sky130 model files. 

Simulated CMOS inverters with ngspice, analyzed key static and dynamic parameters, created layout views in MAGIC, and gained an introduction to LEF files, routing tracks, and DRC error analysis.

# CMOS inverter Switching threshold (Vm)
It can be defined as the point on transfer characteristics plot where Vin equals vout. At this point bot PMOS and NMOS will be in ON state leading to rise in leakage current

# CMOS fabrication process

1. Substrate selection Selecting the substrate material.

2. Well Formation Create N-well and P-well regions where PMOS and NMOS transistors will be placed.

3. Isolation Form isolation regions (oxide trenches) to separate transistors on the wafer.

4. Gate Formation Grow a thin gate oxide and deposit/pattern polysilicon to create the transistor gate.

5. Source/Drain Formation Dope the regions on both sides of the gate to form source and drain terminals.

6. Contact Creation Open small holes (contacts) in the insulating layer so metal can touch the transistor terminals.

7. Metallization Deposit and pattern metal layers to connect different devices and form interconnects.

8. Passivation Add a protective top layer and open windows for bonding pads used in packaging.

# CMOS Inverter Simulation Using ngspice 

A CMOS inverter was simulated using Sky130 device models to understand both static and dynamic behavior. DC and transient analyses were performed using ngspice.

# Static Characteristics of CMOS Inverter 

# Switching Threshold 
The input voltage at which the inverter output switches from logic high to logic low.

# Input Low Voltage 
The maximum input voltage interpreted as logic 0.

# Input High Voltage 
The minimum input voltage interpreted as logic 1.

# Output Low Voltage 
The output voltage level corresponding to logic 0.

# Output High Voltage 
The output voltage level corresponding to logic 1.

# Noise Margins 
Noise margins represent the tolerance of the inverter to noise and are defined for both logic high and logic low regions.

# Dynamic Characteristics of CMOS Inverter 

# Propagation Delay 
The delay between a change in input and the corresponding change in output.

# Rise Time 
The time taken by the output to transition from low to high.

# Fall Time
The time taken by the output to transition from high to low.

# Standard Cell Design Using MAGIC 

# Inverter Layout Creation 
The CMOS inverter layout was created using the MAGIC layout editor following Sky130 design rules. Proper placement of transistors, diffusion, poly, and metal layers was ensured based on the schematic.

# Parasitic Extraction 
Extraction Process Once the layout was completed, parasitic extraction was performed to capture resistive and capacitive effects.

# Day 3 Labs: Inverter Characterization Screenshots

# Lab steps to git clone vsdstd cell design
To clone the standard cell, copy the file path from github repository and paste it in the openlane directory after initiating the command git clone. The file path to clone the std cell is as follows

    # Change directory to openlane
    cd Desktop/Openlane

    # Clone the repository with custom inverter design
    git clone https://github.com/nickson-jose/vsdstdcelldesign

    # Change into repository directory
    cd vsdstdcelldesign

    # Copy magic tech file to the repo directory for easy access
     cp /home/user/Desktop/openlane/pdks/sky130A/libs.tech/magic/sky130A.tech .

    # Check contents whether everything is present
     ls

    # Command to open custom inverter layout in magic
    magic -T sky130A.tech sky130_inv.mag &

This creates vsdstd cell design in openlane directory

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2018-48-29.png?raw=true)

if we go into the vsdstd cell directory, you can see .mag file, libs file and so on. Now let’s view .mag file see what layers are used to build the inverter. So, to view the file we need technology file. So, we will copy the file from given address. Now the file is copied to vsdstd cell design folder

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-10%2018-49-09.png?raw=true)

If we want to know the information about the layers, click on the area and press and type what in tckon window, similarly we can check for output terminal also, but double pressing “S”

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2010-52-12.png?raw=true)

Lab steps to create std cell layout and extract spice netlist

To extract spice netlist, input command extract all to tckon window. It extracts the spice netlist

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2010-54-22.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2010-54-47.png?raw=true)

          # Check current directory
           pwd

          # Extraction command to extract to .ext format
           extract all

          # Before converting ext to spice this command enable the parasitic extraction also
           ext2spice cthresh 0 rthresh 0

          # Converting to ext to spice
           ext2spice

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-07-35.png?raw=true)

lets go to the vsdstd cell directory and check whether the spice netlist is extracted or not.

we will use this .ext file to extract the spice file to use with ngspice tool to verify the transfer characteristics. For extract the ngspice input the commands ext2spice cthresh 0 r thresh 0 followed by ext2spice

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-08-17.png?raw=true)

In the generated spicefile, we can see all the details about the NMOS and PMOS connectivity and information about the power also.

Now, we need to modify the ngspice file to simulate and view the results. So we include this file in terminal by .include.libs/pshort.lib and.include.libs/shsort.lib command

Set power supply VDD to 3.3V by assigning VDD VPWR 0 3.3V, and also add command to do transient analysis over certain time like. tran 1n 20n.

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-34-26.png?raw=true)

Now plotting the graph here by command, plot y vs time a

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-46-37.png?raw=true)

Now if we increase the C3 value from 0.00174ff to 2ff, the graph will look like this, it observed that the graph becomes smoother.

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-46-41.png?raw=true)

Lab steps to characterize inverter using sky130 model files

Here we calculate the values of parameters

1.Rise time

Rise time is defined as the time taken to reach 20% value to 80% value.

So, the rise time = (5.72289-6.15663) e-09= 77.54psec

2.Fall time

It is time taken by output for transition from 80% to 20%

So, the fall time= (4.08434-2.09639) e-09= 19.9psec

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2011-46-56.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-10-08.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-13-00.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-28-07.png?raw=true)

  Use the command magic -d XR

To open the magic tool. Open met3.mag file from the file menu. We can see different layouts with different DRC values.

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-48-31.png?raw=true)

# Lab introduction to magic tool options and DRC rules
The technology file is set if rues that declares layers, types and electrical connectivity, DRC, device extraction rules, and rules to read lef and def files. It can be sourced from opencircuitdesign.com using the below path ‘
                                        
                           wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
                                                 
                            tar xfz drc_tests.tgz
                            
![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-58-43.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-59-20.png?raw=true)

To check for vias in the metal3 layer, make a rectangluar selection in an empty space and paint it with the m3contact color from the color palette by clicking middle mouse button. The vias can be viewed by: cif see VIA2

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2012-59-57.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2013-11-35.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2013-14-10.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2013-17-20.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-11%2020-09-16.png?raw=true)

# Day 4 focused on timing-aware physical design, with an emphasis on analyzing timing behavior prior to routing and aligning standard cell layouts with routing tracks. 

The session also covered integrating a custom inverter into the OpenLANE flow, supported by hands-on labs involving timing optimization, LEF generation, synthesis tuning, and post-synthesis timing verification.

# Pre-Routing Timing Perspective 
Before detailed routing begins, it is critical to evaluate timing to prevent late-stage violations. Pre-layout timing analysis allows designers to identify long paths, improper buffering, and clock-related issues early in the flow.

A well-structured clock distribution is necessary to:

1.Control clock skew 

2.Reduce timing uncertainty 

3.Improve overall design reliability 

# Delay-Based Timing Representation 

# Concept of Delay Tables 
Delay tables capture how much time signals take to propagate through logic cells and interconnects under different conditions. These values form the basis for estimating path delays during synthesis and placement.

# Application in Design Flow 

1.Used by synthesis tools to calculate arrival and required times 

2.Helps tools choose optimal cell sizes and buffering 

3.Assists in meeting timing targets before physical routing 

# From Layout Grids to Routing Tracks 

# Why Track Alignment Matters 

Physical layouts are drawn on grids, while routing follows predefined tracks provided by the technology. Converting grid-based layouts to track-aligned designs ensures compatibility with automated routing.

# Cell Layout Constraints 

1.Pins should lie on valid routing intersections 

2.Cell width must align with horizontal track pitch 

3.Cell height must match vertical track spacing 

# Track Configuration Details 

Track definitions are provided through the tracks.info file, which includes:

1.Track pitch values 

2.Layer-specific routing directions 

3.Spacing constraints 

This information guides both cell layout and routing feasibility.

# Day 4 Lab Work: Custom Inverter Preparation Loading the Inverter Layout The inverter layout was opened in MAGIC for inspection and modification.

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-03-25.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-05-02.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-08-18.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-17-23.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-18-58.png?raw=true)

# Standard cell lef generation

To generate .lef file, first invoke magic tool to view the vsdstd cell design. Now type lef write on tckon window, the lef file will be generated in the folder as shown in the below screenshot:

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-21-26.png?raw=true)

the lef file is generated on vsd design folder

Now the lef file has been created, now we need to move this file to picorv32a. Before that we need to movie this file to src folder so that all the designs will be available at on location.`

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-35-16.png?raw=true)

Here we need to modify the config.tcl of picorv32a directory and add commands as shown in image

In order to integrate standard cell into the openlane input these command in the openlane flow

      prep -design picorv32a -tag 02-07_07-56 -overwrite
        set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
        add_lefs -src $lefs
        run_synthesis

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-39-37.png?raw=true)

Synthesis was successful

Post synthesis and floorplan placement is done.

To view the layout, magic tool is invoked in results/placement directory

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-40-12.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-40-47.png?raw=true)

Since Clock Tree Synthesis (CTS) is not yet completed, the timing analysis is performed using an ideal clock. At this stage, only setup time slack is evaluated. Setup slack is defined as the difference between the required arrival time and the actual data arrival time. For timing to be met, the worst-case slack must be zero or positive. If a negative slack is observed during pre-CTS analysis, the following corrective actions can be taken:

Adjust the synthesis strategy, including buffering and cell sizing options.

Check for cells that violate maximum fanout limits and replace or restructure high-fanout cells to reduce delay.

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2013-59-30.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-01-07.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-01-13.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-03-24.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-03-59.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-04-52.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-06-32.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-07-16.png?raw=true)

Sky130_vsdinv is added to the picorv32a design.

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-08-14.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-11-56.png?raw=true)

![image alt](https://github.com/Shiva67555/soc-design-and-planning-nasscom-vsd/blob/main/Screenshot%20from%202025-12-14%2014-12-32.png?raw=true)

# Day 5: Power Planning, Routing, and GDSII Generation. 

The final day of the workshop focused on completing the physical design flow by generating the Power Distribution Network (PDN), performing routing, validating timing after routing, and producing the final GDSII file for fabrication. This stage marks the transition from design implementation to tape-out readiness.

# Power Distribution Network in OpenLANE 

# Role of PDN 

A Power Distribution Network ensures reliable delivery of power and ground to every standard cell and macro within the chip. A well-designed PDN minimizes voltage drop, improves signal integrity, and enhances overall chip stability.

In comparison with ASIC flow, the power distribution in openlane is out of floorplan. PDN must be generated post CTS and timing analysis

To generated PDN network give command mentioned below

    gen_pdn

To ensure that PDN network is generated successfully you can give variable

    echo $::env(CURRENT_DEF)

The PDN primarily distributes:

1.VDD (power) 
2.VSS (ground) 

across the core using rails and straps.

# PDN Generation Flow 

# gen_pdn Execution 

OpenLANE provides the gen_pdn procedure to automatically generate the power grid. This step constructs horizontal and vertical power rails and connects them to all power pins in the design.

The PDN stage relies on predefined technology and library information to maintain compatibility with the routing and placement stages.

# PDN Configuration Dependencies 

# Required Variables 

Before executing PDN generation, certain configuration variables must be correctly defined.

# LIB_SYNTH_COMPLETE 

This variable must be present in the config.tcl file. It is internally referenced by the PDN scripts to access complete synthesis libraries.

# LEF_MERGED_UNPADDED 

This variable points to the merged LEF file without padding. It provides structural information required for power grid creation.

Improper configuration of these variables may cause PDN generation to fail.

# Routing:

Openlane uses two stages of routing. 

1.Fast routing: Routing region is divide into rectangular grids

2.Detailed routing: routing region is divide into finer grid to implement physical wiring using trionroute tool.

To run routing input command

    run_routing

Before initiating routing, key routing-related variables were inspected to confirm the current design state.

![image alt](https://github.com/Gobika404/NASSCOM-VSD-SoC--design-and--Planning-Program/raw/main/Screenshot%20from%202025-12-14%2022-34-31.png)

THANK YOU
