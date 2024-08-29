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

a.out file (VCD file) is created.
Load the .vcd file into gtkwave generator. 
![image](https://github.com/user-attachments/assets/3a56bfbf-2857-4731-bea4-ba6f4efa004c)

![image](https://github.com/user-attachments/assets/f927d3ab-f4bc-467b-84b4-8ff89e1a5ad4)

### Introduction to Yosys and logic synthesis

Yosys is the synthesizer tool used for converting RTL to netlist. Netlist is the representation of design in the form of standard cells present in .lib. 
![image](https://github.com/user-attachments/assets/5754c11e-9bf2-48b7-b080-d98cac6478ba)

This synthesis can be verified by applying synthesized netlist and testbench to the iverilog and output vcd file which can be viewed in gtkwave should be  same as output observed during RTL simulation.
![image](https://github.com/user-attachments/assets/6834edb6-5e46-4d37-ab45-20c4a3418ad0)

Introduction to Logic Synthesis :-

![image](https://github.com/user-attachments/assets/d7acdf30-ec7c-4d50-ad96-9769411178b7)

Labs using Yosys and Sky130 PDK’s

![image](https://github.com/user-attachments/assets/de8f5198-eaf8-4b12-aaca-8b5346148ca9)

![image](https://github.com/user-attachments/assets/8d4e377a-d545-4181-a15d-e3a38b76cf64) 

![image](https://github.com/user-attachments/assets/50c99c37-f1e7-4544-89ed-83ff95edfb54)

![image](https://github.com/user-attachments/assets/61c18c52-0877-4cdb-8f89-212a6be0ab07)

![image](https://github.com/user-attachments/assets/7b3f1ed3-b047-4b07-8f52-66bd3fc7db34)

# Day 2 : Timing libs, hierarchical vs flat synthesis and efficient flop coding styles
### Lab Introduction to timing.libs

Lets first understand the lib name. Here lib name is sky130_fd_sc_hd_tt_025C_1v80  where 
- tt stands for typical
- 025C stands for temperature
- 1v80 stands for voltage of 1.8v
Libraries are characterized based on Process Voltage Temperature.
Process : Variation due to Fabrication
Voltage : Variation due to voltage
Temperature : Variation due to Temperature.
.lib contains information about :
- technology here technology used is cmos, delay model, units of time(ns),voltage(V),power(nW),current(mA),resistance(Kohm),capacitance(pf) ,
- Operating conditions (PVT) ,
- Information about all the standard cells and its leakage power,area,pin related information such as input capacitance,power and delay associated with that pin,
- timing information of cell such input transition and output load.

Observation : As the size of cell increases delay decreases, power and area increases.


Hierarchical vs Flat synthesis :
![image](https://github.com/user-attachments/assets/b1841855-42e4-4131-b3a8-ffb5e1aeed0b)

Hierarchical vs Flat synthesis :-
RTL code of multiple_modules.v

![image](https://github.com/user-attachments/assets/9c2eb924-119e-4b4e-af4e-76aac6962314)

Submodule 1 has AND gate and submodule 2 has or gate. This is an example of hierarchical synthesis.
Before synthesis logic is :

![image](https://github.com/user-attachments/assets/e0db1f48-0600-4831-b027-ce5a26175b5d)

![image](https://github.com/user-attachments/assets/b3de1e36-6bff-4684-ace6-16d39f4959fd)

![image](https://github.com/user-attachments/assets/3632b4e0-7f25-4b7c-a026-0ee9da4eae09)

![image](https://github.com/user-attachments/assets/43929ffb-e6c7-4c48-a215-570acc0b4b11)

![image](https://github.com/user-attachments/assets/194bfdcc-819e-4361-80bc-77f39b132601)

![image](https://github.com/user-attachments/assets/5427c4d2-3254-41ae-bf28-9ed1c24f2097)

In hierarchical synthesis both the modules are synthesized separately.
Logic after synthesis :-

![image](https://github.com/user-attachments/assets/e447c625-f04d-4462-9cf6-ea96326ca8c3)


After synthesis,tool rather than applying inputs a and b directly to or gate, a and b are passed through inverter and then NAND gate. Tool chooses NAND implementation because in CMOS stacking PMOS in OR gate is bad as PMOS has poor mobility and to improve this we have to make sure the cell is wider in order to get appropriate output.

Flat synthesis 
In flat synthesis, both the modules are instantiated under the top module.

![image](https://github.com/user-attachments/assets/34079bb9-138d-43a3-bca6-e31212b6ae7b)

![image](https://github.com/user-attachments/assets/a4c34620-238f-4296-bd3f-49dc7059fc46)

![image](https://github.com/user-attachments/assets/af4838e2-7dc4-4a32-984b-70eb82d25a53)

![image](https://github.com/user-attachments/assets/c87f47fa-0b4e-4368-81b8-aeea8345fef3)

Submodule Level Synthesis 

![image](https://github.com/user-attachments/assets/7b96b49c-30c8-4c88-a0c5-32da31f1527c)

Here synthesis is done at submodule1 level

![image](https://github.com/user-attachments/assets/4dca2f07-8106-49cb-93e3-a59cf0d2a2dd)

![image](https://github.com/user-attachments/assets/8b3b3942-d1be-4436-b1fc-02995e009769)

![image](https://github.com/user-attachments/assets/66fc9384-dda6-44a1-9810-bf6816441e84)

Why submodule level synthesis is needed?
For example, consider a design called multiplier and multiplier is instantiated for a multiple times. So instead of synthesizing multiplier for multiple times we instead synthesize multiplier for one time and replicating it for multiple times and then stitched that netlist to the top level to save time.
Module Level Synthesis is preferred when : 
- we have multiple instances of same module.
- Divide and conquer : When the design is very massive in that case we divide the design into small portion then give it to tool so that we can get appropriate netlist and then stitched that netlist to the top level.
To synthesize the submodule Independently command used is : -
synth -top module_name

Various Flop Coding Styles and Optimization
- Why do we need flipflops?

In digital circuits, glitches refers to the unnecessary signal transitions in a combinational circuit and it can occur due to the different propagation delays of the signals in the combinational circuits so to avoid glitch flipflops are used in such a way that it will give stable output at the specific clock edge  eventhough flipflop input is glitchy.
flipflops are used in between the combinational circuits so flipflop acts as a synchronizer. To control the initial state of flipflop reset/set signals are used and this control signals can be synchronous or asynchronous.

### Flipflop coding styles 

![image](https://github.com/user-attachments/assets/54d56f5e-bbf4-4537-8b74-b82131f5e07a)

DFF with Asynchronous posedge reset : DFF output is irrespective of clock so Whenever the reset signal is high DFF output will become zero.

![image](https://github.com/user-attachments/assets/15fb720b-013c-49bc-83ec-42b1551aa720)

DFF with Asynchronous posedge set : DFF output is irrespective of clock. Whenever the set signal is high DFF output will become 1.

![image](https://github.com/user-attachments/assets/ca3ccbfb-18c9-4797-9dcb-b39f25238d60)

Posedge DFF with synchronous  posedge reset : DFF output Is with respect to positive clock edge. output will become zero only at the positive clock edge and when reset is high.

![image](https://github.com/user-attachments/assets/30bbce5e-8156-4262-b928-ce73561910da)

### Lab Flop Synthesis simulations 
The screenshots below shows the waveform of DFF with asynchronous reset display in gtkwave.

![image](https://github.com/user-attachments/assets/8de08a68-cf47-4478-b969-26e0a4b5b2ec)

![image](https://github.com/user-attachments/assets/6c55a197-1dbe-48b3-b1a7-40dd54543fab)

Synthesis of asynchronous reset flipflop

![image](https://github.com/user-attachments/assets/cae0c78e-2eaa-4baf-b303-662e420fca6a)

![image](https://github.com/user-attachments/assets/11cddd86-0345-4cd8-9a10-8aeb1af524ad)

![image](https://github.com/user-attachments/assets/01223aa8-5bc5-43c3-bfc5-f752ea0e28c2)

![image](https://github.com/user-attachments/assets/b127da54-f385-4ed3-9744-620ba156f7f0)

![image](https://github.com/user-attachments/assets/79973fb8-dcdb-41ea-821e-b1fc3b7e3889) 

synthesis of asynchronous set DFF :-

![image](https://github.com/user-attachments/assets/7f1252cb-004b-4213-8b94-472e17f764c8)

![image](https://github.com/user-attachments/assets/7e97666d-6f39-414a-9793-4015a15ac784)

![image](https://github.com/user-attachments/assets/53066fc9-72ba-4933-957c-d2942a9bde6c)

![image](https://github.com/user-attachments/assets/1d975b71-7273-42ae-afcb-0b9ae79880d2)

Synthesis of synchronous reset 

![image](https://github.com/user-attachments/assets/9201acfb-f96b-4b05-a112-a8704d876b26)

![image](https://github.com/user-attachments/assets/16c5e9cd-1db5-4bdd-b6ea-412989f6b4ef)

![image](https://github.com/user-attachments/assets/da4119b4-510f-4953-996e-91b513b66bde)

![image](https://github.com/user-attachments/assets/cf0a1fdb-fbd6-4d68-9824-7e5f254784de)

Screenshot below shows the logic of synchronous reset flipflop before synthesis and after synthesis. 

![image](https://github.com/user-attachments/assets/5e6c0746-bd79-4f66-8fe9-8be7c8de72a9)

Synthesis of Mul_2 :-
RTL code

![image](https://github.com/user-attachments/assets/63756a5b-25ba-4642-aafc-0ef078bb34e3)

The above RTL code accepts 3 bit input (a) and it is generating a 4 bit y. and y is equal to 2 * a.

![image](https://github.com/user-attachments/assets/b80bda3a-5f7f-4597-9593-1849d1732f96)

Truth table :-

![image](https://github.com/user-attachments/assets/4d2e7312-4ac8-42d9-a387-4884cf1be068)

From truth table you can observe that 1st 3 bits of output y is exactly same as 3 bit input a, only the last bit of output y is appended with zero. 
So the number multiplied with 2 (i.e a * 2)  = the number a appended with 1’b0

![image](https://github.com/user-attachments/assets/f953148e-372f-478c-8f4c-d378cda84da2)

![image](https://github.com/user-attachments/assets/759fd56b-59cf-43c7-8d28-670ad8797e5f)

Screenshot below shows output y = the number a appended with 1’b0

![image](https://github.com/user-attachments/assets/65333819-7c62-4381-88c6-f2421014519a)

![image](https://github.com/user-attachments/assets/6b46d856-6080-4f17-b333-0dd1e6e018f9)

![image](https://github.com/user-attachments/assets/a4e4ae62-8f35-4a99-a220-27f185ad816d)

In netlist also you can observe that y is a appended with 1 b’0.

Synthesis of mul_8

![image](https://github.com/user-attachments/assets/14bc85ce-41bf-4fd0-8bff-cd5b0caa5bb8)

![image](https://github.com/user-attachments/assets/378b251a-1493-4169-80f7-40e0bda59320)

Since the number of cells present for mapping are zero so need to perform abc mapping.

![image](https://github.com/user-attachments/assets/36528df1-f50a-4914-84d4-078c456190d9)

![image](https://github.com/user-attachments/assets/70caec2a-606e-47aa-ad15-26781a64f01d)


![image](https://github.com/user-attachments/assets/d3e12a94-1d3f-4f82-a3ee-80d0c2eb21dd)

![image](https://github.com/user-attachments/assets/342b29d2-9980-45f3-83c0-9e5f36c8291a)

# Day 3 : Combinational and Sequential optimization

### Introduction to Combinational Logic Optimization :-
It means Squeezing the logic to get the most optimised design in terms of Area and Power.
Techniques used to perform combinational logic optimization are :
- 1.	Constant Propagation : It is a Direct optimization technique.
- 2.	Boolean Logic Optimization : It is used to simplify big Boolean logic expression using techniques like K-map, Quine McKluskey

Example of Constant Logic Optimization : The propagation of a constant can generate a more optimize logic.
Previously, Y = ((AB) +C)’ -- 6 transistors required 
 but when A = 0, Y = C’ --- 2 transistors required.

![image](https://github.com/user-attachments/assets/c0ea2f53-2c6b-444d-8b04-6601db2e2a36)

Boolean Logic Optimization 

![image](https://github.com/user-attachments/assets/3ee3a78f-e0a9-4bb4-843d-01bd9f7ff12b)

Sequential Logic Optimization 
Techniques of Sequential Logic Optimization are :-
- 1.	Basic
    - Sequential Constant Propagation


- 2.	Advanced [Not Covered as part of Lab]
    - State Optimisation
    - Retiming
    - Sequential Logic Cloning (Floorplan Aware Synthesis)

Example of Sequential constant Propagation :-
When RST is enable Q = 0 ,
When RST is disable Q = 0 since input D = 0.
So output Q is always 0 irrespective of RST signal.
And When constant sequential constant is propagated to NAND gate,output of NAND gate (Y) will always be 1.
Example 1 :-

![image](https://github.com/user-attachments/assets/88b54a8f-5034-46d0-acfa-a444d7fa4025)

Example 2 :- When Set is enable 1, Q=1 and When Set is disable so with respect to clock Q = 0. Q pin is not taking constant value. It can take value either 0 or 1 Because of this sequential constant is not propagated at the output of flipflop. This flop cannot be optimized so this needs to be retain the circuit.

![image](https://github.com/user-attachments/assets/ba37d6c6-19dc-4586-8b50-bbcb656a0719)

![image](https://github.com/user-attachments/assets/37ef3787-481f-45ad-b86e-d7cbc86fc172)

Lab on Combinational Logic Optimization 
Code used for optimizing is :-

![image](https://github.com/user-attachments/assets/05e2e8cd-60ef-4a5a-b209-d3a7aa29698e)

![image](https://github.com/user-attachments/assets/ec1a690b-b881-4f14-bb3f-0f8533ddfef5)

Command to do Constant Propagation and all the optimization is :- opt_clean -purge

![image](https://github.com/user-attachments/assets/23b88131-8aee-4185-9a84-9a35408f0415)

![image](https://github.com/user-attachments/assets/201ded30-1bf9-4430-8238-652399a50385)

![image](https://github.com/user-attachments/assets/f329135d-9da7-4392-90c4-75f6714964fd)

![image](https://github.com/user-attachments/assets/c272540c-3f5b-4810-8b2f-0b5b97cace62)

Previously Y = a ? b : 0
After synthesis , Y = a.b 
In the above screenshots you can see the AND gate. 

![image](https://github.com/user-attachments/assets/0ed8d581-d185-4a53-bb4d-adc3092ba0dd)

Synthesis of Opt_check2
RTL code:-

![image](https://github.com/user-attachments/assets/70731952-4b14-45b8-9474-c0947275012b)

![image](https://github.com/user-attachments/assets/82379e36-33f9-4c54-87a9-b410f2c492c3)

![image](https://github.com/user-attachments/assets/d881728b-bc5c-4104-bda7-6b519cfb0356)

![image](https://github.com/user-attachments/assets/c70aa3da-a399-459a-8d93-45939b664f6b)

![image](https://github.com/user-attachments/assets/47a72393-99fa-455a-9a53-3733c35c9032)

Synthesis of Opt_check3

![image](https://github.com/user-attachments/assets/6f6b3b2a-7e98-4b59-9657-6a2caa17ac14)

![image](https://github.com/user-attachments/assets/ed0d320a-743c-4b3a-987f-eef8ef37276d)

![image](https://github.com/user-attachments/assets/870192b0-29c2-40d2-9813-573431807107)

![image](https://github.com/user-attachments/assets/fcf8a241-2d04-4ac0-b7ec-b4ac37f16103)

![image](https://github.com/user-attachments/assets/063dd17f-3a2d-44dc-8294-7b2ebef646b1)

In the above screenshot you can see the 3 input AND gate.

Synthesis of opt_check4 

![image](https://github.com/user-attachments/assets/d0833826-be2c-42d0-aa0b-acdae57f808d)

![image](https://github.com/user-attachments/assets/746a4d89-1ff8-43bf-816d-6ffa4c413d5b)

![image](https://github.com/user-attachments/assets/9c6117fd-6848-4b01-ab90-cd510f29c56b)

![image](https://github.com/user-attachments/assets/df03b7a9-77f7-4391-8649-0848858708c1)


Lab on Sequential Logic Optimization 
Optimizing dff_Const1.v
RTL code of dff_const1.v:-

![image](https://github.com/user-attachments/assets/a1b567ae-2578-4317-97d3-351e64c13b79)

![image](https://github.com/user-attachments/assets/d0435312-8014-4bc2-821f-fb8c8c177cb4)

When RST = 1, Q = 0 else Q = 1
Waveform :-

![image](https://github.com/user-attachments/assets/f5f49072-3ff9-467d-807e-2545b96eedf3)

From above screenshot you can see that when RST is 1,   Q= 0 and when RST = 0, Q will not immediately become 1 it will wait for next possitive edge to become 1.

![image](https://github.com/user-attachments/assets/34b539e8-d26c-4ad0-b071-8f54d6d33174)

![image](https://github.com/user-attachments/assets/ea1f6d61-c57e-441b-b438-a376205007b9)

![image](https://github.com/user-attachments/assets/a1454ade-d360-499d-acbd-9a846fc9f5d2)

Optimizing dff_const2.v
RTL code of dff_const2.v:-

![image](https://github.com/user-attachments/assets/8ed8eb5b-dfca-4ea9-aaa4-4b29f5dc0edd)

![image](https://github.com/user-attachments/assets/98aabc48-fc25-4a96-abc1-3869644fde0c)

Here RST pin is acts like a SET. When RESET = 1,Q=1 and at the edge of the RST it will become 1 and at the next edge again it becomes 1.

![image](https://github.com/user-attachments/assets/0b213fb5-38ff-4677-b40c-30be872266cb)

![image](https://github.com/user-attachments/assets/36245e92-1c79-4868-b9d5-0981b9603cbe)

Synthesis of dff_const1.v

![image](https://github.com/user-attachments/assets/e955fd25-fcc0-4919-8bef-e1ce679adec0)

After that use command dfflibmap -liberty lib_path.
Since design has flipflop so we have to tell the tool that use this lib for flipflop mapping. 

![image](https://github.com/user-attachments/assets/0563a7bd-af87-426c-a3dc-195514d893da)

![image](https://github.com/user-attachments/assets/985f923d-5b4a-4567-8f4c-9fdb69e491c8)

![image](https://github.com/user-attachments/assets/78eac9fd-51a4-4151-bf38-34e39dc95de8)

![image](https://github.com/user-attachments/assets/7dc9b74c-1fae-4451-bc4b-337989d5593c)

From above screenshot you can observe that, in design we make RST as active high but in lib by default RST is active low so thats why tool have given RST signal to RST pin of flipflop through inverter.

Synthesis of dff_const2.v

![image](https://github.com/user-attachments/assets/b0ce2548-a532-4739-9405-18ae93f98226)

![image](https://github.com/user-attachments/assets/ffa7c261-17d3-4a50-8630-c3cb31eb47ba)

In the above screenshot you can see that tool has shown 0 cells.

![image](https://github.com/user-attachments/assets/a93f7e7f-ebb6-43bc-bfce-dfa91ca3d158)

![image](https://github.com/user-attachments/assets/bba4ce99-b43a-4237-81f7-d5dff3c3acc6)

In above screenshot you can see that irrespective of RST,CLk  Q is always 1 hence there is no need of flipflop.hence after synthesis, tools has not shown flipflop.

Optimizing dff_const3.v
RTL code of dff_const3.v:-

![image](https://github.com/user-attachments/assets/b9ebc763-7602-470f-b015-630f7f589696)

![image](https://github.com/user-attachments/assets/95dc6399-80b8-4b0c-b836-0f0b635fa5d8)

Here when RST 1, Q1 = 0 and when RST = 0 at this edge Q1 will remain 0 till the next clock edge and at the next clock Q1 becomes  1.
When SET = 1, Q = 1 and when SET = 0 at this clock edge Q becomes 1 till it gets next clock edge and the next clock it becomes 0 and again after once cycle Q becomes 1. So Q will always become 1 except one clock edge.

![image](https://github.com/user-attachments/assets/6fc8e94f-34c9-4474-b33a-1301c05a9576)

![image](https://github.com/user-attachments/assets/3ab0ff54-321b-4980-8daa-03144b268dab)

Synthesis of dff_const3.v
![image](https://github.com/user-attachments/assets/154dd972-fac1-45f4-8958-05cd9e956f70)

![image](https://github.com/user-attachments/assets/3e80f113-cd12-4799-87bc-d262f0754c06)

In the above scrrenshot you can see that in the statistics table,it is showing 2 flipflops.
![image](https://github.com/user-attachments/assets/2dd24729-155b-450b-844c-a74e950ce758)

![image](https://github.com/user-attachments/assets/8c3411c7-ce08-498d-b93c-cd128848052e)

![image](https://github.com/user-attachments/assets/8d5f611b-8ab3-499e-a02f-8d3a9db84156)

![image](https://github.com/user-attachments/assets/1851ece3-921b-45dd-8dac-1b548bddbb9a)

In the above scrrenshot you can see that both RESET and RST input is given through inverter and Flipflops ares also properly mapped.


Sequential Optimization for unused optimization 
Optimizing counter_opt.v :- 3 bit up counter

![image](https://github.com/user-attachments/assets/2316c7d6-47c6-4b82-b953-b1a4781fb3db)

![image](https://github.com/user-attachments/assets/3669bbc5-8864-4200-8323-6073b3047f21)

Here the final output Q is sensing only count[0]. So remaining count[1] and count[2] are unused as this is the logic in design.
when the logic which is not affecting output,need not to be present in the design.
In the truth table also you can observe that only bits present at 0th location are used as for every bit it is toggling,remaining are not used.
Here, Case 1 is : only at 0th possition bits are used.
Case 2 is : All 3 bits are used.

Case 1 :-
RTL code :- 

![image](https://github.com/user-attachments/assets/1dea3231-3fac-408f-b7b3-500aab461c9b)

![image](https://github.com/user-attachments/assets/9dc34c15-a9da-4edd-8377-67cb380e2da9)

![image](https://github.com/user-attachments/assets/a0b4d95c-dea1-4669-ab2d-a9d8ed87b4e3)

In the above screenshot you can observe that for 3 bit counter tool should have shown 3 flipflops but it has used only 1 flipflop.why?
![image](https://github.com/user-attachments/assets/123c99f5-b194-41bb-9b70-076f7c306052)

![image](https://github.com/user-attachments/assets/792bcb58-b930-4d86-8596-87a01686eeb2)

![image](https://github.com/user-attachments/assets/9f5ea5b1-ce52-4a73-b5ed-fa140223a7bd)

![image](https://github.com/user-attachments/assets/729b7bb6-7021-48e7-a80e-588ff41b1aa8)

Here in the above screenshot you can see that output q is only sensing count[0] bit. Hence only for that 1 flipflop is used and the output of q is given to the input pin D through inverter.
Since count[1] , count[2] bits are unused hence it is removed durring optimization.That is why only one flipflop is used in the design.


Case 2 : All 3 bits are used hence expecting 3 flipflops in the design
RTL code :-

![image](https://github.com/user-attachments/assets/64bcd135-ad52-4a18-84ca-74ce1bffa99f)

Synthesis :-

![image](https://github.com/user-attachments/assets/6fb3163c-bbaf-4b94-9995-e167869b1224)

![image](https://github.com/user-attachments/assets/2e70bb67-0824-42f8-b8f0-1253281d3185)

Here as expected it is showing 3 flipflops.
![image](https://github.com/user-attachments/assets/95717e1e-5308-4ee1-b430-3f5b2892e4a7)

![image](https://github.com/user-attachments/assets/d71a5d78-00ef-43b2-8e4a-6b8bee6ba693)

![image](https://github.com/user-attachments/assets/17d980d4-f1ac-4878-b32b-5b245bdebfc2)

Q = count[2] .count[1] bar. Count[0] bar 
![image](https://github.com/user-attachments/assets/ecf44955-8e55-4798-b06d-254c96031046)

![image](https://github.com/user-attachments/assets/a6e86294-9d10-499e-9ede-2c81e8003c15)

# Day 4 : GLS, blocking vs Non-blocking and synthesis simulation mismatch
Introduction to Gate level simulation (GLS) and synthesis simulation mismatches
What is GLS ?
-	Running the testbench with netlist as Design Under Test
-	Netlist is logically same as RTL code.same testbench will align with the design.
Why GLS?
-	Verify the logical correctness of design after synthesis.
-	Ensuring the timing of the design is met.For this GLS needs to be run with delay annotation. 

GLS using iverilog 
![image](https://github.com/user-attachments/assets/6ceecf9b-ccc3-4b42-9677-c57a29dd9937)

Here design is netlist.
![image](https://github.com/user-attachments/assets/7b92e03c-5acd-4a8e-a277-e9fdf73ce99d)

Synthesis Simulation Mismatch
It can happen due following reasons :-
-	Missing sensitivity list
-	Blocking vs Non-Blocking assignments
-	Non standard verilog coding

![image](https://github.com/user-attachments/assets/158d15cf-fad6-40ca-b1fe-66f8be54a240)

Simulator works in such a way that it checks for the change in signal activity. When input changes ,output changes. 
Above screenshot shows the RTL code of 2:1 mux. In the left side RTL code, output y changes only when there is change in sel line.It will not check for change in i0 and i1.since sel line is given as sensitivity list in the always block. So this code ascts as a latch. In the right side RTL code, * is given as sensitivity list. Hence y changes when any of the input changes.

Blocking and Non- blocking statements in verilog :-
Inside always block :-
Blocking statements are represented using “=” sign.
-	It executes the statements in the order it is written.
-	So the first statemnt is evaluated before the second statement.

Non – Blocking statemnts are represented using “<=” sign.
-	It executes all the RHS when always block is entered and assigns to LHS.
-	It performs parallel evaluation.

![image](https://github.com/user-attachments/assets/6cc0189d-4722-4997-965d-77b93bd7a932)

![image](https://github.com/user-attachments/assets/027875a2-f8d8-4401-86e1-e59ae457e031)

Lab on GLS synth simulation mismatch 
Input of GLS : Design (netlist), gate level verilog model,testbench.
Output : vcd file
Simulation of ternary_operator_mux.v 
RTL code :-

![image](https://github.com/user-attachments/assets/5676e447-4bef-4be1-ba82-ef0a65c9692a)

![image](https://github.com/user-attachments/assets/e041ee35-b81b-44d9-83e5-8776bd078e86)

![image](https://github.com/user-attachments/assets/254fc23b-6db2-4922-aeb5-54a619628aa9)

In the above screenshot you can see that when sel = 0, y = i0 and when sel =1, y = i1.

Synthesis of ternary_operator_mux.v

![image](https://github.com/user-attachments/assets/a6d7490e-f302-40c5-9f34-95a13501afaf)

![image](https://github.com/user-attachments/assets/eba8991f-1926-44c4-9ec3-f8d5fa7d05ab)

![image](https://github.com/user-attachments/assets/2fd1a64e-597d-4495-bb28-4fa11f749fab)

![image](https://github.com/user-attachments/assets/e15853da-246b-495a-995e-446cb1ec18ee)

![image](https://github.com/user-attachments/assets/c0bbc69e-6cf0-4c75-85a9-713aa3ee3bf3)

![image](https://github.com/user-attachments/assets/6aa8288e-ae32-4cc3-a38b-3703821f6793)

Invoking GLS :-
![image](https://github.com/user-attachments/assets/372490fb-9497-448d-aa5a-8c9ba5f26a05)

![image](https://github.com/user-attachments/assets/754a6d82-7b5a-4d28-99e7-f44094bdb117)

Simulation of bad_mux.v
RTL code :-

![image](https://github.com/user-attachments/assets/09c86afc-3c26-4f70-bfb4-f10ec58f6f4e)

![image](https://github.com/user-attachments/assets/fc89daa2-d875-42c5-907d-e690232f9b5b)

![image](https://github.com/user-attachments/assets/933bf993-f4ae-4a68-bd15-489b9089c2fa)

In the above screenshot you can see that,always block executed only at sel signal because of that it works like a flop rather than mux.
Synthesis of bad_mux.v

![image](https://github.com/user-attachments/assets/26710820-64e4-4c5b-a025-3497598ad882)

![image](https://github.com/user-attachments/assets/84b0fc7f-002a-4ae7-88e9-629fcccc3cef)

![image](https://github.com/user-attachments/assets/7ed3827d-30c8-4eef-9839-c0780fff9a07)

![image](https://github.com/user-attachments/assets/e153c316-3a33-4aaf-b616-9ffb6ec52b97)

Invioking GLS :-
![image](https://github.com/user-attachments/assets/254fa6cc-2170-43c4-9cf2-296a4cadc5e2)

GLS output :-
![image](https://github.com/user-attachments/assets/86dc47a0-3d2b-45a2-8df7-0211e537206a)

By comparing RTL simulation and GLS output, you can observe that in GLS output when sel is low, the activity of i0 is reflecting on y whereas in RTL simulation when sel is low,the activity of i0 is not reflecting on y. Also in GLS simulation when sel is 1, i1 is reflecting on y whereas in RTL simulation it is not reflecting. This is called synthesis simulation mismatch due to missing sensitivity list.
Labs on Synthesis simulation mismatch for blocking statement
Simulation of Blocking_caveat.v
RTL code:-

![image](https://github.com/user-attachments/assets/55c69983-e892-46d9-9c3c-35f341dc6735)

![image](https://github.com/user-attachments/assets/be9bd0d9-f494-43db-97ce-eaf1ce388442)

Simulation using iverilog :-
![image](https://github.com/user-attachments/assets/469acbbc-e1e5-4b33-aa49-8d64cf7dc590)

![image](https://github.com/user-attachments/assets/6c0937c7-017a-4fc5-91a5-cf3295b787fc)

In the above screenshot you can observe that because of blocking statement, value of x is updated after evaluating d expression hence at the output expression d evaluated using old value of x.hence not getting expected output.

Synthesis :-

![image](https://github.com/user-attachments/assets/f8ed9ba8-a802-4e44-9e11-61c4d5b21718)

![image](https://github.com/user-attachments/assets/4e0927e3-3106-4220-9caa-00182d21b774)

![image](https://github.com/user-attachments/assets/7e49ddcc-a33a-4dd1-9a86-e6ea14709298)

![image](https://github.com/user-attachments/assets/72688ba4-fd88-4e95-804b-8b4567b0c048)

![image](https://github.com/user-attachments/assets/efcb365c-a448-46e5-8c56-ca85b46d9f2a)

![image](https://github.com/user-attachments/assets/c8001d10-0c7a-4ebd-b433-1851825a7590)

Invoking GLS :-

![image](https://github.com/user-attachments/assets/79917dfd-6688-4d2d-9af2-658cc4d1254a)

GLS output :-

![image](https://github.com/user-attachments/assets/aab33ba7-0b93-4be5-bdcc-8940e42a0ad1)

In the above screenshot also you can see that there is a synthesis simulation mismatch caused due to blocking statements.so use blocking statements in verilog only when it is needed otherwise can get unpredictable results. 

