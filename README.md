# pes_elevator 
# Content
- [Steps on Which we would be Working in this ](#Steps-on-Which-we-would-be-Working-in-this )
- [RTL and GLS](#RTL-and-GLS)
- [Installation of ngspice magic and OpenLANE](#installation-of-ngspice-magic-and-openlane)
- [OpenLANE Flow](#openlane-flow)
# Steps on Which we would be Working in this 
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/07cf0d73-6197-4580-9718-92785e2342c4)
**As per Shown RTL(Test bench , Verification) is done and sent to next step Synthesis after that the final stage GLS where we simulate and get the netlist**

## Brief On Elevator Controller
'The provided Verilog code presents the fundamental structure of an elevator controller module, which plays a critical role in managing the operation of an elevator system. Elevator controllers are essential components in modern buildings, ensuring efficient transportation between different floors. This controller module processes a set of input signals, including requests from passengers, the current floor, clock pulses, reset commands, and signals indicating the duration the elevator door has been open and weight exceeding the limit. It uses these inputs to determine the elevator's behavior. When reset, the controller initializes the current floor. During normal operation, it evaluates floor requests, moves the elevator in the appropriate direction, and updates the current floor. It also monitors the door's open duration and the weight inside the elevator to trigger alerts when necessary. The controller then produces output signals, reflecting the elevator's direction, operational status, door alerts, weight alerts, and the current floor, which are crucial for passenger safety and efficient building transportation. This Verilog module is a digital representation of the core logic that governs elevator behavior, an integral part of vertical transportation systems in modern structures.'

### *Illustration of How the elevator controller would look* ( Final Schemetic May Vary)
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/2b725fa9-34af-45f1-a052-152039b44381)

# RTL and GLS
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

## Installation of ngspice magic and OpenLANE

**ngspice**
- Download the tarball from https://sourceforge.net/projects/ngspice/files/ to a local directory
```
cd $HOME
sudo apt-get install libxaw7-dev
tar -zxvf ngspice-41.tar.gz
cd ngspice-41
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
sudo make
sudo make install
```

**magic**
```
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
sudo make
sudo make install
```

**OpenLANE**
```
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git

sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot 
# After reboot
docker run hello-world (should show you the output under 'Example Output' in https://hub.docker.com/_/hello-world)

- To install the PDKs and Tools
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```
## OpenLANE Flow
- First create a folder in you Openlane/design directory and save your design there.
![1](https://github.com/dsingla54/pes_elevator/assets/139515749/f62398b0-2b68-444b-b340-281ff12d48c7)


- Then create a folder named 'src' and save the main verilog code in that folder too and also save it outside the folder as well , with the verilog code also saved
 ![3](https://github.com/dsingla54/pes_elevator/assets/139515749/c8d2b83b-b078-41fb-bd6d-88a6b573d275)

```
sky130_fd_sc_hd__fast.lib
sky130_fd_sc_hd__slow.lib
sky130_fd_sc_hd__typical.lib
```
- create a config.json file outside your src folder.
- all the files are present at the top
![2](https://github.com/dsingla54/pes_elevator/assets/139515749/195c1e73-4765-46e6-917e-5cf2cb3f4552)

Now use command
``` gedit config.json ```
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/20a04948-57ab-44a5-ba9a-1c6f37eea7bd)


### Interactive OpenLane flow
Open terminal in home directory and then type the following:


```
cd OpenLane/ 
sudo make mount
```
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/107a11b0-e74f-4eb1-a256-ca3bfedd5ddd)
 
```
./flow.tcl -interactive
package require openlane 0.9
```
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/f9cc1697-531a-4daa-b523-4a7f16e14183)

```
prep -design pes_elevator
```
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/1ef448b2-9bee-40db-ba77-9bb0ba89ec93)

## Commands That we are gonna use 
```
run_synthesis
run_floorplan
run_placement
run_cts
run_routing
run_magic
run_magic_spice_export
run_magic_drc
run_netgen
run_magic_antenna_check
```
## Synthesis stage:
Synthesis is a fundamental stage in the digital design flow. It takes an abstract hardware description and generates a netlist consisting of logical gates and flip-flops that represent the desired functionality of the design.




- Area report

![image](https://github.com/dsingla54/pes_elevator/assets/139515749/05cf202c-8dc7-47ca-8f8f-d10b5ec87664)

## Floorplan stage:

The floorplan stage in digital integrated circuit design involves creating a high-level layout for the chip, defining the core area, the locations of I/O pads, and other critical structures. It establishes the overall physical framework for the chip design and serves as a foundation for subsequent stages such as placement and routing. During the floorplan stage, designers make decisions about the chip's dimensions, aspect ratio, power grid, and other essential aspects to meet the project's requirements. The goal is to efficiently allocate space for various components while adhering to design constraints, ultimately ensuring that the chip will meet its performance, power, and area goals.

![image](https://github.com/dsingla54/pes_elevator/assets/139515749/062d68c5-a1ba-4642-a7e9-9c42692a163d)

```
magic -T /home/dhruv/OpenLane/pdk/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def pes_elevator.def &
```
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/1ea87b9c-6a59-446a-b7a6-678309fc3f63)
**Zoomed** 
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/804f0c61-c503-47fe-a68b-acc52c3f95bf)

## Placement stage:

The placement stage in digital integrated circuit design involves determining the physical positions of synthesized logic cells on the chip's layout. This critical step aims to optimize the arrangement of cells to minimize wirelength, meet design constraints, and achieve desired performance. Placement typically involves global placement, which provides a rough layout, followed by legalization to ensure cells conform to design rules and spacing requirements. The outcome of this stage is a physical placement file that specifies the coordinates of each cell, serving as the basis for subsequent routing and design verification steps. Efficient placement is essential for optimizing area, power, and signal timing in the final chip design.

![image](https://github.com/dsingla54/pes_elevator/assets/139515749/b41d0cfe-a998-47c4-b5cd-caba2ec54d3d)

![image](https://github.com/dsingla54/pes_elevator/assets/139515749/36bebc80-cbba-4f0f-8ff0-374625677479)

```
magic -T /home/dhruv/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def pes_elevator.def &
```

![image](https://github.com/dsingla54/pes_elevator/assets/139515749/1ea87b9c-6a59-446a-b7a6-678309fc3f63)

- Placement Zoomed.

**Zoomed** 
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/804f0c61-c503-47fe-a68b-acc52c3f95bf)

## CTS(Clock Tree Synthesis) Stage:



The Clock Tree Synthesis (CTS) phase's primary objective is to establish a clock distribution network guaranteeing dependable and synchronized clock signals for all the sequential components, such as flip-flops, within the chip. This phase encompasses the subsequent pivotal procedures:

- Buffer Insertion: In the CTS procedure, buffers are incorporated into the clock network to achieve uniform distribution of the clock signal. These buffers play a crucial role in mitigating clock skew, thereby ensuring simultaneous delivery of clock signals to all sections of the chip.

- Clock Tree Construction: The clock tree is built by linking the buffers in a hierarchical manner, extending from the global clock source (such as a PLL or external input) to the individual leaf-level cells across the entire chip.

- Skew Minimization: Within the CTS phase, the objective is to reduce clock skew, which represents the disparity in clock signal arrival times at various locations in the design. By minimizing skew, the aim is to guarantee that all registers observe the same clock edge concurrently, a critical requirement for the effective operation of the circuit.
- 
- Power Optimization: CTS also involves power optimization techniques to reduce dynamic and static power consumption in the clock distribution network.

- Constraints and Timing: It takes into consideration the design constraints related to clock paths, such as clock-to-q requirements, setup and hold times, and other timing considerations.

- Clock Gating: Clock gating cells may be inserted in the clock tree to save power when certain parts of the chip are not in use, and the clock can be temporarily disabled.

- Command ``` run_cts```
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/dbfe705c-9786-4729-809d-b88ea30c6316)

<br>
- report
  
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/0646077d-e952-40b1-840b-3e0ca936e1e6)
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/2743db56-8d9f-49b1-9a33-4d476ed510f9)
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/18bfb907-c6a2-4b3c-a23b-aaec23460bb5)
## Routing stage:

