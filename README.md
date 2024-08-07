# NASSCOM--VSD-SOC-design

# Digital VLSI SoC Design and planning Training

Welcome to the OpenLane workshop! Throughout this session, we will explore the journey of creating an Application Specific Integrated Circuit (ASIC) using the OpenLane ASIC flow. This comprehensive process begins with an RTL file and progresses through multiple crucial stages, ultimately resulting in the creation of a GDS file.

## Lessons Learned

Understanding the RTL to GDS Flow:

1. Grasped the end-to-end process of converting a high-level hardware description to a physical ASIC layout.
Recognized the importance of each step in the flow, from synthesis to sign-off.

2. Synthesis:

Understood the complete process of transforming a high-level hardware description into a physical ASIC layout.
Appreciated the significance of each stage in the flow, from synthesis all the way to sign-off.

3. Floor and Power Planning:
Understood the significance of floor planning in chip partitioning and I/O pad placement.

## Day 1

The RTL to GDSII flow in VLSI design is a critical process that translates an RTL description of a digital circuit into a physical layout suitable for fabrication. It encompasses key stages such as RTL synthesis, floor planning, placement, routing, and culminates in generating the GDSII file format, which encapsulates the layout data. This meticulous process ensures that the final IC layout faithfully represents the intended functionality and complies with fabrication standards.

