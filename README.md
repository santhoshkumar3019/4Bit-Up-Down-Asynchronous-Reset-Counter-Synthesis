# 4Bit-Up-Down-Asynchronous-Reset-Counter-Synthesis

## Aim:

Synthesize 4Bit-Up-Down-Asynchronous-Reset-Counter design using Constraints and analyse reports, Timing, area and Power.

## Tool Required:

Functional Simulation: Incisive Simulator (ncvlog, ncelab, ncsim)

Synthesis: Genus

### Step 1: Getting Started

Synthesis requires three files as follows,

◦ Liberty Files (.lib)

◦ Verilog/VHDL Files (.v or .vhdl or .vhd)

◦ SDC (Synopsis Design Constraint) File (.sdc)

 ### Step 2 : Creating an SDC File

•	In your terminal type “gedit input_constraints.sdc” to create an SDC File if you do not have one.

•	The SDC File must contain the following commands;

create_clock -name clk -period 2 -waveform {0 1} [get_ports "clk"]

set_clock_transition -rise 0.1 [get_clocks "clk"]

set_clock_transition -fall 0.1 [get_clocks "clk"]

set_clock_uncertainty 0.01 [get_ports "clk"]

set_input_delay -max 0.8 [get_ports "rst"] -clock [get_clocks "clk"]

set_output_delay -max 0.8 [get_ports "count"] -clock [get_clocks "clk"]

i→ Creates a Clock named “clk” with Time Period 2ns and On Time from t=0 to t=1.

ii, iii → Sets Clock Rise and Fall time to 100ps.

iv → Sets Clock Uncertainty to 10ps.

v, vi → Sets the maximum limit for I/O port delay to 1ps.

### Step 3 : Performing Synthesis

The Liberty files are present in the library path,

• The Available technology nodes are 180nm ,90nm and 45nm.

• In the terminal, initialise the tools with the following commands if a new terminal is being
used.

◦ csh

◦ source /cadence/install/cshrc

• The tool used for Synthesis is “Genus”. Hence, type “genus -gui” to open the tool.

• Genus Script file with .tcl file Extension commands are executed one by one to synthesize the netlist.
          read_libs  <Library Path>
          read_hdl counter.v
          elaborate
          read_sdc input_constraints.sdc 				
          syn_generic
          report_area
          syn_map
          report_area
          syn_opt 
          report_area					
          report_timing > counter_timing.txt			
          report_area > counter_area.txt			
          report_power > counter_power.txt			
          write_hdl > counter_netlist.v 				
          write_sdc > counter_output_constraints.sdc		
          gui_show

#### Synthesis RTL Schematic :

#### Area report:
![Screenshot (184)](https://github.com/user-attachments/assets/dddc004f-a06a-4bf1-a30d-2ccc1a79c633)

#### Power Report:
![Screenshot (185)](https://github.com/user-attachments/assets/c3c949b4-2385-43ed-8553-07f738d4110c)

#### Timing Report: 
![Screenshot (187)](https://github.com/user-attachments/assets/30958e9f-ccbf-4f60-8a97-3e8ea0969a7e)

#### Result: 

The generic netlist has been created, and area, power, and timing reports have been tabulated and generated using Genus.