- The routing stage is responsible for creating the physical wire connections between the placed cells on the chip layout. This involves determining the paths for signal wires, power distribution, and clock signals, while adhering to design rules, avoiding congestion, and optimizing for various factors such as wirelength, signal delay, and power consumption.

- Use Command ``` run_routing ```
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/3f31f44f-9e36-4a4f-8780-fb6c09c10865)
```
magic -T /home/dhruv/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.nom.lef def pes_elevator.def &
```

![image](https://github.com/dsingla54/pes_elevator/assets/139515749/190f41cb-930c-40e0-82fb-68c176b79930)


- **Router zoomed**
  
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/9d70210e-1450-44b8-930a-7cbba4466de7)



- Power report

![image](https://github.com/dsingla54/pes_elevator/assets/139515749/3de14438-b5c5-4ac6-a595-fad47349384a)

- Skew report
![image](https://github.com/dsingla54/pes_elevator/assets/139515749/8050b9f2-0295-49cd-9ef8-c20548ce5f9f)

- Area and Summary report
- ![image](https://github.com/dsingla54/pes_elevator/assets/139515749/a601704b-b754-4c1a-b3da-27c8fb74fd6c)

**Summary**
- Area = 1430 um2
- Internal Power = 1.37e-05  W
- Switching Power = 5.40e-06 
- Leakage Power =  6.47e-10
- Total Power =  1.91e-05
