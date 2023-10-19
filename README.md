# pes_elevator 
## Brief On Elevator Controller
The provided Verilog code presents the fundamental structure of an elevator controller module, which plays a critical role in managing the operation of an elevator system. Elevator controllers are essential components in modern buildings, ensuring efficient transportation between different floors. This controller module processes a set of input signals, including requests from passengers, the current floor, clock pulses, reset commands, and signals indicating the duration the elevator door has been open and weight exceeding the limit. It uses these inputs to determine the elevator's behavior. When reset, the controller initializes the current floor. During normal operation, it evaluates floor requests, moves the elevator in the appropriate direction, and updates the current floor. It also monitors the door's open duration and the weight inside the elevator to trigger alerts when necessary. The controller then produces output signals, reflecting the elevator's direction, operational status, door alerts, weight alerts, and the current floor, which are crucial for passenger safety and efficient building transportation. This Verilog module is a digital representation of the core logic that governs elevator behavior, an integral part of vertical transportation systems in modern structures.

**Illustration of How the elevator controller looks** ( Final Schemetic May Vary)
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/2b725fa9-34af-45f1-a052-152039b44381)


## Iverilog simulation
Commands
```
iverilog pes_elevator.v pes_elevator_tb.v
./a.out
gtkwave pes_elevator_tb.vcd
```
![image](https://github.com/dsingla54/pes_elc/assets/139515749/39c38a04-0ae2-4acf-ae4e-51c4c7b4fbb0)

### Waveform
![image](https://github.com/dsingla54/pes_elc/assets/139515749/1e7d09e8-1033-4dc5-8c54-9c0d84a879d4)

## GLS 

**yosys Simulation**


Code lines

```
read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib
read_verilog pes_elevator.v
synth -top pes_elevator
abc -liberty ../my_lib/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
show
```
![image](https://github.com/dsingla54/pes_elc/assets/139515749/509c4b20-52db-4618-be1c-e86873d823aa)
![image](https://github.com/dsingla54/pes_elc/assets/139515749/78f26c85-4d93-408e-966a-53c6d9ce2733)

**Design**
![image](https://github.com/dsingla54/pes_elc/assets/139515749/baf3f673-734d-4ff5-b7b4-483224c493d7)

**Verification after GLS**
![image](https://github.com/dsingla54/pes_elc/assets/139515749/1e7d09e8-1033-4dc5-8c54-9c0d84a879d4)
