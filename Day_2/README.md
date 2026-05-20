# Day-2:Timing libs, hierarchical vs flat synthesis and efficient flop coding styles

## Introduction to timing .lib

### Introduction to dot Lib part1


* Lets see what `.lib` contain
* Enter command:

<img width="1857" height="51" alt="Screenshot 2026-05-20 083620" src="https://github.com/user-attachments/assets/35b91653-5ebc-449b-b495-049759b6351a" />

* It opens like this then to have pleasant colour, enter command shown at bottom of image:

<img width="1273" height="716" alt="Screenshot 2026-05-20 083855" src="https://github.com/user-attachments/assets/477f8df0-6870-4c05-807e-977cb48bace4" />

* It tells us about:  
  Technology used  
  Units of voltage, power, time,etc  
  Operating conditions:    
  >Process, voltage and temperature
  
<img width="1267" height="710" alt="Screenshot 2026-05-20 083917" src="https://github.com/user-attachments/assets/de9512b0-3e6f-4df5-9442-29a13c75074d" />

* First line tells about library:  
  `sky130:` It is a 130nm library  
  `tt:`     Typical  
  `025C:`   Temperature  
  `1v80:`   Voltage

 ### Introduction to dot Lib part2

* It tells us about different features of the cell like leakgae power for different combinations of input
  and we can also view equivalent verilog model to understand functionality of cell (above part in below image). 

 <img width="1840" height="858" alt="Screenshot 2026-05-20 103547" src="https://github.com/user-attachments/assets/ab6ce4cc-a0c0-4c57-9fb0-e68f370b6981" />


* It gives information about each pin like power, delay and transition related to pin

<img width="1047" height="342" alt="Screenshot 2026-05-20 104454" src="https://github.com/user-attachments/assets/8a6b7579-2060-4d2d-acc3-e7931b9d6035" />


### Introduction to dot Lib part3

* Lets see `AND` gate

<img width="757" height="455" alt="Screenshot 2026-05-20 105328" src="https://github.com/user-attachments/assets/890e9388-6bfa-4c27-b850-b48c8897464f" />

* Comparing different `and` cells with differet driving stregths  
  1)  You can observe that area increases from `_0` to `_4` as wider transistors used to drive more current  
  2)  Similarly power dissipation also increases as wider transistors have wider channels and larger gate surface areas, which increases both parasitic capacitance and 
      subthreshold leakage paths.Dynamic power also increases because the internal capacitance of the larger cell takes more energy to switch.  
  3)  Delay decreases

<img width="1787" height="661" alt="Screenshot 2026-05-20 105501" src="https://github.com/user-attachments/assets/3784b678-99d8-42eb-b197-13cd02e4ce19" />

## Hierarchical vs Flat Synthesis

### Hier synthesis flat synthesis part1

* Open `multiple modules.v`

  <img width="1408" height="61" alt="Screenshot 2026-05-20 120059" src="https://github.com/user-attachments/assets/145fe8bc-543a-43f8-9ead-6b984c9e897a" />

  <img width="1657" height="462" alt="Screenshot 2026-05-20 120315" src="https://github.com/user-attachments/assets/2b903dc5-d993-4de0-9a9e-65144037a866" />

  * As per above code, we expect synthesis output like below:

    <img width="840" height="510" alt="Screenshot 2026-05-20 120526" src="https://github.com/user-attachments/assets/fdb96754-b984-433f-a8ad-934ef7b946c7" />


  * We expect `or`, `and` gate but it is showing `u1` and `u2` as they are instances of `submodule1` and `submodule2`. This is called **Hierarchical Design** as we see hierachies

    <img width="511" height="536" alt="Screenshot 2026-05-20 121203" src="https://github.com/user-attachments/assets/12c03e0e-dce3-4ede-a4bf-fe542d8fb4bc" />

* Now write nelist

  <img width="1637" height="350" alt="Screenshot 2026-05-20 121541" src="https://github.com/user-attachments/assets/085ebf4f-2e4a-4f57-af99-2e5e6dfa2323" />


* We can see that hierarchies are preserved

  <img width="1651" height="806" alt="Screenshot 2026-05-20 121831" src="https://github.com/user-attachments/assets/828e1162-2907-470b-9011-bc10fbdd530a" />

  <img width="1451" height="702" alt="Screenshot 2026-05-20 121953" src="https://github.com/user-attachments/assets/426707d4-ab8a-492b-a5b0-3418182227a1" />