![image](https://github.com/user-attachments/assets/d79f2d9a-2c62-402e-a3ce-5f9d428da5f6)

## Overview of QFN-48 Chip, Pads, Core, Die, and IPs

VSD Squadron Board: This board highlights a specific area dedicated to the "Microprocessor," where our focus lies. Using the RTL to GDS flow, we will meticulously design this microprocessor, transitioning it from the abstract RTL level to the finalized fabrication-ready layout.

![image](https://github.com/user-attachments/assets/ddf592ec-bee3-4064-9a63-c3ce953c2bed)

## Introduction to IC Design components and terminologies

![image](https://github.com/user-attachments/assets/2b6ba079-5154-4bf5-ba5a-46d2a816bc46)
![image](https://github.com/user-attachments/assets/612c63c4-6c4c-4e4e-bcae-51ef652114c6)
![image](https://github.com/user-attachments/assets/99cab89c-ef2a-4624-a7d8-1c4c9790f7f6)
![image](https://github.com/user-attachments/assets/e0b51f1a-aaf3-469f-be8a-3d63d6ff5983)

- Core
   A core represents the central region within a chip where the fundamental logic of the design resides. It encompasses all the combinational circuits, both soft and hard Intellectual Properties (IPs), and the interconnecting nets essential for the chip's functionality.

- Die
   A die is a distinct area on a chip that includes the core logic and IO pads. Dies are replicated across the silicon wafer multiple times to enhance manufacturing efficiency and overall throughput.

- IO Pads
  IO pads are pins that facilitate communication between the core and the external environment. Pad cells encircle the rectangular metal areas where external connections are established. These include input pads, output pads, and power pads.

- IPs
    Foundry IPs, such as SRAM, ADC, DAC, and PLLs, are typically manually designed or require significant human involvement to define and create them.
  
- PDKs
    PDKs (Process Design Kits) serve as the interface between foundries and design engineers. They consist of a set of files that model the fabrication process for the design tools used in IC design. These files include device models, DRC (Design Rule Checking), LVS (Layout Versus Schematic), physical extraction, layers, LEF (Library Exchange Format), standard cell libraries, timing libraries, and more. In this workshop, the SkyWater 130nm PDK, specifically sky130_fd_sc_hd, is used, and OpenLANE is built around this PDK.

## Introduction to RISC-V
ISA (Instruction Set Architecture) is a method of interacting with the computer. Generally, we use coding languages like C, Java, and others to write programs that need to be executed by the system, but machines cannot understand these languages directly. This is where ISA comes into play. ISA translates written code from assembly language to binary, or machine-comprehensible language. The RISC-V ISA is the most recent ISA to be published, fulfilling this purpose.
![image](https://github.com/user-attachments/assets/0eccb7a7-d0b7-4728-b28d-960b0f79be14)

## From Software Applications to Hardware

In real life, we typically interact with application software to communicate with hardware. But how does this process work exactly? Between the application software and the hardware, there is a layer called system software. The applications interface with the system software, which then translates the instructions into a language the hardware can understand, namely binary language.

The system software is comprised of several layers:
![image](https://github.com/user-attachments/assets/fa977d4d-8ea1-4a3f-9e3d-83d0fec3ad11)


   Operating System (OS): In addition to general tasks like handling input/output operations, memory allocation, and low-level system functions, the OS translates application software instructions into corresponding machine code, enabling the hardware to execute them. The OS also manages the execution of programs written in languages such as C, C++, or Java, providing an interface between the software and hardware.

   Compiler: The compiler takes the code written in high-level programming languages and converts it into an instruction set (e.g., .exe files). These instructions are tailored to the specific type of hardware being used, allowing the software to be executed efficiently by the hardware.

   Assembler: The assembler translates the assembly code generated by the compiler into binary language (machine code), which the hardware can understand and execute to perform the desired operations.
   
##  OpenLane: Introduction to Components of Open-Source Digital ASIC Design

To design an open-source digital ASIC, several key components are required:
![image](https://github.com/user-attachments/assets/66a8e239-bb3d-4fc8-855b-b82dcd124b41)

- RTL Designs
- EDA Tools
- PDK Data

What are RTL Designs?

EDA (Electronic Design Automation) tools are software applications used to design and develop electronic systems, such as integrated circuits (ICs) and printed circuit boards (PCBs). These tools assist in various stages of the design process, including:

Schematic Capture: Creating and editing circuit diagrams.
Simulation: Testing and verifying circuit behavior through virtual models.
Layout Design: Arranging components on a PCB or IC layout.
Verification: Ensuring the design meets specified requirements through techniques like DRC (Design Rule Checking) and LVS (Layout Versus Schematic).
Synthesis: Converting high-level design descriptions into a lower-level representation that can be physically implemented.
Overall, EDA tools help automate and streamline the design process, improving efficiency and accuracy in creating complex electronic systems.

 I/O Libraries

## Simplified RTL to GDS Flow

The simplified RTL to GDS flow begins with an RTL file and, through a series of stages, produces a GDS file, which can be sent to a foundry for fabrication. The steps in the RTL to GDS flow include:
![image](https://github.com/user-attachments/assets/9c20bdd1-48ab-4ba3-8e17-5938b2b61687)

    Synthesis:
   The RTL (Register-Transfer-Level) file is converted into a physical circuit using components from the Standard Cell Library. Standard Cells in this library have a uniform height but vary in width, ensuring a regular and consistent layout. Each cell in the library is characterized by multiple models that include electrical properties, HDL (Hardware Description Language) specifications, Spice simulation parameters, and layout details (both abstract and detailed).

![image](https://github.com/user-attachments/assets/c5ac1b46-6839-4b57-9093-08cf0a212ef8)

    Floor Planning & Power Planning:
        Floor Planning: Determines the position of components on the chip to minimize area, including the placement of I/O pins, ports, and pads.
        Power Planning: Designs the power supply network (VDD and GND) using power rings, power straps, and power pads, typically on the top metal layers for minimal resistance and                              delay.
        
![image](https://github.com/user-attachments/assets/be30a2a0-da92-44c8-9eba-30c838c889c4)

    Placement:
        Components are placed within the designated areas from the floor planning stage.
        Standard Cells required in the design are also placed within their cell boundaries.
        Placement is performed in two stages: Global Placement (where cells may overlap) and Detailed Placement (where cells are optimally placed following placement rules).

![image](https://github.com/user-attachments/assets/08941932-f2c1-4526-963e-45bffbaba60e)

    CTS (Clock Tree Synthesis):
        Clock routing is performed before signal routing to address clock skew, the difference in time for the clock to reach various destinations.
        Symmetric Tree Structures (H-tree, I-tree, X-tree) are used to eliminate clock skew.

![image](https://github.com/user-attachments/assets/50f2895f-2b11-44f4-9ad6-02d766c5ed46)

    Routing:
        After clock routing, signal routing is performed using the remaining metal layers.
        Routing is divided into Global Routing (generates a routing guide based on PDK instructions) and Detailed Routing (actual routing according to the guide).
        
![image](https://github.com/AnoushkaTripathi/NASSCOM-VSD-SoC-design-Program/assets/98522737/6aa48de1-e1b3-4752-b38a-e0b996cf4aae)

    Sign-off:
        Once routing is completed, the chip undergoes various checks during the sign-off stage:
            Physical Verification Checks: Design Rule Check (DRC) and Layout vs. Schematic (LVS). DRC verifies design rule compliance, while LVS ensures functional correctness against 
                                          the gate-level netlist.
            Timing Checks: Static Timing Analysis (STA) checks the design for timing violations.

-----------------------------------------------------------------------------------------------------------------------------------------
## Introduction to OpenLANE Detailed ASIC Design Flow

The image illustrates the detailed ASIC design flow in OpenLANE. The process begins with the Design RTL, which undergoes RTL synthesis using Yosys and ABC to produce an optimized gate-level netlist. This netlist is then analyzed through STA (Static Timing Analysis) to check for timing violations. After STA, Design for Test (DFT) is performed—though this step is optional—and utilizes the FAULT tool.
![image](https://github.com/user-attachments/assets/6624ae33-7dc9-42a3-8ff2-de0f05e26d9a)

OpenLane started as an open-source flow for a true open-source tape-out experiment, initiated by e-fabless. It is a platform that supports various tools such as Yosys, OpenRoad, Magic, KLayout, and other open-source tools. OpenLane integrates and abstracts the different steps of silicon implementation. At e-fabless, they have an SOC family called Strive, which encompasses open-source elements, including Open PDK, Open RTL, and Open EDA.

![image](https://github.com/user-attachments/assets/15f33eb2-03f1-48dc-ad43-fa16ac387ed1)

FAULT (for DFT) includes:

   - Scan Insertion
   - Automatic Test Pattern Generation (ATPG)
   - Test Pattern Compaction
   - Fault Coverage
   - Fault Simulation

![image](https://github.com/user-attachments/assets/3d830380-96c0-4ea4-a66d-eeeb10eaa69f)

After DFT, the next phase is Physical Implementation, also known as Automated Place and Route (PnR), using OpenRoad.

OpenRoad (for Physical Implementation) includes:

    Floor/Power Planning
    End Decoupling Capacitors and Tap Cells Insertion
    Placement: Global and Detailed
    Post-Placement Optimization
    Clock Tree Synthesis
    Routing: Global and Detailed

During PnR, Logic Equivalence Checking (LEC) must be performed for each design change to ensure the functionality remains unchanged after netlist modifications. An important step during physical implementation is the "Fake Antenna Diodes Insertion Script."

Dealing with Antenna Rule Violations:
When a metal wire segment is fabricated, it can act as an antenna. Reactive ion etching can cause charge accumulation on the wire, potentially damaging transistor gates during fabrication.

Solutions:

Bridging: Attaching a higher layer intermediary, which requires router awareness.

![image](https://github.com/user-attachments/assets/e6509251-5c4f-4758-b9a7-ad0ec863d3fc)

Add antenna diode cell to leak away the charges. Antenna diodes are provided by the SCL. For this we took a preventive approach.
Add a Fake antenna didoe next to every cell input after placement.  Run the Antenna Checker(Magic) on the routed layout.If the checker reports violation on the cell input pin, replace the fake diode cell by a real one

And at the end, we perform Physical Verification. Which includes DRC(Design Rule Checking) , LVS(Layout Vs Schematic). Along with the P.V we also performs STA to check for timing violations in the design.

MAGIC is used for DRC and SPICE Extraction from Layout.

MAGIC and Netgen are used for LVS by comparing Extracted SPICE by MAGIC and Verilog Netlist.

![image](https://github.com/user-attachments/assets/bcf4a1d2-646c-4d56-b566-1a18683fabf1)

# RTL2GDS OpenLANE ASIC Flow Practical implementation

## Day 1 Labs

![image](https://github.com/user-attachments/assets/a4b0c98b-4f08-43a2-91b3-b35be88aa99d)
![image](https://github.com/user-attachments/assets/3f65e488-78d1-4575-a72e-0afae9e425c4)




![Screenshot from 27 ‎July ‎2024, ‏‎11:28:25](https://github.com/user-attachments/assets/36759026-d74d-4ec1-9f6a-3b9558126c4a)

1.  Understanding the use of various linux commands

   - pwd : It displays the present working directory and its path.

   - cd : Using this command we can move in both ways in the directory tree.

   - ls : It lists all the sub-directories and files present in the current directory.

   - mkdir : Using this command, we can create a new directory.

   - rmdir : Using his command, we can delete an existing directory.

   - rm : This command is used to delete the files.

   - help : using this command we can know the working of any command.

   - clear : This command clears the terminal.

![2](https://github.com/user-attachments/assets/8c9ff688-e6ab-4f96-8532-88cb757d2529)

To run in interactive mode (step by step mode)

    bash-4.2$ ./flow.tcl -interactive
    
`Package import and check`

    % package require openlane

`Prepare design`

To prepare and setup the design

    % prep -design picorv32a

![3a](https://github.com/user-attachments/assets/f5fbe8d5-a1a9-4b80-928e-79be10525605)
![3b](https://github.com/user-attachments/assets/b9d58f9b-0d7e-4e25-b1fd-ee29c809f8c9)

Once the preparation is complete, a new directory with the current date will be generated within the “runs” folder. Inside this directory, all the necessary subdirectories for storing results, reports, and other relevant data will be created.

![4](https://github.com/user-attachments/assets/df7d8160-dc29-4651-9f1e-f41a290ef4b2)

The preparation step involves the following actions for the picorv32a design within the openLANE flow:

**Directory Structure Setup:**

A new directory structure is created to organize the design files.
This structure includes subdirectories for different components (e.g., results, reports).

- LEF Merging:
The technology LEF (.tlef) and cell LEF (.lef) files are merged into a unified format.The technology LEF contains layer information (such as metal layers), while the cell LEF contains cell informations.
- Design Placement:
All design-related files are placed under the designs directory.
This ensures that the necessary files are organized and accessible during subsequent steps.

![5](https://github.com/user-attachments/assets/32ca3c89-8e11-42b0-b8fd-63a82c1847f1)

| `config.tcl`	 | contains the configurations used by openLANE |                      
| :-------- | :-------                                     | 
| `src`      |  contains verilog files and constraints file|

![6](https://github.com/user-attachments/assets/316e6f41-3ad8-449d-98a8-0745ccc9acf7)

` Synthesis `
   % run_synthesis

![7](https://github.com/user-attachments/assets/7019bdab-eb5f-4a81-9c5a-350d8ef7eaba)

![8](https://github.com/user-attachments/assets/11b67f58-5740-4419-a2ae-4f25ca1db790)

![9](https://github.com/user-attachments/assets/62d3982b-c5cb-4d4c-84cc-ea80716a3bd3)

![10a](https://github.com/user-attachments/assets/f01634b2-5600-4265-a5bc-c0902bd238ba)

![10b](https://github.com/user-attachments/assets/b56ed027-9000-4d8c-b2b6-d47f38402ae4)


# Day 2

## Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells
Chip FloorPlanning Considerations

![image](https://github.com/user-attachments/assets/62f54821-6e05-4d81-a313-66b59e680a19)


Utilization Factor and Aspect Ratio
In order to find out the Utilization Factor and Aspect Ratio, first we need to know how to define height and width of core and die areas.

- Core is an area in a chip which is used to place all the logic cells and components in a chip. It is the place where logic lies in a chip.

- Die is an area that encircles the core area and used for placing I/O related components.

The height and width of the core area are determined by the netlist of the design, which specifies the number of components needed to implement the logic. The dimensions of the die area will then be based on the height and width of the core area, reflecting the overall size requirements to accommodate the design.

![image](https://github.com/user-attachments/assets/54b83d76-d4ea-437b-b6f2-5ef16828d65d)

For example, lets consider a netlist that is having two logic gates and two flipflops each having area of 1 sq.unit. The netlist contains 4 elements and the minimum total area required for the core area will be 4 sq.units.

![image](https://github.com/user-attachments/assets/b87bd7e0-cc94-41bf-b56c-9f086af263c5)

![image](https://github.com/user-attachments/assets/ecb63258-6ad9-4dcb-96d3-522e25df98f1)

*Utilization Factor :*  Utilization Factor is defined as "The ratio of the core area occupied by the netlist to the total core area".For a good FloorPlan, The Utilization Factor should never be '1' because when the Utilization factor becomes '1' , there will be no place for adding additional logic if needed and it will be considered as a bad FloorPlan.


`Utilization Factor = (Area occupied by netlist / Total core area)`

*Aspect Ratio :*  Aspect Ratio is defined as "The ratio of Height of the core to the width of the core". If the Aspect ratio is '1' , then the core is said to be in a square shape and other than '1' the core will be a rectangle.

`Aspect Ratio = (Height of the core / Width of the core)`

![image](https://github.com/user-attachments/assets/7360a095-5469-40c8-88b3-06447bdb30c3)

In this case, when calculated

- Utilization factor = (4 squnits)/(4 squnits) = 1

- Aspect Ratio = (2 units)/(2 units) = 1 //The core is in a square shape.

![image](https://github.com/user-attachments/assets/951efc7d-ff16-4512-bfcb-612e1d67af21)

In this case, when calculated

- Utilization factor = (4 squnits)/(8 squnits) = 0.5

- Aspect Ratio = (2 units)/(4 units) = 0.5 //The core is in a rectangular shape.


# Day 2 Labs
# Steps to run floorplan using OpenLANE

![image](https://github.com/user-attachments/assets/57113e78-7302-4ee6-9c26-ab573eeb3d06)

For a smooth floorplan process, designers need to manage certain switches that influence the floorplan configuration. For example, switches such as the utilization factor and aspect ratio play a role in determining the floorplan's dimensions and layout. Designers should carefully review these switches to ensure they align with the project's requirements before initializing the floorplan. The image below illustrates the various types of switches used in the floorplan stage.

    % run_floorplan

![1 floorplan_tcl](https://github.com/user-attachments/assets/b03d5433-6dfe-433e-ba93-3b0d96fa840c)

![2 floorplan tcl file](https://github.com/user-attachments/assets/020f0c36-1514-4725-8952-55e652fcf8d5)

![3 config_tcl](https://github.com/user-attachments/assets/4375ad78-494f-40ac-b54d-ccaca2a45bba)

![4 floor results](https://github.com/user-attachments/assets/0fd425ed-2a52-4db8-823d-a06b6a18007e)

![5 def file](https://github.com/user-attachments/assets/933ff44e-5ff0-46d5-8644-d0c4169e864a)

 Once the floorplan is complete, you can review the generated report to assess aspects such as die area. However, to visualize the design in a graphical user interface (GUI), you should use the MAGIC tool.

![6 magic](https://github.com/user-attachments/assets/91a025aa-96f0-4881-ac7a-c16251955a80)

![7 magic](https://github.com/user-attachments/assets/aaf39941-2fcf-4a3b-822e-7913fc80013e)

Review Floorplan layout in magic
## Design Alignment Instructions

### Centering the Design:
1. Press `S` to select the entire design.
2. Press `V` to vertically align it to the middle of the screen.

### Zooming In on a Specific Area:
1. Left-click and drag to select the desired region.
2. Right-click to bring up the context menu.
3. Press `Z` to zoom in on the selected area.

### Getting Details of a Cell:
1. Move your cursor to the cell of interest.
2. Press `S` to select the cell.
3. In the `tkcon` window, enter the command "what"  to display cell details.

![8 metal layer](https://github.com/user-attachments/assets/ef10e706-a3ae-4595-9b31-d69e88233686)

## Placement in VLSI Design

Placement plays a crucial role in VLSI (Very Large Scale Integration) design. It involves determining the physical locations of standard cells or logic elements within a chip or block. Let's break it down:

1. **Global Placement:**
   - Global placement assigns general locations to movable objects (cells).
   - Some overlaps between placed objects are allowed during this stage.
   - The goal is to achieve a rough layout that satisfies area constraints.
   - 
![9 run placement](https://github.com/user-attachments/assets/3f14981f-fea7-4fb6-9510-089ebb46bc6d)

2. **Detailed Placement:**
   - Detailed placement refines the object locations obtained from global placement.
   - It enforces non-overlapping constraints and ensures that cells are placed on legal cell sites.
   - The quality of detailed placement significantly impacts subsequent routing stages.

`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`

![10 magic Placement](https://github.com/user-attachments/assets/822c04d8-ef5d-48be-8dae-1f817d37bdb7)

![11 magic P](https://github.com/user-attachments/assets/23b6558f-27dc-4083-8511-d8e8c9dcb429)


### Inputs
| Item                    | Description                                                                                   |
|-------------------------|-----------------------------------------------------------------------------------------------|
| PDKs                    | Process Design Kits (PDKs) provide technology-specific information for chip design.          |
| DRC and LVS rules       | Design Rule Check (DRC) and Layout vs. Schematic (LVS) rules ensure layout compliance.        |
| SPICE models            | These models describe transistor behavior for circuit simulation.                             |
| Library & User-defined specs | Custom libraries and specifications specific to your project.                                 |

### Design Steps
1. **Circuit Design:**
   - Create the logical schematic of your circuit.
   - Define the functionality and connections of standard cells.

2. **Layout Design:**
   - Use layout tools (e.g., MAGIC) to create the physical layout.
   - Follow design rules and guidelines for placement and routing.

3. **Characterization using GUNA:**
   - Perform timing, power, and noise characterizations.
   - Validate the design against specifications.

### Outputs
- **CDL (Circuit Description Language):** A textual representation of the circuit.
- **GDSII:** The layout file in GDSII format for fabrication.
- **LEF (Library Exchange Format):** Contains information about cell sizes, pin locations, and other details.
- **Spice Extracted Netlist:** Includes parasitic information for circuit simulation.
- **Timing, Noise, and Power Libraries:** Generated during characterization.


## Day 3

# Inverter Characterization using Sky130 Model Files

## CMOS Inverter Simulation with ngspice

This guide demonstrates how to create a basic CMOS inverter netlist, perform DC and transient analyses using ngspice, and understand key static and dynamic characteristics.

## Static Characteristics

Certainly! Here’s a table detailing the characteristics of a CMOS inverter, including noise margin:

| **Characteristic**         | **Details**                                                |
|----------------------------|------------------------------------------------------------|
| **Transistor Types**       | PMOS and NMOS                                              |
| **Power Supply Voltage (Vdd)** | Typical values: 1.8V, 3.3V, 5V                           |
| **Input Voltage (Vin)**    | 0V to Vdd                                                  |
| **Output Voltage (Vout)**   | 0V to Vdd                                                  |
| **Threshold Voltage (Vth)** | NMOS: ~0.2V to 0.5V, PMOS: ~-0.2V to -0.5V                |
| **Static Power Consumption** | Very low, ideally near zero (minimal leakage currents)    |
| **Dynamic Power Consumption** | \( P_{dynamic} = \frac{1}{2} C_{load} V_{dd}^2 f_{clk} \) |
| **Input-Output Characteristics** | Inverter transfer characteristic curve: shows the relationship between Vin and Vout |
| **Propagation Delay**      | Time taken for the output to change state in response to a change in input, affected by load capacitance and drive strength |
| **Noise Margin**           | **NM_H** (High Noise Margin): \( NM_H = V_{OH} - V_{IH} \) <br> **NM_L** (Low Noise Margin): \( NM_L = V_{IL} - V_{OL} \) <br> Where: <br> - \( V_{OH} \) = Output High Voltage <br> - \( V_{OL} \) = Output Low Voltage <br> - \( V_{IH} \) = Input High Voltage <br> - \( V_{IL} \) = Input Low Voltage |
| **Power Gain**             | Typically less than 1, but provides strong drive capabilities |
| **Switching Speed**        | Depends on transistor sizes and supply voltage; generally faster with larger transistors and higher Vdd |
| **Load Driving Capability** | Strong drive capability; can drive other gates and large capacitive loads |

This table includes noise margin characteristics, which are crucial for understanding how much noise the inverter can tolerate before its output is affected.

## Dynamic Characteristics

1. **Propagation Delays:**
   - The time taken for the output to change after a change in input.
2. **Rise Time (tr):**
   - The time taken for the output to transition from Vol to Voh.
3. **Fall Time (tf):**
   - The time taken for the output to transition from Voh to Vol.


# Design library cell using Magic Layout and ngspice characterization
## Creating Standard Cell Layout

1. **Design the Inverter Layout:**
   - Use a layout tool (such as MAGIC) to create the inverter layout.
   - Follow process-specific design rules and guidelines.
   - Place standard cells (transistors, metal layers, etc.) based on the logical schematic.

2. **Extraction Process:**
   - After layout creation, extract parasitic capacitances and resistances.
   - In the `tkcon` window, execute the command `extract all`.
   - This generates an extracted file with parasitic information (e.g., capacitances, interconnect resistance).
   - The extracted file is saved in the `vsdstdcelldesign` directory.

3. **SPICE Netlist:**
   - Use the extracted data to create a SPICE-compatible netlist (usually in `.sp` or `.cir` format).
   - Include transistor models, capacitances, and resistances.
   - Use this netlist for simulation in tools like ngspice.


## Introduction to LEF Files in VLSI Design
In VLSI (Very Large Scale Integration) design, LEF (Library Exchange Format) files play a crucial role in interfacing between layout tools and place-and-route (PnR) tools. Hereâ€™s what you need to know:

Purpose of LEF Files:

The entire layout information of a block (whether itâ€™s a macro or a standard cell) is not necessary for PnR tools.
PnR tools require minimal information, including the PR boundary (bounding box) and pin positions.
LEF files provide an abstract representation of the block, exposing only the essential details needed for PnR.



| Cell LEF	 | Abstract view of the cell which holds information about PR boundary, pin positions and metal layer information.  |
|---------------|---------------|
| Technology LEF | Holds information about the metal layers, via, DRC technology used by placer and router.|

![image](https://github.com/user-attachments/assets/9fa7c18f-dbd0-4d6f-95d5-67e532f93c5c)


# VLSI Routing: Tracks and Routes

In VLSI design, understanding tracks and routes is essential for successful interconnect design. Let's break it down:

## Tracks

- **Definition:**
  - Tracks represent predefined horizontal and vertical paths on each metal layer.
  - They serve as guidelines for routing wires (metal traces) within a chip.

- **Purpose:**
  - Tracks help maintain uniform spacing and alignment during routing.
  - They simplify the routing process by providing fixed paths.

## Routes

- **Definition:**
  - Routes are the actual metal traces that carry signals (such as interconnects or wires).
  - These traces can be placed over the tracks, following specified routing rules.

- **Functionality:**
  - Routes connect different components (cells) within the chip.
  - They form the wiring network for data flow.

## `tracks.info` File

- The `tracks.info` file:
  - Provides information about horizontal and vertical tracks available on each metal layer.
  - Specifies pitch, spacing, and other relevant details necessary for efficient routing.

    
# Day 3 labs

Magic layout view to cmos inverter
To get the cell files refer  

 [vsdstdcelldesign](https://github.com/nickson-jose/vsdstdcelldesign) 
 
 ![1 clone](https://github.com/user-attachments/assets/1d82aca4-3616-4287-af07-e8c7e9978a41)

 ![2 copy](https://github.com/user-attachments/assets/c10b6a20-f501-4a8d-a8e0-4e1ef6a8cdf7)

 ![3 magic](https://github.com/user-attachments/assets/8affa364-3f0b-4d74-b23a-d48c75013c67)

 ![4 inverter](https://github.com/user-attachments/assets/da9757df-31ea-4de1-b704-531ef6b137f7)


To extract the parasitics and characterize the cell design use below commands in tkcon window.

    extract all
    ext2spice cthresh 0 rthresh 0
    ext2spice

![5 extract](https://github.com/user-attachments/assets/6e4eef97-a4d9-41cd-819a-6c8d2df10113)

![6 ext file name](https://github.com/user-attachments/assets/d19bc9ce-9cf9-449b-8959-cd96a13f9712)


Modify the file according to 

![image](https://github.com/user-attachments/assets/f4c4bc49-30e1-49f3-8118-452d3f9d131c)

![7 vim spice](https://github.com/user-attachments/assets/c2825f3f-8021-4cda-8f70-25e262152b1e)

![8 spice file edited as per diagram](https://github.com/user-attachments/assets/6e1c100b-df7c-4715-bc8a-38f54aa78ad7)


Now the next step is to run the SPICE file in ngspice tool by using command ngspice sky130_inv.spice

![9 ngspice](https://github.com/user-attachments/assets/d5a7a37b-3364-484d-af6d-cb28a6f460aa)

![10 plot](https://github.com/user-attachments/assets/efbffbe6-860f-490b-a33e-7a31be8dd065)


# Inverter Characterization using Sky130 Model Files

In this lab, we will characterize the inverter using ngspice and Sky130 model files. The goal is to extract key parameters from the simulation results.

## LEF File Creation
Now that we have successfully characterized the inverter, the next step is to create a LEF (Library Exchange Format) file.

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

**VLSI Layout Geometries and DRC Errors**

In this section, we explore independent example layout geometries (M3.1, M3.2, M3.5, and M3.6) and highlight the specific DRC (Design Rule Check) errors associated with each:

1. Certainly! Here’s the information formatted in blocks:

---

### M3.1 (Metal Width DRC)
- **Violation:** 
  - The metal trace width in M3.1 is below the specified minimum width threshold.
- **Error:** 
  - Metal width does not meet design rules.

---

### M3.2 (Metal Spacing DRC)
- **Violation:** 
  - The distance between adjacent metal traces in M3.2 does not meet the required spacing.
- **Error:** 
  - Metal spacing violation.

---

### M3.5 (Via Overlapping DRC)
- **Violation:** 
  - The vias in M3.5 overlap with each other.
- **Error:** 
  - Via overlapping issue.

---

### M3.6 (Minimum Area DRC)
- **Violation:** 
  - The enclosed area within M3.6 does not meet the specified minimum area requirement.
- **Error:** 
  - Minimum area violation.

---

Use the command `magic -d XR` to open the Magic tool

![11 drc files and contents](https://github.com/user-attachments/assets/b0d07132-1ad9-4f56-b926-468fd76fc6f0)

# Using Magic Tool: Filling an Area with Metal 3 and Creating a VIA2 Mask

In this guide, we'll demonstrate how to fill a selected area with metal 3 and create a VIA2 mask using the Magic layout tool.

## Steps:

1. **Select an Area and Fill with Metal 3:**
   - Open the Magic GUI.
   - Select the desired area on your layout.
   - Guide the pointer to the metal 3 layer.
   - Press `P` to fill the selected region with metal 3.

2. **Create the VIA2 Mask:**
   - Open the `tkcon` terminal within Magic.
   - Type the command: `cif see VIA2`.
   - The metal 3-filled area will now be associated with the VIA2 mask.


![12 met3](https://github.com/user-attachments/assets/88fd82d7-bc22-4827-bf8e-703586d71cb8)

## **Lab exercise to fix Poly-9 error in Sky130 tech file**

![13 load poly](https://github.com/user-attachments/assets/06fcb110-844a-413c-bb08-23eeae757951)

![14 poly](https://github.com/user-attachments/assets/a724c23a-9b7c-4b68-9e3b-1f2e40a90c8a)


Commands to run in tkcon window

     # Loading updated tech file
       tech load sky130A.tech

     # Must re-run drc check to see updated drc errors
      drc check

     # Selecting region displaying the new errors and getting the error messages 
      drc why


Incorrectly implemented difftap.2 simple rule correction

![image](https://github.com/user-attachments/assets/de1702d8-7ffe-42ea-a99c-4eb80299358f)


![image](https://github.com/user-attachments/assets/90d808cb-a60f-4018-a7a3-90b4220f55ec)


## DRC error as geometrical construct

N well rules 

![image](https://github.com/user-attachments/assets/3df743de-76c7-464e-bc9e-463f1dbc2019)

![15 nwell](https://github.com/user-attachments/assets/9431a2a3-2f95-43ff-81a4-49cf7393ac3a)


# Day 4 : Pre-layout timing analysis and importance of good clock tree 

# Timing Modeling Using Delay Tables and Converting Grid Info to Track Info

In this section, we'll explore timing modeling using delay tables and the process of converting grid information to track information. Let's break it down step by step:

## Timing Modeling with Delay Tables

Certainly! Here’s the information in table format:

| **Category** | **Details**                                                                                           |
|--------------|-------------------------------------------------------------------------------------------------------|
| **Delay Tables** | - **Description:** Provide information about the delay (propagation time) of signals through various components (such as gates, wires, and interconnects). <br> - **Purpose:** Help estimate signal arrival times and ensure proper timing in the design. |
| **Usage**    | - **Context:** Used during the physical design process to model the behavior of standard cells, macros, and other components. <br> - **Function:** Guide the placement and routing tools to optimize signal paths for timing closure. |

## Converting Grid Info to Track Info

Here’s the information formatted in a table:

| **Category**         | **Details**                                                                                                           |
|----------------------|-----------------------------------------------------------------------------------------------------------------------|
| **Purpose**          | - **Objective:** Convert grid information (rows and columns) into track information. <br> - **Definition:** Tracks represent predefined horizontal and vertical paths on each metal layer. |
| **Considerations**   | - **Alignment:** Input and output ports should align with the intersection of vertical and horizontal tracks. <br> - **Dimensions:** The standard cell's width should be an odd multiple of the track pitch, and its height should be an odd multiple of the vertical track pitch. |
| **LEF File Extraction** | - **Requirement:** Extract the LEF (Library Exchange Format) file for the Inverter cell. <br> - **Purpose:** Provides essential information for the place-and-route (PNR) process. |
| **Understanding Tracks** | - **File:** Open the `tracks.info` file. <br> - **Contents:** Learn about the horizontal and vertical tracks available on each metal layer, including pitch, spacing, and other relevant details necessary for efficient routing. 

# Day 4 Labs

 Commands to open the custom inverter layout
![1 tracks](https://github.com/user-attachments/assets/e3ec19b2-54bf-4177-894c-d9f03f569c61)


    # Change directory to vsdstdcelldesign
    cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

    # Command to open custom inverter layout in magic
    magic -T sky130A.tech sky130_inv.mag &

 Commands for tkcon window to set grid as tracks of locali layer

    # Get syntax for grid command
    help grid

    # Set grid values accordingly
    grid 0.46um 0.34um 0.23um 0.17um

![2 grid](https://github.com/user-attachments/assets/f7868225-b4d4-4592-8af0-79b041136471)

 **Save the finalized layout with custom name and open it.**

    # Command to save as
    save sky130_vsdinv.mag


Generate lef from the layout.

Command for tkcon window to write lef

    # lef command
    lef write

![3 copy lef file](https://github.com/user-attachments/assets/dcd13249-de67-4d5f-908f-7d90b94c5312)


![4 copied cell characterixation fie](https://github.com/user-attachments/assets/56fda176-7517-4101-b47d-9a6af130fe33)


Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

![image](https://github.com/user-attachments/assets/7e28f51e-c091-454b-a683-dbeb10ba07d4)

![6 re design](https://github.com/user-attachments/assets/2b1d9e0e-36e8-4682-b93b-be1aea3476c5)

     set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

     set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
     set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib" 

     set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

     set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

**Run openlane flow synthesis with newly inserted custom inverter cell.**

run_synthesis 

![5 synthesis](https://github.com/user-attachments/assets/c961caff-21c5-4ad6-a9d3-ed3ecdeb49dd)

Commands to view and change parameters to improve timing and run synthesis
```
# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)


# Now we are ready to run placement
run_placement

```
![8 magic result](https://github.com/user-attachments/assets/abcf68bc-ac3c-4529-9f74-ce90ca69f262)

![image](https://github.com/AnoushkaTripathi/NASSCOM-VSD-SoC-design-Program/assets/98522737/b7c8cdb1-5b2a-4216-b99e-119553f2bf75)


```

Do Post-Synthesis timing analysis with OpenSTA tool.

Newly created pre_sta.conf for STA analysis in openlane directory

![9 my base](https://github.com/user-attachments/assets/a0b024ea-4783-4a40-b7b0-98a3a359d96a)

my_base.sdc


![image](https://github.com/AnoushkaTripathi/NASSCOM-VSD-SoC-design-Program/assets/98522737/0b5679e3-85f4-409c-b4da-b456e8c83258)


# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

# Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

# Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

# Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

# Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

# Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

# Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

# Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
```

![11 sta](https://github.com/user-attachments/assets/7a79357f-1a47-4785-8ff0-a9ecbcb9791e)

![12 cts](https://github.com/user-attachments/assets/1825b62e-a9a7-48f6-ac3b-4aeab6b24ed8)

Finally slack is met 


**Now run Placement**

![8 magic result](https://github.com/user-attachments/assets/710d0fb8-c00d-44fc-ad86-7349c36f2170)


# Day 5 GDS II Final step

## Power Distribution Network (PDN) Generation in OpenLANE

In OpenLANE, the PDN (Power Distribution Network) is crucial for proper power delivery within the chip. Let's walk through the steps to build the PDN:

## 1. PDN Generation

- The PDN ensures that all standard cells and macros receive adequate power.
- It provides a network of power rails (VDD and VSS) across the chip.

## 2. Using `gen_pdn` Procedure

- The `gen_pdn` procedure is responsible for running the PDN generation process.
- It sets up the power grid, defines power rails, and ensures proper connectivity.

## Common Issues

1. **`LIB_SYNTH_COMPLETE`:**
   - This variable must be defined in the `config.tcl` file.
   - It is called by the `gen_pdn` procedure defined in the `or_pdn.tcl` file.

2. **`LEF_MERGED_UNPADDED`:**
   - Ensure that this variable is correctly set in the `config.tcl` file.
   - It provides essential information for PDN generation.

![8 magic result](https://github.com/user-attachments/assets/7700d7de-ae83-450c-b02d-183165dc1e9e)


##Routing

Command to perform routing
```
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

# Command for detailed route using TritonRoute
run_routing
```
![1 routing](https://github.com/user-attachments/assets/5c975fb4-edd2-4826-a176-a1b622905ca0)


Power Planning :

![image](https://github.com/user-attachments/assets/27508f5c-736c-49b7-a15e-38490205c8a0)



## VLSI Routing: Global Route and Detail Route

In VLSI design, the routing process is divided into two main stages: global route (or fast route) and detail route. Let's explore each stage:

## 1. Global Route (Fast Route)

- **Purpose:**
  - The global route focuses on quickly establishing a high-level routing solution.
  - It divides the chip into rectangular grid cells, forming a 3D routing graph.

- **Key Points:**
  - The global route creates a routing guide, which consists of boxes (representing pins of cells).
  - The output of the global route is a set of routing guides for each net.

## 2. Detail Route

- **Performed by Engine:**
  - Detail route is executed by the engine called tritonRoute.
  - It refines the routing solution obtained from the global route.

- **Using Global Route Output:**
  - Detail route utilizes the output from the global route, including the routing guides.
  - Algorithms are applied to find the best possible connectivity among all the routing points.

![image](https://github.com/user-attachments/assets/d32f97fc-b6a2-48e1-ac99-7cdd0571fbb1)

![image](https://github.com/user-attachments/assets/1c7aac04-b778-4990-a6d3-4820da9f75af)




## Links

https://github.com/sush5591/NASSCOM--VSD-SOC-design

https://www.linkedin.com/in/sushant-sukhadeo-gawade-59b60a84/


