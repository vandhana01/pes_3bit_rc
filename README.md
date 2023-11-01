![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/9ecf3d0f-38e6-476c-b64e-fa67fb9b387b)# pes_3bit_rc

# 3-bit ring counter
- A 3-bit ring counter is a type of digital sequential circuit in which a counter composed of flip-flops connected into a shift register, with the output of the last flip-flop fed to the input of the first, making a "circular" or "ring" structure.
- Ring counter is a typical application of shift register, the only change is the output of last flipflop is connected as input to the input of the first register
- The operation of a ring counter is determined by its clock input and feedback configuration.
- Here **The number of states = Number of flip flops used**

<p align="center">
<img width="897" alt="image" src="https://github.com/vandhana01/pes_3bit_rc/assets/142392052/235ff226-3cda-4f91-8358-5829bf0d36ce">
</p>

- **Basic Operation:**
  - A 3-bit ring counter has three flip-flops (registers) connected in a ring configuration.
  - The output of one flip-flop is connected to the input of the next, and the last flip-flop's output is fed back to the input of the first flip-flop, forming a closed loop.
  - The sequence of binary values produced by the counter depends on the clock input and the feedback path.
  - The counter counts in a cyclic sequence of binary values. In the case of a 3-bit ring counter, it counts from 000 (binary) to 111, and then wraps back to 000.
  - The sequence is often referred to as a "ring" because it continuously loops through the same values, just like numbers on a clock face.
  - **clock**
    - "CLK" is associated with digital circuit design and synchronization.
    - The counter is clocked by an external clock signal, typically labeled clk.
    - On each rising edge of the clock signal, the counter advances to the next binary value in the sequence.
  - **over riding input**
    - "ORI" is associated with assembly language programming and microprocessor instructions, here it controls the counter's behavior.
    - If ori is asserted, the temp register is set to 3'b100. This appears to be the initial state or a reset condition for the counter.
    - If ori is not asserted (logic low), the counter performs a shifting operation. It shifts the bits in temp to the right, and the most significant bit (temp[2]) is moved to the least significant position (temp[0]).

<p align="center">
<img width="457" alt="image" src="https://github.com/vandhana01/pes_3bit_rc/assets/142392052/b8791429-5cb2-4e2a-8ac8-e55b11bca3a7">
</p>

## Advantages and disadvantages 
- Advantages and disadvantages of a 3-bit ring counter, as well as counters in general, depend on the specific application and requirements. Here are some general advantages and disadvantages:

## Advantages
- Simplicity: Ring counters are relatively simple to design and implement compared to more complex counter types like binary counters or Johnson counters. They have fewer flip-flops and straightforward logic
- Cyclic Behavior: Ring counters inherently produce cyclic sequences of values. This can be advantageous in applications where you need a repeating pattern or sequence of events.
- Frequency Division: Ring counters can be used as frequency dividers. By tapping into one of the stages, you can obtain a signal with a frequency lower than the clock frequency.
- Applications: Ring counters are used in applications like frequency synthesizers, digital signal processing (DSP), state machines, and LED displays, where cyclical patterns or sequences are required.


## Disadvantages
- Limited Counting Range: A 3-bit ring counter can only count from 0 to 7 (binary 000 to 111). If you need to count to larger values, you would need a larger counter, which increases complexity.
- Uneven Distribution: In some cases, the distribution of states in a ring counter can be uneven. This means that certain states may occur more frequently than others, which can be problematic in applications requiring uniform distribution.
- Synchronization Challenges: Ring counters may require careful synchronization when used in complex systems. Synchronizing multiple counters or combining them with other logic elements can be challenging.
- Limited Functionality: Ring counters primarily perform simple counting operations. They may not be suitable for applications requiring more complex arithmetic or conditional operations.
- Reset Considerations: Ring counters may require reset logic, especially if they need to start from a specific state. Managing resets can add complexity to the design

