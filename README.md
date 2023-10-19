# pes_elevator 
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

