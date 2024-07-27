# NASSCOM--VSD-SOC-design





[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](https://choosealicense.com/licenses/mit/)



![Logo](https://www.vlsisystemdesign.com/wp-content/uploads/2016/12/vsd_logo.jpg)


# Digital VLSI SoC Design and planning Training

Welcome to the OpenLane workshop! In this workshop, we will delve into the process of designing an Application Specific Integrated Circuit (ASIC) from the Register Transfer Level (RTL) to the Graphical Data System (GDS) file using the OpenLane ASIC flow. The flow is composed of several key steps, starting with an RTL file and culminating in a GDS file.

## Lessons Learned

Understanding the RTL to GDS Flow:

1. Grasped the end-to-end process of converting a high-level hardware description to a physical ASIC layout.
Recognized the importance of each step in the flow, from synthesis to sign-off.

2. Synthesis:

Learned how RTL is converted to a gate-level netlist using standard cell libraries.
Identified the different views of cells (Liberty, HDL, SPICE, Layout).

3. Floor and Power Planning:
Understood the significance of floor planning in chip partitioning and I/O pad placement.



## Day 1


The RTL to GDSII flow is a process in VLSI design that converts an RTL
description of a digital circuit into a physical layout ready for fabrication. It
involves stages like RTL synthesis, floor planning, placement, routing, and
ultimately generating the GDSII file format, which contains the layout data.
This meticulous process ensures the final IC layout accurately reflects the
desired functionality and meets fabrication requirements

![image](https://github.com/user-attachments/assets/2b5106fe-f87d-478c-83d8-332de757523e)

## Overview of QFN-48 Chip, Pads, Core, Die, and IPs

VSD Squadron Board: This is a VSD Board that you can see below. Here, we concentrate more on the enclosed region, which houses the "Microprocessor," which we will use the RTL to GDS flow to design from the abstract level to the fabrication level.

![image](https://github.com/user-attachments/assets/ddf592ec-bee3-4064-9a63-c3ce953c2bed)

## Introduction to IC Design components and terminologies

![image](https://github.com/user-attachments/assets/2b6ba079-5154-4bf5-ba5a-46d2a816bc46)
![image](https://github.com/user-attachments/assets/612c63c4-6c4c-4e4e-bcae-51ef652114c6)
![image](https://github.com/user-attachments/assets/99cab89c-ef2a-4624-a7d8-1c4c9790f7f6)
![image](https://github.com/user-attachments/assets/e0b51f1a-aaf3-469f-be8a-3d63d6ff5983)

- Core

   A core is an area in the chip where the fundamental logic of the design is placed. It encapsulates all the combinational circuit, soft and hard IPs, and nets.

- Die

   Die is an area of chip that encapsulates the core and IO pads. Die is imprinted multiple times along the silicon area or wafer to increase the throughput.

- IO Pads

   IO pads are the pins that act as the source of communication between core and the outside world. Pad cells surround the rectangular metal patches where external bonds are made. input,output and power pad.



- IPs

    Foundary IPs are manually designed or need some human interference (or intelligence) essentially to define and create them like SRAM, ADC, DAC, PLLs.
- PDKs

    PDKs are interface between foundary and design engineers. PDKs contains set of files to model fabrication process for the design tools used to design IC like device models, DRC, LVS, Physical extraction, layers, LEF, standard cell libraries, timing libraries etc. SkyWater 130nm is the PDK used in this workshop specifically sky130_fd_sc_hd and openLANE is built around this PDK.

## Introduction to RISC-V
ISA: ISA is known as "Instruction Set Architecture".It is merely a means of interacting with the computer. Generally speaking, we use coding languages like C, Java, and others to write programs that must be performed by the system, but machines are unable to comprehend these languages. Here's when ISA enters the picture. The written codes will be translated from assembly language to binary, or machine comprehensible language, using ISA. The RISC V ISA is the most recent ISA to be published, and it serves this purpose.
![image](https://github.com/user-attachments/assets/0eccb7a7-d0b7-4728-b28d-960b0f79be14)



## From Software Applications to Hardware

In real life, we typically interact with application software (apps) to communicate with hardware. But how does this process work exactly? Between the application software and the hardware, there is a layer called system software. The applications interface with the system software, which then translates them into a language the hardware can understand, namely binary language.

The system software is comprised of several layers:
![image](https://github.com/user-attachments/assets/fa977d4d-8ea1-4a3f-9e3d-83d0fec3ad11)


  -  Operating System (OS): In addition to general tasks like handling input/output operations, memory allocation, and low-level system functions, the OS translates application software into corresponding code in languages such as C, C++, or Java.

   - Compiler: The compiler takes the code produced by the OS and converts it into an instruction set (e.g., .exe files). These instructions are tailored to the specific type of hardware being used.

   - Assembler: The assembler then converts these executable files into binary language, which the hardware can understand and execute to perform the desired operations.

##  OpenLane: Introduction to Components of Open-Source Digital ASIC Design

To design an open-source digital ASIC, several key components are required:
![image](https://github.com/user-attachments/assets/66a8e239-bb3d-4fc8-855b-b82dcd124b41)


   - RTL Designs
- EDA Tools
- PDK Data

What are RTL Designs?

RTL (Register-Transfer-Level) design is a critical phase in the VLSI design flow, focused on creating electronic circuits using integrated circuits (ICs). It specifies a digital circuit by describing the flow of digital signals between hardware registers and the logical operations performed on these signals.
What are EDA Tools?

EDA (Electronic Design Automation) tools are software applications used to design and verify the functionality of integrated circuits (ICs). They ensure that the IC meets the required performance and density specifications.
What is PDK Data?

PDK (Process Design Kit) is a set of files used to model a fabrication process for EDA tools during IC design. This kit includes:

  -  Process Design Rules: DRC (Design Rule Check), LVS (Layout Versus Schematic), PEX (Parasitic Extraction)
 Device Models
Digital Standard Cell Libraries

 I/O Libraries

## Simplified RTL to GDS Flow

The simplified RTL to GDS flow begins with an RTL file and, through a series of stages, produces a GDS file, which can be sent to a foundry for fabrication. The steps in the RTL to GDS flow include:
![image](https://github.com/user-attachments/assets/9c20bdd1-48ab-4ba3-8e17-5938b2b61687)

    Synthesis:
        The RTL file is converted into a circuit using components from the Standard Cell Library.
        Standard Cells in the library have a regular layout with the same height but different widths.
        Each cell has various models based on electrical, HDL, Spice, and layout (abstract and detailed) parameters.

![image](https://github.com/user-attachments/assets/c5ac1b46-6839-4b57-9093-08cf0a212ef8)

    Floor Planning & Power Planning:
        Floor Planning: Determines the position of components on the chip to minimize area, including the placement of I/O pins, ports, and pads.
        Power Planning: Designs the power supply network (VDD and GND) using power rings, power straps, and power pads, typically on the top metal layers for minimal resistance and delay.
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
            Physical Verification Checks: Design Rule Check (DRC) and Layout vs. Schematic (LVS). DRC verifies design rule compliance, while LVS ensures functional correctness against the gate-level netlist.
            Timing Checks: Static Timing Analysis (STA) checks the design for timing violations.


