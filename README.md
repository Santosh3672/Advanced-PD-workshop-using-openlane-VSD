# Advanced-PD-workshop-using-openlane-VSD
## This repo contains all the learnings and labs on Advanced PD workshop by VSD. It contains all the informations on RTL to GDSII implementation of a PICORV32 design using openlane flow.
# Table of content
- [Day 1 Inception of open-source EDA, OpenLANE and Sky130 PDK](#day1-inception-of-open-source-eda-openlane-and-sky130-pdk)
 - [Introduction](#introduction)
 - [Day2: Good floorplan vs bad floorplan]
 - [Day3: Design library cell using Magic Layout and ngspice characterization]
 - [Day4: Pre-layout timing analysis and importance of good clock tree]
 - [Day5: Final steps for RTL2GDS using tritonRoute and openSTA]
 
# Day1: Inception of open-source EDA, OpenLANE and Sky130 PDK
## Introduction:
During ASIC design we will come across some terms more frequenlty few of them are listed below: \
**Pad:** Used to communicate with outside world. \
**Core:** Area where the digital logic sits. \
**Die:** Size of entire chip. \
**Foundry:** Fabrication plant for semiconductor chips. \
**Foundry IP’s:** IP’s supported by foundries. \
![ASIC Chip](Images/D1_1.png?style=centerme)

## Introduction to RISCV ISA
RISCV ISA: (Reduced Instruction Set computer V) is an open source architecture of processor based on RISC principle also known as instruction set architecture. The hardware runs on low level opcode.
For running a software/app first the software/app informs the system software which has compiler to convert the high level code to instructions then the instruction of given architecture(intel x86, ARM or MIPS) are converted to opcodes using assembler. \
![How software run](Images/D1_2.png)

## SoC Design using Openlane:
![Openlane ASIC Flow](Images/D1_3.png) \

We can see that it follows typical ASIC design flow. Some of its key features are discussed here. Synthesis exploration is where we try various tried and tested strategies on the design and select the strategy with best performance. After that we do STA on the synthesizes netlist followed by DFT insertion using fault tool. Post that physical implementation is done on OpenROAD.

## Openlane Directory sturcture
The tools are at directory ~/Desktop/work/tools. Inside it we have two directories ‘pdk’ and ‘Openlane’.
Pdk directory has 3 directories skywater-pdk: compatible with commercial tools, open-pdk: has scripts to make it compatible with opensource tools and ‘sky130A’ pdk that are compatible with open source EDA tools. Sky130A has 2 directory libs.ref has files specific to the technologies and libs.tech has files specific to the tools. All the libraries can be found at libs.ref.

**Openlane Flow:** Inside Openlane directory parallel to pdk there is a file named flow.tcl.We need to Invoke flow.tcl on docker, which will start the flow and complete the RTL to gdsii flow, using -interactive switch we can interactively control each step of the flow.
Commands used:
```console
docker
flow.tcl -interactive
```
![Openlane console](Images/D1_4.png)
After invoking openlane flow we need to do following steps as a prerequisite to start working on the flow.
•	**Loading the required openlane packages:** 
```console 
package require Openlane 0.9
```
0.9 is the version of openlane
•	**Preparing directory structure:** Here we will set the design name using prep -design {design_name}, there is a directory named design parallel to flow.tcl, which contains all designs, inside any design we will have source file containing .v and .sdc file and configuration file to override default configuration.
```console 
prep -design {design_name} -tag {tag_name} -overwrite
```
If we want to work on a present tag of the design we can specify that using -tag switch.

We can run synthesis using `run_synthesis` command.

After that we can see that inside design directory for the given design there will be runs directory created with files named as the date and time of the run which contains all the information of the run.
![Post synthesis](Images/D1_5.png)
![](Images/D1_6.png)
![](Images/D1_7.png)
Statistics of the synthesized design. 
Area of design: 198775.6416.
Total cells: 20234.

# Day2: Good floorplan vs bad floorplan
# Day3: Design library cell using Magic Layout and ngspice characterization
# Day4: Pre-layout timing analysis and importance of good clock tree
# Day5: Final steps for RTL2GDS using tritonRoute and openSTA