* We can observe synthesis tool give `nand` instead of `or`

  <img width="757" height="436" alt="Screenshot 2026-05-20 122254" src="https://github.com/user-attachments/assets/a5db146d-ae4d-4e02-bdea-8a32beadb79f" />

* It is given like that as stacked pmos is not preferred as it has poor mobility and to improve it, 
  width of transistor should be increased which  requires more area(so logic 1 given by synthesis tool instead of logic2)

  <img width="887" height="498" alt="Screenshot 2026-05-20 122513" src="https://github.com/user-attachments/assets/3ce6d8c3-00e9-4667-aeba-76ee9ce7807d" />

### Hier synthesis flat synthesis part2

* Now, to write `Flat` netlist we use command `flatten` and write nelist

  <img width="633" height="513" alt="Screenshot 2026-05-20 123417" src="https://github.com/user-attachments/assets/80e2a7ed-aa06-4ac2-a74e-0ffe56ab0a81" />

* We can observe that hierachies are flattened out and there is direct instantiation of `and`, `or` gate under module `multiple module`(see right side image, i.e.. flattened netlist code)

  <img width="1662" height="837" alt="Screenshot 2026-05-20 163625" src="https://github.com/user-attachments/assets/9c794104-aa64-464a-877a-d7c09ec8493e" />

* Flattened Netlist

  <img width="1840" height="372" alt="Screenshot 2026-05-20 174615" src="https://github.com/user-attachments/assets/a7ca8f73-956c-40a5-83fb-a7316a225ce5" />


* Now let's do submodule level synthesis. So lets do `submodule1` synthesis from `multiple module`
*  We cotrol with command
  ```
  synth -top module/submodule
  ```
  
  
<img width="1531" height="300" alt="Screenshot 2026-05-20 175753" src="https://github.com/user-attachments/assets/5873e48a-ebd6-4d66-8767-7dc4a87afcaa" />

  
  <img width="1700" height="318" alt="Screenshot 2026-05-20 180022" src="https://github.com/user-attachments/assets/62bb0bed-d922-4bf0-9d20-d8830bbea2c4" />


**Why we do module level synthesis?**
* When module is instantiated multiple times then synthesize module once and replicate it to form top module
* To synthesize by divide and conquer method in case of massive designs like giving portion by portion to tool to get optimised design then stitich all to get massive top netlist

 <img width="881" height="495" alt="Screenshot 2026-05-20 181309" src="https://github.com/user-attachments/assets/5acb8956-9f9d-445b-a0f9-3931fa6fae01" />
 

## Various Flop Coding Styles and optimization

### Why Flops and Flop coding styles part1

*  More the combinational circuits  more will be glitches in output, implies output will never settle down

*  So, we want a element to store a value i.e., Flop. Ex:D-Flip Flop

*  By using them in middle of chain of combination circuits, glitches avoided to propogate as they give output  based on clock edges. So, even input has multiple glitches (from combination circuit) output will be stable (from Flop) which can also help in providing stable input to next combination circuit in design, reducing in propogation of glitch

  
<img width="947" height="798" alt="Screenshot 2026-05-20 182200" src="https://github.com/user-attachments/assets/9475e652-3726-4f2f-82a2-0d5c289a1813" />

**Note:**
Initialise Flop state as combination circuit taking input from Flop may evaluate garbage value and produce output, so to initialise clock , there is control pins:
* SET, RESET
* Can be synchronous or asynchronous


### Why Flops and Flop coding styles part2


* Different types of D-flops and their design

  <img width="870" height="213" alt="Screenshot 2026-05-20 210404" src="https://github.com/user-attachments/assets/4c53c5d8-4491-4ef5-8f41-40e190e88b41" />

  <img width="941" height="607" alt="Screenshot 2026-05-20 210435" src="https://github.com/user-attachments/assets/e87b4ab7-ccc8-4dfe-aac6-569d7f309ec9" />

  <img width="1333" height="722" alt="Screenshot 2026-05-20 210121" src="https://github.com/user-attachments/assets/abf47b3b-cd94-41d7-882e-45cbc0d8a2bf" />


