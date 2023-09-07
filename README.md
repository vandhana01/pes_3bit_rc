# pes_3bit_rc

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
https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh
- Download the run.sh
- Open terminal
- cd Downloads
- ./run.sh

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
  
