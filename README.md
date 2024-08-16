# NASSCOM--VSD-SOC-design
- [Content Learned](#ContentLearned)
- [Day 1](#Day1)
- [Overview of QFN-48 Chip, Pads, Core, Die, and IPs](#OverviewofQFN-48Chip,Pads,Core,Die,andIPs)
- [Introduction to IC Design components and terminologies](#IntroductiontoICDesigncomponentsandterminologies)
- [Introduction to RISC-V](#IntroductiontoRISC-V)
- [From Software Applications to Hardware](#FromSoftwareApplicationstoHardware)
- [OpenLANE:Introduction to Components of Open-Source Digital ASIC Design](#OpenIntroductiontoComponentsofOpen-SourceDigitalASICDesign)
- [Simplified RTL to GDS Flow](#SimplifiedRTLtoGDSFlow)
- [Introduction to OpenLANE Detailed ASIC Design Flow](#IntroductiontoOpenLANEDetailedASICDesignFlow)
- [Day 1 Labs](#Day1Labs)
- [Day 2](#Day2)
- [Good FloorPlan Vs Bad FloorPlan and Introduction to Library Cells](#GoodFloorPlanVsBadFloorPlanandIntroductiontoLibraryCells)
- [Steps to run floorplan using OpenLANE](#StepstorunfloorplanusingOpenLANE)
- [Design Alignment Instructions](#DesignAlignmentInstructions)
- [Placement in VLSI Design](#PlacementinVLSIDesign)
- [Day 3](#Day3)
- [CMOS Inverter Simulation with ngspice](#CMOSInverterSimulationwithngspice)
- [StaticCharacteristics](#StaticCharacteristics)
- [Dynamic Characteristics](#DynamicCharacteristics)
- [Creating Standard Cell Layout](#CreatingStandardCellLayout)
- [Introduction to LEF Files in VLSI Design](#IntroductiontoLEFFilesinVLSIDesign)
- [Tracks](#Tracks)
- [Routes](#Routes)
- [Day 3 labs](#Day3labs)
- [LEF File Creation](#LEFFileCreation)
- [Lab exercise to fix Poly-9 error in Sky130 tech file](#LabexercisetofixPoly-9errorinSky130techfile)
- [DRC error as geometrical construct](#DRCerrorasgeometricalconstruct)
- [Timing Modeling with Delay Tables](#TimingModelingwithDelayTables)
- [Converting Grid Info to Track Info](#ConvertingGridInfotoTrackInfo)
- [Day 4 Labs](#Day4Labs)
- [Day 5 GDS II Final step](#Day5GDSIIFinalstep)
- [Power Distribution Network (PDN) Generation in OpenLANE](#PowerDistributionNetwork(PDN)GenerationinOpenLANE)
- [PDN Generation](#PDNGeneration)
- [Routing](#Routing)
- [VLSI Routing: Global Route and Detail Route](#VLSIRoutingGlobalRouteandDetailRoute)
- [Links](#Links)

# Digital VLSI SoC Design and planning Training

Welcome to the OpenLane workshop! Throughout this session, we will explore the journey of creating an Application Specific Integrated Circuit (ASIC) using the OpenLane ASIC flow. This comprehensive process begins with an RTL file and progresses through multiple crucial stages, ultimately resulting in the creation of a GDS file.

## Content Learned

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
        
![image](https://github.com/user-attachments/assets/b129d5cc-5dac-44ca-ad16-4380caf23313)


    Sign-off:
        Once routing is completed, the chip undergoes various checks during the sign-off stage:
            Physical Verification Checks: Design Rule Check (DRC) and Layout vs. Schematic (LVS). DRC verifies design rule compliance, while LVS ensures functional correctness against 
                                          the gate-level netlist.
            Timing Checks: Static Timing Analysis (STA) checks the design for timing violations.

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

![1 openlane](https://github.com/user-attachments/assets/e02c120c-c92a-4cde-8b3d-9797e53b66da)


1.  Understanding the use of various linux commands

   - pwd : It displays the present working directory and its path.

   - cd : Using this command we can move in both ways in the directory tree.

   - ls : It lists all the sub-directories and files present in the current directory.

   - mkdir : Using this command, we can create a new directory.

   - rmdir : Using his command, we can delete an existing directory.

   - rm : This command is used to delete the files.

   - help : using this command we can know the working of any command.

   - clear : This command clears the terminal.

![2 openlane](https://github.com/user-attachments/assets/8dc565ba-fa06-4b85-be6f-1f19e1ed3541)
![3 openlane](https://github.com/user-attachments/assets/fc659b31-13d1-428c-bb55-9d1f5de416bb)

To run in interactive mode (step by step mode)

    bash-4.2$ ./flow.tcl -interactive
    
`Package import and check`

    % package require openlane

`Prepare design`

To prepare and setup the design

    % prep -design picorv32a

![4 openlane](https://github.com/user-attachments/assets/dc396367-17d8-4eca-bdc7-500d70ada99b)

Once the preparation is complete, a new directory with the current date will be generated within the “runs” folder. Inside this directory, all the necessary subdirectories for storing results, reports, and other relevant data will be created.

![5 location](https://github.com/user-attachments/assets/dfe8bde1-df4a-4dd3-bcc2-ef4ffa0bcf3a)

The preparation step involves the following actions for the picorv32a design within the openLANE flow:

**Directory Structure Setup:**

A new directory structure is created to organize the design files.
This structure includes subdirectories for different components (e.g., results, reports).

- LEF Merging:
The technology LEF (.tlef) and cell LEF (.lef) files are merged into a unified format.The technology LEF contains layer information (such as metal layers), while the cell LEF contains cell informations.
- Design Placement:
All design-related files are placed under the designs directory.
This ensures that the necessary files are organized and accessible during subsequent steps.


| `config.tcl`	 | contains the configurations used by openLANE |                      
| :-------- | :-------                                     | 
| `src`      |  contains verilog files and constraints file|

![8 tcl file location](https://github.com/user-attachments/assets/ef8fd537-6b4f-4e18-82cd-147e37dd51e1)
![9 config tcl](https://github.com/user-attachments/assets/fb6c6116-4860-4031-805a-71de527dc81c)

` Synthesis `
   % run_synthesis

![6 executing abc](https://github.com/user-attachments/assets/c40b2547-768a-4299-91aa-3db46202491f)

![7 synthesis successful](https://github.com/user-attachments/assets/8eb0fe0d-5f3c-4e1f-8288-71da9f126ec3)

![10 chip area](https://github.com/user-attachments/assets/5cb26b74-dcc4-4ab5-aedb-bf7b410408b6)

` Flop Ratio `= 10.84%

![11 d ff count by no of cell](https://github.com/user-attachments/assets/7b906d99-9eda-4333-afd9-791a6c2e54a0)

![12 flop ratio](https://github.com/user-attachments/assets/0f513ca4-6490-4868-827a-c3be48a7d7ab)


## Day 2

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
## Steps to run floorplan using OpenLANE

![image](https://github.com/user-attachments/assets/b218a695-0880-47ea-9f7e-ae00fa6a9bf8)
![image](https://github.com/user-attachments/assets/b6a3b0fa-a2ac-405d-995b-61c29fc7dee3)

For a smooth floorplan process, designers need to manage certain switches that influence the floorplan configuration. For example, switches such as the utilization factor and aspect ratio play a role in determining the floorplan's dimensions and layout. Designers should carefully review these switches to ensure they align with the project's requirements before initializing the floorplan. The image below illustrates the various types of switches used in the floorplan stage.

   

![1 all tcl file](https://github.com/user-attachments/assets/0e5c1fe3-11e6-42f6-8c85-d22285afc03c)
![2 floorplan tcl](https://github.com/user-attachments/assets/3efbf632-a14c-4ca0-b7ef-53243c55fa99)

 % run_floorplan
 
![3 run floor plan](https://github.com/user-attachments/assets/524d99ea-066a-4322-b2bb-419b9e3b8ba0)
![4 floorplan succesful](https://github.com/user-attachments/assets/22d543ce-cd18-4362-a930-f5977a5527c2)
![5 floorplan time stamp](https://github.com/user-attachments/assets/3a416cf7-9197-4411-89f4-8b06bf06f119)


 Once the floorplan is complete, you can review the generated report to assess aspects such as die area. However, to visualize the design in a graphical user interface (GUI), you should use the MAGIC tool.

![7 invoke magic](https://github.com/user-attachments/assets/a04aa62a-56ac-49a7-bd5e-a80ec283e27b)

Review Floorplan layout in magic
## Design Alignment Instructions

### Centering the Design:
1. Press `S` to select the entire design.
2. Press `V` to vertically align it to the middle of the screen.

![7 invoke magic s v](https://github.com/user-attachments/assets/a6fd7b2e-7549-4dd8-9871-0ce2eab8f0a7)

### Zooming In on a Specific Area:
1. Left-click and drag to select the desired region.
2. Right-click to bring up the context menu.
3. Press `Z` to zoom in on the selected area.

## Placement in VLSI Design

Placement plays a crucial role in VLSI (Very Large Scale Integration) design. It involves determining the physical locations of standard cells or logic elements within a chip or block. Let's break it down:

1. **Global Placement:**
   - Global placement assigns general locations to movable objects (cells).
   - Some overlaps between placed objects are allowed during this stage.
   - The goal is to achieve a rough layout that satisfies area constraints.
   - 
% run_placement

![11 placement done](https://github.com/user-attachments/assets/6403d408-02c2-4971-82fb-4d38aecf84f9)

2. **Detailed Placement:**
   - Detailed placement refines the object locations obtained from global placement.
   - It enforces non-overlapping constraints and ensures that cells are placed on legal cell sites.
   - The quality of detailed placement significantly impacts subsequent routing stages.

`magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &`

![12 magic after P](https://github.com/user-attachments/assets/4f538944-03c6-4792-a4e9-004395aca988)

![13 invoke magic](https://github.com/user-attachments/assets/fd081b30-b49c-4acf-8540-927134326cb7)

### Getting Details of a Cell:
1. Move your cursor to the cell of interest.
2. Press `S` to select the cell.
3. In the `tkcon` window, enter the command "what"  to display cell details.

![14 placement of SC](https://github.com/user-attachments/assets/185735da-74d6-46dd-975c-85a9b426653a)

![tkcon what](https://github.com/user-attachments/assets/fd5db515-44a7-4eb5-aaab-70940f0e4511)

![different metal layer](https://github.com/user-attachments/assets/35ea2a05-c6be-4c17-b084-0fdd32f06426)


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

    
## Day 3 labs

IO Placer Revision

![1 mode 1 in floorplan tcl](https://github.com/user-attachments/assets/58167d77-24a3-42d4-8dd8-ac72679c9055)
![2 change to mode 2 run FP](https://github.com/user-attachments/assets/211eccae-f19c-429a-990b-13a940c6a1ad)

Check changes in the pins loacation through magic -T

 ![3 see again magic FP](https://github.com/user-attachments/assets/721a9417-e09a-4592-84a1-1d93ebdaefa1)
 
Clone custom inverter standard cell design from github repo

![4 clone git](https://github.com/user-attachments/assets/82891ded-3768-47d4-8317-14eb4076fddd)

![5 copy sky130 tech to vsdstd cell](https://github.com/user-attachments/assets/32ce47c2-bcbf-4785-ad59-3ea6a15465df)

Open custom invrter using magic command

![6 invoke magic](https://github.com/user-attachments/assets/9a6fe3c6-c649-4dac-9659-f8290df6e8df)

![7 cmos inverter all layer](https://github.com/user-attachments/assets/aa1c7912-1a1c-4343-8587-64c0f8fcedce)


To extract the parasitics and characterize the cell design use below commands in tkcon window.

    extract all
    ext2spice cthresh 0 rthresh 0
    ext2spice

![8 after extracting](https://github.com/user-attachments/assets/ce69a142-acf1-4d39-873a-785224d18e98)

![9 spice file has been created](https://github.com/user-attachments/assets/04598749-0d7d-4684-b705-22906bfcb2b8)


![10 spice file need to edit](https://github.com/user-attachments/assets/18d2eaf3-fb19-4428-8d45-a0e7f726f2b9)

Modify the file according to diagram given in video

![11 edited spice file](https://github.com/user-attachments/assets/cfb9f1c5-50a3-45b6-a9b4-6e6d6c957f0b)


Now the next step is to run the SPICE file in ngspice tool by using command ngspice sky130_inv.spice

These were th few errors facd while installing
![12 few errors while installing ngspice](https://github.com/user-attachments/assets/8307dc77-64a9-4682-9c53-1247d54c79f4)

![13 plot](https://github.com/user-attachments/assets/55d36762-8ae2-460c-baf5-f6ca08c0d32c)

![14 cmos inv](https://github.com/user-attachments/assets/b3c70f16-9c6f-4cf7-ab2b-10e6298b36ec)

Few readings are shown below

![15 readings rise](https://github.com/user-attachments/assets/f515e06f-69a4-4e35-9838-e238ce9e78c2)


# Inverter Characterization using Sky130 Model Files

In this lab, we will characterize the inverter using ngspice and Sky130 model files. The goal is to extract key parameters from the simulation results.

## LEF File Creation
Now that we have successfully characterized the inverter, the next step is to create a LEF (Library Exchange Format) file.

wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

![16 pdk documentation](https://github.com/user-attachments/assets/d643d272-9778-49be-b4c6-30a7d5ab32bc)


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

Use the command `magic -d XR` to open the Magic tool & Open met3.mag file as shown

![18 open metal 3](https://github.com/user-attachments/assets/991f0eef-b0df-4a36-91fb-fb672e10f305)

# Using Magic Tool: Filling an Area with Metal 3 and Creating a VIA2 Mask

In this guide, we'll demonstrate how to fill a selected area with metal 3 and create a VIA2 mask using the Magic layout tool.

## Steps:

1. **Select an Area and Fill with Metal 3:**
   - Open the Magic GUI.
   - Select the desired area on your layout.
   - Guide the pointer to the metal 3 layer.
   - Press `P` to fill the selected region with metal 3.
  
![19 select area](https://github.com/user-attachments/assets/29338159-69e9-4adf-afc8-6c277dbe33bc)

2. **Create the VIA2 Mask:**
   - Open the `tkcon` terminal within Magic.
   - Type the command: `cif see VIA2`.
   - The metal 3-filled area will now be associated with the VIA2 mask.

![20 paint via](https://github.com/user-attachments/assets/027f88a4-5dfb-4a0a-bd3f-9d577862f503)


## **Lab exercise to fix Poly-9 error in Sky130 tech file**

![21 load poly](https://github.com/user-attachments/assets/fa135cdb-a841-4102-9c78-6df8e6c8d12f)

![22 edit sky 130 tech file](https://github.com/user-attachments/assets/54a1b4bc-667e-4e41-89a3-00d9aa9f1874)

![23 poly error](https://github.com/user-attachments/assets/d2b71392-7031-4805-8d96-8b24c670babd)

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

![24 load nwell](https://github.com/user-attachments/assets/32a6828a-fb3d-47d6-ad71-1dd910e295c6)

![25 no error](https://github.com/user-attachments/assets/bcce48cb-bdcc-45eb-abfd-a737903925d4)


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

## Day 4 Labs

 Commands to open the custom inverter 
 ![2 tracks](https://github.com/user-attachments/assets/8ad04956-2f35-4b33-adab-274878a49f2b)

    # Change directory to vsdstdcelldesign
    cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

    # Command to open custom inverter layout in magic
    magic -T sky130A.tech sky130_inv.mag &

    ![1 magic with mag file](https://github.com/user-attachments/assets/dd55a150-cc7b-47c4-89ee-f9e3b6f3667c)

 Commands for tkcon window to set grid as tracks of locali layer

    # Get syntax for grid command
    help grid

![3 grid](https://github.com/user-attachments/assets/52036481-9a35-4354-ab63-3cc29230c7cd)

    # Set grid values accordingly
    grid 0.46um 0.34um 0.23um 0.17um

![4 with specific grid](https://github.com/user-attachments/assets/4c165e62-5100-40b7-837c-0b91e85bbfea)


 **Save the finalized layout with custom name and open it.**

    # Command to save as
    save sky130_vsdinv.mag
    a
![6 mag file](https://github.com/user-attachments/assets/1a7b3831-0df2-4c94-a0b1-4518238d9e06)


Generate lef from the layout.

Command for tkcon window to write lef

    # lef command
    lef write

![7 magic mag](https://github.com/user-attachments/assets/7ca3e920-6570-411e-a590-ad4dc7345604)

![8 lef write](https://github.com/user-attachments/assets/20415ec7-c978-43ba-91db-0e7dbb406bbe)

![9 copied all files t src directory](https://github.com/user-attachments/assets/14f61f9e-5916-49ad-a5f9-6e042eb66a19)


Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

![10 edit config tcl file](https://github.com/user-attachments/assets/d83486d8-a3b2-4bb7-b201-93afee160cdb)

     set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

     set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
     set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib" 

     set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

     set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

**Run openlane flow synthesis with newly inserted custom inverter cell.**

run_synthesis 

![12 invoke docker](https://github.com/user-attachments/assets/2d6f5ee2-da61-4717-9ea8-be6ef047814a)

![13 add 2 lines and synthesis](https://github.com/user-attachments/assets/53b758c2-b7b3-4864-82ce-1babb5971c50)

![14 synthesis complete'](https://github.com/user-attachments/assets/29cabef6-df91-4c71-ac0f-2faa2002e55c)

![15 chip area](https://github.com/user-attachments/assets/d7a9482c-6a0b-47e1-9996-4ea2dd7499e3)


Commands to view and change parameters to improve timing and run synthesis
```
![16 improve slack added few lines](https://github.com/user-attachments/assets/86cb69fe-bef3-4ddf-81d8-d39984356e0b)


# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 14-08_18-31 -overwrite

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

![17 synthesis done](https://github.com/user-attachments/assets/455512bc-5289-441d-a583-b5851773e0b6)

![18 floor plan](https://github.com/user-attachments/assets/7aac441b-dc35-4156-b6cf-572093ebf4c0)

![19 io decap](https://github.com/user-attachments/assets/32bf9125-5d55-4212-af0f-11401cf0d857)


# Now we are ready to run placement
run_placement

```
![20 placement analysis](https://github.com/user-attachments/assets/c7259303-3012-48d0-96e8-4bb430e39fe7)

![21 magic after P](https://github.com/user-attachments/assets/1f13ff5b-c7f6-445f-a117-883fbedf52ed)

![22 magic](https://github.com/user-attachments/assets/1d88a373-d244-43d5-9284-7343cbd17bc9)

![23 magic a](https://github.com/user-attachments/assets/80a48437-d3b0-45e7-a10f-4fc6b389d1f4)


```

Do Post-Synthesis timing analysis with OpenSTA tool.

Newly created pre_sta.conf for STA analysis in openlane directory

![25 pre sta](https://github.com/user-attachments/assets/2fb849e0-f57b-4381-a650-15374d461360)

my_base.sdc

![24 my base](https://github.com/user-attachments/assets/540fb9bd-43e9-42de-b018-d1d60528de53)

![26 sta](https://github.com/user-attachments/assets/5ba8ba96-9723-455a-8f45-34b809688dc5)


# Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 14-08_18-31 -overwrite

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

![29 synthesis with fanout 4](https://github.com/user-attachments/assets/6ff2bc52-6a8e-4975-9e24-237a93d96b4a)

![30 new STA after synthesis](https://github.com/user-attachments/assets/bc1c5928-34c8-4524-a3da-358978c1cc28)

![sta 2](https://github.com/user-attachments/assets/12a12fd4-8603-4cd7-ab3e-6e952d5c10ff)

Finally slack is met 


**Now run Placement**



## Day 5 GDS II Final step

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