## Applications
- Frequency Division: Ring counters can be used to divide the frequency of an incoming clock signal. By tapping into one of the stages, you can obtain an output signal with a lower frequency, which can be useful in applications like clock domain crossing and signal synchronization.
- Digital Signal Processing (DSP): In DSP applications, ring counters can be used to generate specific sequences of values or control the timing of various operations within a digital signal processor. They are often used in filters and signal generators.
- State Machines: Ring counters can serve as the basis for simple state machines. Each state corresponds to a specific count value, and transitions between states occur with each clock pulse. This is useful in control systems and finite state machines.
- Timing and Synchronization: Ring counters are used in applications where precise timing and synchronization are essential. They can be part of clock distribution networks or used to generate timing signals for specific tasks.
- Pattern Generation: Ring counters can be used to generate repeating patterns or sequences of values. This is useful in applications like pattern testing and pseudorandom number generation.

## State transition diagram for 3-bit counter
<p align="center">
<img width="457" alt="image" src="https://github.com/vandhana01/pes_3bit_rc/assets/142392052/1b4fb9ef-b4e4-4b82-bf3c-105ca0705b47">
</p>


## Installation

- https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh
- Download the run.sh
- Open terminal
- cd Downloads
- ./run.sh
-  For openlane installation : https://openlane.readthedocs.io/en/latest/getting_started/installation/installation_ubuntu.html



## ---------------------------------------IMPLEMENTATION----------------------------------------

# ---     Simulation      ---

<details>
<summary> Simulation </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


## Simulation
- CODE
  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `iverilog pes_3bit_rc.v pes_3bit_rc_tb.v`
  - `./a.out`
  - `gtkwave pes_3bit.vcd`

- OUTPUT
<p align="center">
<img width="897" alt="image" src="https://github.com/vandhana01/pes_3bit_rc/assets/142392052/6a9bfb4c-47aa-4739-b753-68f99da28215">
</p>  

</details>

# ---      Synthesis      ---

<details>
<summary> Synthesis </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


## Synthesis
- CODE
   - invoke `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog pes_3bit_rc.v`
   - `synth -top pes_3bit_rc`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `write_verilog pes_3bit_rc_netlist.v`
   - `show`
     
- OUTPUT     
<p align="center">
<img width="897" alt="image" src="https://github.com/vandhana01/pes_3bit_rc/assets/142392052/b62632fb-1b87-45e5-812c-d621c63875d6">
</p>

<p align="center">
<img width="897" alt="image" src="https://github.com/vandhana01/pes_3bit_rc/assets/142392052/6cce6667-d95f-42b5-b57b-bc096f370086">
</p>

</details>

# ---Gate-Level Simulation---

<details>
<summary> Gate-Level Simulation </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


## Gate-Level Simulation
- CODE
  - `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v pes_3bit_rc_netlist.v pes_3bit_rc_tb.v`
  - `./a.out`
  - `gtkwave pes_3bit.vcd`

- OUTPUT
  
<p align="center">
<img width="897" alt="image" src="https://github.com/vandhana01/pes_3bit_rc/assets/142392052/a1ae6519-8666-4c22-8049-0ca648191eb3">
</p>

<p align="center">
<img width="897" alt="image" src="https://github.com/vandhana01/pes_3bit_rc/assets/142392052/571dfecf-1770-4d42-8f25-28b8df3112fc">
</p>
  
</details>

# ---   OpenLane flow     ---

<details>
<summary> OpenLane flow </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


## Creating a design folder through OpenLane
- To create a design folder with a default config.json file
- ``cd``
- ``cd OpenLane``
- ``make mount``
- ``./flow.tcl -design <YOUR_DESIGN_NAME_HERE> -init_design_config``

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/0bcb2b3d-2cc5-4330-8c48-179566816581)

- In a new tab,
- ``cd ~/OpenLane/openlane/<YOUR_DESIGN>``
- ``mkdir src``
- ``cd src``
- ``gedit <DESIGN_NAME>.v``


![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/1329c2d8-3a88-432c-ba23-82c92ccb19d3)

- This will open the Gedit text editor with a new or existing file named "DESIGN_NAME.v" for you to edit your Verilog code.
- In Gedit, you can write or edit your Verilog code. Make sure to save your changes when you're done.
- After saving your Verilog code, you can close Gedit.
  
