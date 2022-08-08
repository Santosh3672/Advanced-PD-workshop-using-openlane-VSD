# Advanced-PD-workshop-using-openlane-VSD
## This repo contains all the learnings and labs on Advanced PD workshop by VSD. It contains all the informations on RTL to GDSII implementation of a PICORV32 design using openlane flow.
# Table of content
 -[Day 1 Inception of open-source EDA, OpenLANE and Sky130 PDK]
  -[Introduction]
 -[Day 2]
 -[Day 3]
 -[Day 4]
 -[Day 5]
 
# Day1: Inception of open-source EDA, OpenLANE and Sky130 PDK
## Introduction:
During ASIC design we will come across some terms more frequenlty few of them are listed below: \
Pad: Used to communicate with outside world. \
Core: Area where the digital logic sits. \
Die: Size of entire chip. \
Foundry: Fabrication plant for semiconductor chips. \
Foundry IP’s: IP’s supported by foundries. \
![ASIC Chip](Images/D1_1.png)

## Introduction to RISCV ISA
RISCV ISA: (Reduced Instruction Set computer V) is an open source architecture of processor based on RISC principle also known as instruction set architecture. The hardware runs on low level opcode.
For running a software/app first the software/app informs the system software which has compiler to convert the high level code to instructions then the instruction of given architecture(intel x86, ARM or MIPS) are converted to opcodes using assembler.
![How software run](Images/D1_2.png)

## SoC Design using Openlane:
![Openlane ASIC Flow](Images/D1_3.png)

We can see that it follows typical ASIC design flow. Some of its key features are discussed here. Synthesis exploration is where we try various tried and tested strategies on the design and select the strategy with best performance. After that we do STA on the synthesizes netlist followed by DFT insertion using fault tool. Post that physical implementation is done on OpenROAD.
