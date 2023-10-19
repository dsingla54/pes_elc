# pes_elevator 
## Brief On Elevator Controller
The elevator controller is the central brain of an elevator system, responsible for overseeing and managing its various functions. It employs sophisticated control algorithms to prioritize and respond to user requests, such as calling the elevator from specific floors or selecting destinations within the car. The controller's primary goal is to optimize the elevator's operation, reducing passenger wait times and travel times while minimizing energy consumption. It also plays a crucial role in ensuring safety, constantly monitoring various sensors, and employing safety mechanisms like emergency stops and door protections. Moreover, the controller interfaces with users through a user-friendly control panel, usually present both inside the elevator car and in the building's lobby, allowing passengers to input their desired floor selections. Additionally, the controller has the capability to log usage data, aiding in maintenance and diagnostics, helping technicians detect and address issues promptly. In emergency situations, such as fire alarms or power failures, the controller follows predefined protocols to ensure passenger safety.
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
