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
  2)  Similarly power dissipation also increases as wider transistors have wider channels and larger gate surface areas, which increases both parasitic capacitance and subthreshold leakage paths.Dynamic power also increases because the internal capacitance of the larger cell takes more energy to switch.  
  3)  Delay decreases

<img width="1787" height="661" alt="Screenshot 2026-05-20 105501" src="https://github.com/user-attachments/assets/3784b678-99d8-42eb-b197-13cd02e4ce19" />
