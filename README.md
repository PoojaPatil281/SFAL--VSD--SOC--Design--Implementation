# SFAL-VSD-SOC-Design-and-Implementation
### Day 0 : Tool Installation
1. Install Yosys
- $ sudo apt-get update
- $ git clone https://github.com/YosysHQ/yosys.git
- $ cd yosys
- $ sudo apt-get -y install yosys
  
  ![image](https://github.com/user-attachments/assets/f2070fe1-fc7d-4a75-bff2-667dd5aa553f)

2. Install iverilog
  - $ sudo apt-get update
  - $ sudo apt-get install iverilog
    
    ![image](https://github.com/user-attachments/assets/61149620-e0d8-42ca-95a8-73267d3adba7)
    
3. Install gtkwave
 - $ sudo apt-get update
 - $ sudo apt install gtkwave
   
![image](https://github.com/user-attachments/assets/eb03a0dc-4185-434b-a6c9-6e71df38e979)

# Day 1 :-  Introduction to Verilog RTL design and synthesis
#### 1.	Introduction to open source simulator iverilog

Simulator is a tool which is used for checking the RTL design. RTL design is basically a implementation of specifications so by simulating a design we can check whether design meets the required specification or not. In this course we have used tool called iverilog for simulating RTL design. Simulator works in such a way that it looks for the changes on the input signals and based upon that the output is evaluated. If no change to the input, no change to the output.
Testbench is the setup to apply test vectors to the design to check its functionality.
Block diagram of iverilog based simulation flow.
Design and testbench applied to the simulator and simulator checks for the changes in input and accordingly the output is evaluated and the output file is called as value change dump format file (VCD file). To view VCD file gtkwave tool is used to check the waveform.

### Labs using iverilog and gtkwave 
git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
RTL code of good_mux.v
![image](https://github.com/user-attachments/assets/627160b7-036a-4688-88ee-8b4054c153f2)

Testbench of good_mux.v 
![image](https://github.com/user-attachments/assets/af260eed-1712-41ee-8b8f-79dd2bfc9e2c)

Load mux and its testbench in iverilog
![image](https://github.com/user-attachments/assets/50c94a04-e5b4-4232-91e2-a49947a78f57)



