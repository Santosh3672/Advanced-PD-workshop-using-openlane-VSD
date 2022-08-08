# Advanced-PD-workshop-using-openlane-VSD
This repo contains all the learnings and labs on Advanced PD workshop by VSD. It contains all the informations on RTL to GDSII implementation of a PICORV32 design using openlane flow.
# Table of content
- [Day 1 Inception of open-source EDA, OpenLANE and Sky130 PDK](#day1-inception-of-open-source-eda-openlane-and-sky130-pdk)
  - [Introduction to basic IC design terminologies](#introduction)
  - [Introduction to RISCV ISA](#introduction-to-riscv-isa)
  - [SoC Design using Openlane](#soc-design-using-openlane)
  - [Openlane Directory sturcture](#openlane-directory-sturcture)
- [Day2: Good floorplan vs bad floorplan](#day2-good-floorplan-vs-bad-floorplan)
  - [Deciding utilization ratio and aspect ratio](#deciding-utilization-ratio-and-aspect-ratio)	
  - [Defining location of preplaced cells](#defining-location-of-preplaced-cells)
  - [Power planning](#power-planning)
  - [Viewing def file in magic](#viewing-def-file-in-magic)
  - [Binding netlist with physical cells](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#binding-netlist-with-physical-cells)
  - [Congestion aware placement in Openlane using RePlAce](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#congestion-aware-placement-in-openlane-using-replace)
  - [Cell design flow](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#cell-design-flow)
  - [Timing characterization](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#timing-characterization)
- [Day3: Design library cell using Magic Layout and ngspice characterization](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#day3-design-library-cell-using-magic-layout-and-ngspice-characterization)
  - [16 mask CMOS fabrication process](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#16-mask-cmos-fabrication-process)
  - [SPICE simulation of standard cells](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#spice-simulation-of-standard-cells)
  - [Inverter design using openlane](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#inverter-design-using-openlane)
  - [Cell characterization from NGspice waveform](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#cell-characterization-from-ngspice-waveform)
- [Day4: Pre-layout timing analysis and importance of good clock tree](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#day4-pre-layout-timing-analysis-and-importance-of-good-clock-tree)
  - [Timing model using delay table](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#timing-model-using-delay-table)
  - [Setup timing analysis (with ideal clock)](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#setup-timing-analysis-with-ideal-clock)
  - [Clock jitter](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#clock-jitter)
  - [Using the created standard cell in Picorv32a design](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#using-the-created-standard-cell-in-picorv32a-design)
  - [Clock Tree Synthesis](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#clock-tree-synthesis)
  - [Timing analysis after CTS with real Clocks](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#timing-analysis-after-cts-with-real-clocks)
- [Day5: Final steps for RTL2GDS using tritonRoute and openSTA](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#day5-final-steps-for-rtl2gds-using-tritonroute-and-opensta)
  - [Routing and DRC](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#routing-and-drc)
  - [Freatures of TritonRoute](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#freatures-of-tritonroute)
  - [Working of TritonRoute](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#working-of-tritonroute)
  - [Routing on openlane](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#routing-on-openlane)
 - [Reference](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#reference)
 - [Acknowledgement](https://github.com/Santosh3672/Advanced-PD-workshop-using-openlane-VSD/blob/main/README.md#acknowledgement)
 
# Day1: Inception of open-source EDA, OpenLANE and Sky130 PDK
## Introduction to basic IC design terminologies:
During ASIC design we will come across some terms more frequenlty few of them are listed below: \
**Pad:** Used to communicate with outside world. \
**Core:** Area where the digital logic sits. \
**Die:** Size of entire chip. \
**Foundry:** Fabrication plant for semiconductor chips. \
**Foundry IP’s:** IP’s supported by foundries. \
\
![ASIC Chip](Images/D1_1.png)
\
## Introduction to RISCV ISA
RISCV ISA: (Reduced Instruction Set computer V) is an open source architecture of processor based on RISC principle also known as instruction set architecture. The hardware runs on low level opcode.
For running a software/app first the software/app informs the system software which has compiler to convert the high level code to instructions then the instruction of given architecture(intel x86, ARM or MIPS) are converted to opcodes using assembler. \
\
![How software run](Images/D1_2.png)

## SoC Design using Openlane:
\
![Openlane ASIC Flow](Images/D1_3.png) \
\
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
\
![Openlane console](Images/D1_4.png)
\
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
\
![Post synthesis](Images/D1_5.png)
![](Images/D1_6.JPG)
![](Images/D1_7.JPG)  \
\
Statistics of the synthesized design: \
Area of design: 198775.6416 \
Total cells: 20234 

# Day2: Good floorplan vs bad floorplan
## Deciding utilization ratio and aspect ratio:
If we add the area of all the std cells in the design and make a floor plan with a core size of that number then it will have utilization ratio of 100%. \
\
<img src="Images/D2_1.png" width="300"> \
\
*Design with 100% utilization* \
Utilization factor is defined as: \
**Utilization factor** = Area occupied by the netlist / total area of core. \
100% utilization is not practical as there is no room left for other cells and routing. \
**Aspect ratio** = Height/ Width of the core
## Defining location of preplaced cells:
What are preplaced cells?
These could be block of digital logic which have can be used multiple times but have more than one logic gates hence we just need to know about its I/O pin usage and use them like a Blackbox provided we know how to use them. Examples of such blocks are IP’s, memories, etc.
The preplace cells are placed based on design details for example if a memory cell has lot of interaction with input ports on the left side it would be better to place them near that port. Once it is placed, we don’t move them in further steps of the flow.
Adding Decap cells to the preplaced cells: The physical wires have physical dimension hence they have resistance, capacitance, and inductance as well. Due to which there will be voltage drop. This voltage drop might cause the output voltage of cells to be low enough to be on the undefined logic region which could be disastrous for the design.
To prevent this phenomena, we add decoupling capacitance: \
\
![](Images/D2_2.png "Decoupling capacitor supplies energy to the cells when supply voltage is low")
\
As capacitor is an energy storing device it will deliver voltage to the logic near them when the supply voltage is low prevents any voltage drop across the logic. It decouples the circuit from main supply. \
\
![](Images/D2_3.png "Design with preplaced macros and decap cells around them") \
\
Design with preplaced cells and decap placed around them.
## Power planning: 
We can have many macros, memories or std cells in the design and they can have a huge current demand. We can’t have decoupling capacitor on each of the nets because of Voltage droop and Ground bounce.
Suppose a 16-bit bus is connected to Decap cell then if the logic is inverted then for all the bits transitioning from 0 to 1 will charge the capacitance this will cause droop in power pin and for all bits going from 1 to 0 will discharge capacitance and there will be increase in ground voltage callsed ground bounce.
If there was power supply in each of the cells, then we wouldn’t require decap cells to overcome voltage drop issue.
\
<img src="Images/D2_4.png" width="450" height="350"> <img src="Images/D2_5.png" width="450" height="350">

## Pin Placement
In the design apart from the std cells the input and pins are also required to be placed judiciously since good placement of pins can save us routing resources and net delay. It requires a good collaboration between frontend and backend team. 
Post that we need to block the placement of cells outside core area by placement blockage.

## Floorplan using Openlane:
Floorplan is run using ‘run_floorplan’ command when run interactively. It will run with default configuration, we can change it in the configuration directory parallel to flow.tcl. The configuration can be changed in config.tcl or in {pdk name}_config.tcl. The priority is as follow: \
	```console
	Floorplan.tcl << config.tcl << {pdk name}_config.tcl
	``` \
Floorplan was run with changing IO layer number configuration, after the run the def file was generated. \
\
![](Images/D2_6.png) \
\
The DEF files is shown below, it is a large file with around 37k lines. \
\
![](Images/D2_7.png) \
\
1 micron = 1000 database unit. So area of die = (660685/1000 um) * (671405/1000 um) = 443587.2124 um sq. \
Visual representation of FP picorv32a.floorplan.def.png generated by run_floorplan. \
\
![](Images/D2_8.png) \
## Viewing def file in magic:

Command used: 
```console
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef  def read picorv32a.floorplan.def &
```
-T option takes techlef file, \
lef read taked the merged.lef files that was generated while starting Openlane has cell and layer information. \
Def read takes the current floorplan def file.  \
![AB](Images/D2_9.JPG) \
![BA](Images/D2_10.JPG) \
\
Design after floorplan
\
![](Images/D2_11.JPG) \
\
Decap cells and Tap cells in the design

## Binding netlist with physical cells:
All logic gates are physically shaped as a rectangle be it an AND gate, Mux or D FF. This information is stored in libraries that contain physical information as well as timing, noise and other necessary information required for implementation. It also contains different variations of a single logic gate like different size(drive strength), speed, threshold voltage(vt), etc. 
After floorplan we need to place the netlist in the core, so we need to bind the netlist with physical cells. Then we can place those physical cells on the core. This placement also needs to be done judiciously based on the design so that cells that are communicating more with a port or block are placed nearby this will save routing resource, avoid congestion and reduce delay to meet timing. \
\
![](Images/D2_12.png) 
\
On above figure we have design on right and placement of gates on right. For orange and yellow FF, the placement was easy as its input and output ports are on the same row. For blue and yellow FF, it is difficult as their input and output pins are placed diagonally opposite. For green FF it has additional problem due to a preplaced block.
For long wire between two pins, we can add repeaters(buffer) to maintain signal integrity. For example, here we can add one or two buffer between Din2 and yellow FF1. Post that the timing is checked to see if the placed design can run at the desired frequency. Here we assume clocks to be ideal and check setup timing. 
Based on the timing results we can either modify the placement or add buffers.
Library Characterization and modelling:
In synthesis we convert RTL to logic gates then move to floorplan placement all the way to signoff. In all these steps the standard cells are common. The libraries are provided with various models that can be understood by all the tools in PD flow.

## Congestion aware placement in Openlane using RePlAce:
Placement occurs in two stage global and detailed placement. The placement algorithm tries to reduce half parameter wire length. Placement is run using `run_placement` command. 
To view placed design in magic tool use below command:
```console
magic -T ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def picorv32a.placement.def
```
\
![](Images/D2_14.PNG) 

Placed design in magic tool. \
\
![](Images/D2_13_1.PNG) \
![](Images/D2_13_2.PNG) \
\
We can see endcap cells, tap cells, std cells, and pg grid being made. 

## Cell design flow:

As discussed earlier we have library of the std cells with different varieties and each have multiple models for different tools. The cell design flow is discussed \
here. \
\
![](Images/D2_15.png) \
\
For cell design flow we need inputs those are PDKs, DRC & LVS rules (required by foundry), SPICE models (with all physical parameters), library and user defined specs.
Dimension of cell: the height of the cell should be same for all cells so that VSS and VDD will be laid. Width of the cell can be varied wider cells for high drive strength cells. \
Supply voltage: It will be determined by the user (top level designer) and cell designer has to design cells based on that voltage. \
Metal layers: It could be on M1 or M2 or M3 based on user requirement. \
Then based on the given input cell designer will start designing cell. Designer does spice simulation to design circuit like makil w/l of pmos double w/l of nmos, selecting w/l ratio for desired Id value. After which CDL(circuit descriptive language) is given as output.  \
Post that layout design will start. To design layout we first get the CMOS design of the circuit with PMOS and NMOS. Then derive the graphs of PMOS and NMOS network as shown below. \
\
![](Images/D2_16.png) \
\
Here we are discussing about Euler’s path + stick diagram method which gives layout with best performance and best area. In this method after we derive network graph we derive Euler’s path which is the path that is traversed once. For above example it is A-C-E-F-D-B. \
Then we create a stick diagram of the order of Euler’s path and make connection according to the design. Post that we convert it to layout while adhering to the foundry rules and user input rules. \
\
![](Images/D2_17.png) \
\
With the final layout completed we will produce its GDSII, LED and extract its spice netlist (.cir).
After layout we need to the do cell characterization. Steps included in this process are:
1.	Read the model files 
2.	Read the extracted spice netlist
3.	Recognize the behavior of the cell
4.	Read the subcircuit of the cell
5.	Attach the necessary power source
6.	Apply the required stimulus.
7.	Provide necessary output capacitance
8.	Provide necessary simulation command (transient, DC, AC simulation)

After all these steps we feed the configuration file to a characterization software called GUNA which will generate timing, power and noise characterization. 

## Timing characterization

In timing characterization we need to know the variables with which the GUNA software will model the cell, those variables are related to input waveform like:
1. slew_low_rise_thr
2. slew_low_fall_thr 
3. slew_high_rise_thr
4. slew_high_fall_thr 
5. in_rise_thr
6. in_fall_thr 
7. out_rise_thr 
8. out_fall_thr

They contain the value at which we need to calculate the slew rate or delay. \
For example we need to calculate the propagation delay for falling edge of a buffer and in_fall_thr and out_fall_thr are 50% each then we need to subtract the time when output is 50% with the time where input is 50%.  If we want to calculate delay from 40% of in_rise_thr then we can change this variable in GUNA configuration. Correct choice of delay is very important else we could get negative delay due to different slew rate of input and output. \
For example, to calculate transition time we subtract time on slew_high__rise_thr with time on slew_low_rise_thr. 

# Day3: Design library cell using Magic Layout and ngspice characterization
## 16 mask CMOS fabrication process
It is a detailed process that is followed to fabricate CMOS circuits. It starts from p-substrate then on it various layers are laid followed by mask layer which mask certain part of the subsrtate on the exposed part of the mask UV rays are passed to remove certain layers. The process is repeated for 16 times as the name says after which we have both PMOS and NMOS creates as well as the routing metals above them are also created. \
The whole process is very long and has been documented in a separate github repo: https://github.com/Santosh3672/16-mask-CMOS-fabrication-process \
## SPICE simulation of standard cells:
For SPICE simulation of any cell, first we need to create the spice deck which contains following information: \
•	Input and output pin connection and connectivity between nmos, pmos, capacitances, etc. \
•	Component values such as value of capacitances, W and L value. Input, output and supply voltage value is also defined. \
•	Identify nodes: nodes are points between which we have devices or passive elements. \
•	Naming of the nodes.  \
Based on node names and component names and their values we can write the spice model in text which can be understood by the tool. \
\
![](Images/D3_1.png) \
\
In above example we can see circuit of inverter with all components values and nodes named. With those names and values the SPICE we defined the circuit textually followed by defining the input and output voltages and simulation environment. It is followed by calling spice library model from foundry that contains all the physical parameters required for simulation. \
In CMOS the mobility of n carries is more than p type hence we need to have higher Wp/Lp than Wn/Ln so that switching threshold will be half of the Vin. It is required to equalize the rise and fall delay. \
*Switching threshold (Vm):* It is the point where the DC characteristics of CMOS intersects with Vin = Vout curve. \
\
![](Images/D3_2.png) \
\
VSD cell design github repository: https://github.com/nickson-jose/vsdstdcelldesign

## Inverter design using openlane:
The nwell and pwell contact are made to Local interconnect using nsubstratecontact and psubstratecontact respectively and LI are connetcet to M1 using licon. Then as per above theory we have built the cell layout we need to ensure there are no DRC issue. \
Then we need to ensure that the cell is functioning as we want we can do it using SPICE modelling in ngspice. For that we need to extract parasitics from layout. By creating ext file on magic command is `extract all`. Which is followed by setting threshold R and C using `ext2spice cthresh 0 rthresh 0`. Then we create the spice file using `ext2spice` command. \
```console
	extract all
	ext2spice cthresh 0 rthresh 0
	ext2spice
```
\
![](Images/D3_3.png) \
\
Spice file created from magic layout tool for ngspice analysis \
\
Here the input voltage and supply voltages are not defined as they were not defined in magic tool. Also the model files of mos are to be defined that came with the github repo. For simulation we also need to define the simulation type in the spice netlist. After which the SPICE file looks like: \
\
![](Images/D3_4.png) \
\
Now we are ready to run spice simulation we can invoke ngspice using `ngspice {spice_file_name}`.
On ngspice terminal we can plot IO curves using `plot y vs time a` command:
```console
	ngspice {spice_file_name}
	plot y vs time a
```
\
![](Images/D3_5.png) 
\
## Cell characterization from NGspice waveform:
*Rise transition:* Time taken by rising signal at 20% = 2.181 ns \
		Time taken by rising signal at 80% = 2.245 ns \
Rise transition = (2.245-2.181) ns. = 64 ps. \
Similarly, *fall transition* = 4.095 ns - 4.052 ns = 43 ps. \
\
*Propagation delay fall* = 4.077ns – 4.05ns = 27ps \
*Rise delay* = 2.21ns – 2.15ns = 60ps 


# Day4: Pre-layout timing analysis and importance of good clock tree
## Timing model using delay table
In cell design we need to ensure that the pins are located at the intersection of vertical and horizontal routes. In sky130 process the layer connected to cell is of local interconnect we can check it by creating grid with the pitch and offset values from track.tech file and see if the grids are intersecting at pin location. \
Then we need to define the ports of the cells and their functionality using port command in magic before creating LEF file for PR tool. To create LEF file use command `lef write {optional file_name}`. \
By using clock-gating cells we can turn off some clocks and save power. The input transition and output load might vary for a cell hence calculating delay of cell needs to be done for each time these values are changed. Doing a complex spice model would be very time consuming hence to solve that we have delay table where input slew and output load values are written in rows and columns and the delay for certain transition and load are filled using spice model.  \
\
![](Images/D4_2.png) \
\
For example, if the input slew is 60ps and load is 50fF delay would be x15. For any values not in the table we can find delay using linear interpolation. \
While creating clock tree we need to ensure that the skew very low for that we need to find delay using above method and take care of the issue at an early stage of CTS. \
## Setup timing analysis (with ideal clock):
Ideal clock means clock tree not built (no skew). So on 0s clock reaches launch flop and at T(time period) it reached capture flop. So the delay of launch flop and combinational logic should be less than time period. But in practical case there should be a finite time require by the D input to be stable before a clock edge called setup time. So equation is Launch flop delay + combinational delay + setup time < time period.
\
![](Images/D4_3.png) 
\
## Clock jitter:
Clock is produced by PLL or some other source which is real practical source and it might not generate clock at exact times the clock edge time might have some variation than the expected time this is called clock jitter. We need to model the jitter in our equation, in worst case clock period could be less than expected hence setup equation becomes: \
```console
θ< T – S – SU
```
Where: θ = Launch flop delay + combinational path delay \
	T = Time period, S = setup time, SU = Setup uncertainty (clock jitter) \
We can do STA in Openlane flow using opensta tool, there we can analyse the reason of failure of timing paths. Some of the techniques to reduce timing violation are: \
•	Reduce high fanout nets since they have high output capacitance causing high delay. \
•	In case of chains of buffer after buffer try to fix first buffer as its high delay will add to slew of next buffer, upsize the first buffer. \

## Using the created standard cell in Picorv32a design:
We need to add LEF files in src folder of design. Then this file needs to be added in the library. Apart from the LEF file we also need to define other information about our cell as we can see in the library. Also, we need to define them for slow, typical and fast corner. It came with the GitHub link of vsddesing for cell design so we will copy them to the src folder. \
Adding the library files will not automatically tell Openlane flow to include them during synthesis we need to add their path in config.tcl as well. \
Command ‘prep -design picorv32a -tag 03-08_16-04 -overwrite’ to run Openlane of a previous run and overwrite it. After adding the designed cell to the library, we ran synthesis again and saw huge violations in timing. The synthesis strategy was set to AREA 0. Then we changed the strategy to different AREA numbers possible like AREA 1 and AREA 2 the violations were same. \
Post that I changed the strategy to Delay 0 which focuses more on reducing delay of paths. After that all the violations were gone. The summary of design in both situations are tabulated below: \
|               	|     Synthesis   Strategy    	|     WNS (ns)    	|     TNS (ns)    	|     Area (um^2)    	|
|---------------	|-----------------------------	|-----------------	|-----------------	|--------------------	|
|     Before    	|     AREA 0                  	|     -23.89      	|     711.59      	|     147712.9184    	|
|     After     	|     DELAY 0                 	|     0           	|     0           	|     196832.528     	|

We can see that when tool focuses on delay(with DELAY 0 strategy), area is not priority hence the paths are made timing clean by increasing area. \
\
![](Images/D4_1.png)
\
## Clock tree synthesis:
It is the step where we connect clock port with all the sequential elements of the design. The main objective is to reduce skew of the clocks. For which H-tree is and effective method. In this method we create clock in H shape and iteratively create other branches in H shape. This method ensures that the wire length to all flops is similar. \
After H-tree is created we need to add repeaters at regular interval so that the shape of the clock signal is not distorted due to the high capacitance of the clock path. \
\
![](Images/D4_4.png) \
\
Post that we need to do timing analysis with the real clocks with skews. \
*Clock net shielding:* Clocks nets are critical nets and we don’t want it to be affected by crosstalk from other nets. To do that we shield the clock net with additional layer. This protects the clock nets from glitch (causing serious problems) and delta delay(increasing skew) effect. \
\
![](Images/D4_5.png) \
\
Shielding breaks the coupling capacitance between critical and other nets. After shielding the clock nets we can do static timing analysis on the design. \
The command to run cts in Openlane is `run_cts`: some of its configuration settings are `CTS_TARGET_SKEW`( target skew in ps), `CTS_ROOT_BUFFER`(name of cell inserted in tree), `CLOCK_TREE_SYNTH`(enable cts for triton cts), `CTS_TOLERANCE` (tradeoff between qor and runtime) 
```console
	run_cts
```
After running cts flow it creates another netlist named as `{design name}.synthesis_cts.v` \
\
 ![](Images/D4_6.PNG) \
 \
 ![](Images/D4_7.PNG) \
 \
All the command run before like run_synthesis, run_placement, etc are procs of tcl which is similar to functions. They are present in scripts/tcl_commands/ inside the Openlane directrory. \
\
 ![](Images/D4_8.PNG) 
## Timing analysis after CTS with real Clocks
Static timing analysis after CTS becomes more practical, now the difference launch and capture clock edge will be different from the time period by the value of clock skew. \
Now, setup requirement is: 
```console
(θ + D1) < (T + D2) – S – SU
```
Where, D1 and D2 are launch and capture clock arrival time respectively. \
LHS of above equation is data arrival time and RHS is data required time. Data required time subtracted by data arrival time is called slack which should be positive for above equation to hold. \
With real clock we must also check hold violations. Hold time is the minimum time required for the input of a flop to be stable after a clock edge has been passed so we analyse for same clock edges of launch and capture flop. In ideal case the equation becomes: \
`Θ > H`, where H is the hold time of the flop.  \
In CTS design with real clocks, the equation becomes,
```console
Θ + D1 > H + D2
```
The jitter is not an uncertainty here as we will be analysis for the same clock edge same uncertainty both sides (for half cycle hold paths we might have to consider them). Due to this the uncertainty of hold analysis is lower compared to setup analysis uncertainty.

# Day5: Final steps for RTL2GDS using tritonRoute and openSTA
## Routing and DRC:
During routing stage, the pins of placed are routed using metal layers to complete the signal nets.
One of the routing algorithms is Lee’s maze routing algorithm. The aim is to do routing with very less zig zag shaped and have as much L shaped routes between 2 pins as possible. The algorithm works as: \
•	It creates routing grid in the core \
•	Then it identifies source and target and put them in grids. \
•	Then it labels the adjacent grid box of source with number 1, then it labels the adjacent grid box of grid 1 as 2 then this process continues. \
•	The above process should not choose any blockage area. It is continued till we reach the targed grid box. \
•	Once the target is reached, we know the shortest distance from source to target. \
•	The path from source can be tracked by moving adjacent numbers in grid box, we can have multiple paths available. \
\
![](Images/D5_1.png) \
\
After routing we need to ensure that the foundry rules are followed these rules are called design rule check DRC, which are a set of rules from foundry that are required to manufacture a chip. Rules like minimum width, minimum area, minimum spacing, etc are included in DRC if these rules are violated the opto-lithography process will fail. The value of the threshold values like minimum via width, wire width, etc comes from experiments performed by foundry. \
To know the last run done on openlane echo the env variable “CURRENT_DEF”. Our last run was CTS next step is routing. But before that we need to generate power distribution network (PDN) using ‘gen_pdn’ command. But in the new flow the PDN generation occurs in floorplan stage which can be seem in floorplan layout hence it is not needed. In a PDN power flows from power pads to power rings then the power straps that are tapped from power rings provides power to standard cells. \
\
![](Images/D5_2.png) \
\
Now we can proceed with routing stage using ‘run_routing’ command. The routing configurations has switches like GLB_RT_MAXLAYER, ROUTING_STRATEGY (tradeoff between qor and runtime), GLB_RT_ADJUSTMENT, etc. Routing is run using Tritonroute tool it also runs routing using two steps: \
•	Global Route: In this method the entire routing region is converted to a 3D graph on which routing paths are found which provides routing guide for the next stage. \
•	Detailed route: This method ensures that the wires and vias are laid in accordance with the global route results. \
## Freatures of TritonRoute:
•	Performs initial routing
•	Preprocesses route guide: it attempts to follow global route as much as possible, given the guide should have unit width and be in preferred direction.
\
![](Images/D5_3.png) \
\
On the routing guide, the routes on non preffered direction are splited and then merged orthogonal edged routes after that the edges parallel to preferred routing direction are bridged with additional metal layers at last the non preferred directions are converted to another layer (M2 here). \
•	Inter-guide connectivity: Two guides are connected if they are on same metal layer and touching or if they are on neighbouring metal layer with non zero overlapping area(connected through vias). \
Each pins of cell should have a pin shaped overlap with a routing guide. \
•	Intra-layer parallel and Inter-layer sequential panel routing: It means that routing in a layer will occur parallely after that only the routing of the next layer will start. Like M1 routing will occur first followed by M2 routing then M3 and so on. \
## Working of TritonRoute:
*Input:* LEF,DEF, Preprocessed route guides. \
*Output:* Detailed routing solution with optimized wire lengths and via count. \
*Constratined:* Route guide honouring, connectivity constraints and design rule. \
*Handling connectivity:* The goal is to find list of access points to compete routing guide. Access point is a box in routing grid that has connection to upper layer, lower layer, pin or IO ports. \
One of the routing guide is to find minimal spaning tree that follows the routing guide.
## Routing on openlane:
In openlane routing stage is started using `run_routing` command.
```console
run_routing
```
\
![](Images/D5_4.png) \
 ![](Images/D5_4_3.PNG) \
 \
 It took 57 iterations with a runtime of 17 minutes and there are no violations post routing. \
Parasitic extraction is also included in run_routing in new version of openlane we can check it from the proc file of run_routing. \
\
![](Images/D5_4_1.PNG) \
 ![](Images/D5_4_2.PNG) \
 \
The flow also dumps a png file of the def file which can be viewed without any tool. \
\
![](Images/D5_5.png) \
\
Snippet of picorv32a.def.png after routing

# Reference
1. VLSI System Design: https://www.vlsisystemdesign.com/
2. OpenLANE: https://github.com/The-OpenROAD-Project/OpenLane
3. RISCV: https://riscv.org/

# Acknowledgement
1. [Kunal Ghose](https://github.com/kunalg123): Co-founder, VSD Corp. Pvt. Ltd.
2. [Nickson Jose](https://github.com/nickson-jose)