![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/ac4a12e0-19c7-4911-a061-6c0d57c54064)
  
- By default `config.json` file will be created
- The `config.json` file is typically generated or populated with initial settings and design information as part of the OpenLane design flow setup or initialization.
- In most cases, OpenLane will take care of creating and initializing the `config.json` file for you. If you need to add custom information to this file, you can do so after the initial creation or during the design setup.
- You can check your project directory to see if a `config.json` file has been created automatically. If it's not present, you can follow the OpenLane documentation or use OpenLane's commands or scripts to initialize your design, and the `config.json` file should be generated as part of that process.
  
![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/35b9e0a1-41bb-4054-9a9a-f9f61f264f77)

- Add the path to verilog file `dir::src/<DESIGN_NAME>.v` in your `config.json` file for a basic run
- In the JSON, we should add the "src" section within the "designs" block. This is where you specify the path to your Verilog source file.
- You can update it as follows:
  
![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/bbdde173-973d-424e-8366-1463501a6667)

- With this updated config.json, OpenLane will recognize your Verilog source file and include it in the design flow when you run OpenLane for your design.
- Remember to follow the OpenLane documentation and customize the design parameters in the `config.json` file as needed for your project.

# -----Automated Mode-----

<details>
<summary> Automated Mode </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

  
## Running an automated flow 
- An automated design flow typically includes steps such as RTL synthesis, floor planning, placement and routing, and verification, which are essential to turn a logical description into a physical chip.
- Automated design flows, like those used in OpenLane, are critical in the semiconductor industry to design complex and efficient integrated circuits.
- Because, the importance of automated design flows lies in their ability to streamline the design process, improve design quality, and enhance productivity, which is especially critical in fields such as integrated circuit design and electronic system development where precision, efficiency, and speed are paramount.
- To run a basic automated flow using OpenLane, follow these steps:
- Run the OpenLane flow for your design using the following command:
   - `./flow.tcl -design <DESIGN_NAME> -tag <RUN_TAG>`


![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/8b85db94-36d4-4a21-90e5-bffa05ee290a)


- **NOTE**
1. Default Variables: 
    - View the default variables used for the design run in the config.tcl file located at OpenLane/openlane/runs/<SPECIFIC_RUN_FOLDER>.
2. Review Default Values: 
    - Go through all the default values, paths, etc., and decide what changes to make for the next run to improve the design.
3. Viewing Results:
    - Check results related to slack in the synthesis stage, which can be found in the OpenLane/openlane/runs/<SPECIFIC_RUN_FOLDER>/reports/synthesis directory.
    - Examine the AREA stat report for statistics related to design area and cells used in synthesis.
    - Check the STA summary for slack details.
4. Die Area and Core Area:
    - Examine results related to die area and core area in the floorplan directory:
    - The core area file contains coordinates of the core (bottom left and top right corners).
    - The die area file contains coordinates of the entire die.
    - Module area in the synthesis folder is approximately half of the core area because the default core utilization is 50%. You can adjust this by changing the coordinates of the core area using the corresponding variable with a utilization percent as the target.
5. Core Utilization: 
    - Calculate core utilization as core util = module area / core area and adjust it accordingly.
6. Explore All Folders: 
    - Explore all the other folders inside the <SPECIFIC_RUN_FOLDER> to gather more information about the design and the results of each stage in the design flow.

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/d774a1fa-fcda-4e60-bef7-0ea6fdf8dc06)

- It specifies various parameters related to the design and the design flow:

1. `"DESIGN_NAME": "pes_3bit_rc"`: This sets the name of your design, which is "pes_3bit_rc" in this case.

2. `"VERILOG_FILES": "dir::src/*.v"`: This parameter specifies the path to your Verilog source files. It uses a wildcard to include all `.v` files located in the "src" directory.

3. `"CLOCK_PORT": "clk"`: It designates the clock signal's port name, which is "clk" in this case. The "clk" is typically the clock input to your design.

4. `"CLOCK_PERIOD": 12.0`: This parameter sets the clock period to 12.0 time units (e.g., nanoseconds). It defines the desired clock frequency for your design.

5. `"SYNTH_MAX_FANOUT": 14`: This parameter specifies the maximum fanout for logic gates during synthesis. It helps control the loading on the clock network.

6. `"FP_SIZING": "absolute"`: This option indicates that the floorplan sizing is specified in absolute coordinates. The "DIE_AREA" coordinates are set as absolute boundaries, rather than relative to a reference point.

7. `"DIE_AREA": "0 0 500 500"`: The "DIE_AREA" parameter defines the area on the chip where your design will be placed. In this case, it specifies a square area with coordinates starting from (0, 0) in the bottom-left corner and extending to (500, 500) in the top-right corner.

8. `"SYNTH_AUTONAME": 1`: When set to 1, this option enables automatic naming of modules during synthesis.

9. `"FP_PDN_VPITCH": 25` and `"FP_PDN_HPITCH": 25`: These parameters specify the vertical and horizontal pitch for the power distribution network (PDN) components in your floorplan.

10. `"FP_PDN_VOFFSET": 5` and `"FP_PDN_HOFFSET": 5": These parameters define the vertical and horizontal offsets for the PDN components within the floorplan.

This configuration is tailored to the "pes_3bit_rc" design and should be adjusted to match your specific design requirements, target technology, and desired operational characteristics. The "CLOCK_PERIOD" is a critical parameter that determines the clock frequency, so make sure it aligns with your design's performance specifications. The "DIE_AREA" is essential for placing your design on the chip, so ensure it accommodates your design appropriately.  

-  Run ``./flow.tcl -design openlane/pes_3bit_rc`` command after editing `config.json` file wrt errors/warning
    
![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/df1d5cc5-9c34-4336-b44e-59df67e83d5e)

- All the steps are ran successfully
- And the flow is completed


</details>

# -----Interactive Mode-----

<details>
<summary> Interactive Mode </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Running in interactive mode
- OpenLane can also be used interactively, where users can intervene at various stages of the design flow to make manual adjustments, explore design trade-offs, or address specific issues.
- This is especially valuable for research, debugging, and fine-tuning.
    - To run OpenLane in interactive mode, you can follow these general steps:
## Start Interactive Mode:
- `./flow.tcl -interactive`

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/e19cdce6-e1ca-4d43-b790-bee91d9137ba)


## To prep the design type:
- `prep -design openlane/<DESIGN_FOLDER_NAME> -tag <RUN_NAME>`
  
![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/453ac90b-fb94-4222-bba4-a1a19e210f19)

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/d681d3fb-fd61-4932-8bc6-6be0efc30a76)

## Synthesis 
- Synthesis is the process of translating the RTL design description into a gate-level representation using logic gates from a standard cell library.
- `run_synthesis`

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/800bbdab-0760-4718-9270-32d04db01087)

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/e50c83da-3cf0-428a-b1ec-27612eb1370a)

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/d397fa3c-57a3-40e4-b78b-40a9275f3024)



## Floorplan
- The floorplanning stage involves defining the physical boundaries and locations of different functional blocks within the chip's die area.
- Invoke floorplan using command `run_floorplan`

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/b87ac62a-c8fb-4605-a5ed-22b3692d1c2b)

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/5bd06a38-f5e4-4870-b365-e475718e2cb8)

- view floorplan in Magic
- `cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign magic -T sky130A.tech sky130_inv.mag &`

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/384c1c77-f649-485c-847d-9c507a49d3e6)
  

## Placement
- Placement is the process of determining the precise locations of individual standard cells within the defined floorplan.
- Invoke placement using command `run_placement`

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/62b50b72-4fc6-4c39-9a60-a61ab99cbfe5)


## Clock Tree Synthesis
- CTS focuses on the distribution of clock signals across the chip. It ensures that clock signals reach all flip-flops with minimal skew and balanced loads.
- Type the command `run_cts`
  
## Routing
- The routing stage involves the creation of metal interconnections to connect the pins of standard cells, forming the physical wires for data and control signals.
- Invoke routing by `run_routing`

![image](https://github.com/vandhana01/pes_3bit_rc/assets/142392052/c441c06e-7bfa-4f61-b59b-f2818dd3dd01)


</details>  
</details>
