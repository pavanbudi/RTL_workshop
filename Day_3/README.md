# Day 3 - Combinational and sequential optmizations

## Introduction to optimizations

### Introduction to optimisations part1

<img width="1282" height="717" alt="Screenshot 2026-05-21 005049" src="https://github.com/user-attachments/assets/e7b62705-17fb-4c77-8e84-b49e11326eba" />

<img width="1776" height="921" alt="Screenshot 2026-05-21 005436" src="https://github.com/user-attachments/assets/cea71175-f8d7-4b0e-adfd-fa6370958c83" />

<img width="1631" height="845" alt="Screenshot 2026-05-21 005522" src="https://github.com/user-attachments/assets/2c6153bf-107b-4502-a3fa-5b4da6c389ef" />


### Introduction to optimisations part2

<img width="568" height="382" alt="Screenshot 2026-05-21 011626" src="https://github.com/user-attachments/assets/0cc2bb27-14d3-4d83-99ca-2a62529e5647" />


* `Y` is always `1` irrespective of input `A` due to sequential constant propogation, so no hardware is required

 
 <img width="792" height="312" alt="Screenshot 2026-05-21 011933" src="https://github.com/user-attachments/assets/68099eeb-bcd0-4c51-a2d7-a374af7a1db1" />


* Can we say `Q = Set`
* No as `Q` follows `Set` only when `Set=1`
* When `Set` removed(set=0) then `Q` wait until ext clock edge and follows `D` implies no dependency on `Set`
* So flop canot be optimised, whole logic need to be retained
* For flop to be sequential constant `Q` should be always constant
* So every Flop with `D` input tied up is not constant propogation


  <img width="1461" height="492" alt="Screenshot 2026-05-21 010540" src="https://github.com/user-attachments/assets/0423de2d-6241-4506-b1b7-0a07a283f097" />


### Introduction to optimisations part3

<img width="1805" height="987" alt="Screenshot 2026-05-21 012931" src="https://github.com/user-attachments/assets/d0d95568-8b2d-4260-8d14-b3990ec05df3" />

## Combinational logic optimizations

### Combinational Logic Optimisations part1

* Consider files

  <img width="602" height="602" alt="Screenshot 2026-05-21 013405" src="https://github.com/user-attachments/assets/18955351-2fc9-4914-b757-29130ed361ea" />

<img width="390" height="227" alt="Screenshot 2026-05-21 013508" src="https://github.com/user-attachments/assets/f4141974-c2fd-445a-92fb-677a2673c879" />

* Now synthesize

  <img width="1337" height="673" alt="image" src="https://github.com/user-attachments/assets/174d8d37-e4de-404e-803b-d468bd895679" />

* Command to do constant propogation and all optimisations:

  <img width="396" height="60" alt="Screenshot 2026-05-21 013711" src="https://github.com/user-attachments/assets/6e618615-2860-4bb1-bb4b-029bb9b5fb5c" />


* Netlists

  <img width="696" height="122" alt="Screenshot 2026-05-21 014216" src="https://github.com/user-attachments/assets/5cd216d7-fad4-43b7-83be-906c7462a14b" />


<img width="1608" height="112" alt="Screenshot 2026-05-21 014235" src="https://github.com/user-attachments/assets/d2581a2b-27a7-4a6a-933d-cb12bdb44917" />


  <img width="251" height="265" alt="Screenshot 2026-05-21 013830" src="https://github.com/user-attachments/assets/bb0185fd-421f-4139-8cdd-46f050e8f5b5" />
  
**Note:** We have studied that stacked pmos is not preferred

  <img width="532" height="557" alt="Screenshot 2026-05-21 013907" src="https://github.com/user-attachments/assets/5188817f-65a1-4d23-87bf-59a10c2c061e" />


### Combinational Logic Optimisations part2

<img width="648" height="537" alt="Screenshot 2026-05-21 014407" src="https://github.com/user-attachments/assets/b4b9da1f-b49d-41fd-beef-03d55b3ac7c1" />

<img width="821" height="407" alt="Screenshot 2026-05-21 014420" src="https://github.com/user-attachments/assets/06e7843d-036e-4c7d-a830-975563ff22ba" />

<img width="508" height="540" alt="Screenshot 2026-05-21 014439" src="https://github.com/user-attachments/assets/76bf0efe-75f4-4be0-ba27-43f8fbceab70" />

* Work on opt_chect-4&5

* In case of multiple modules, flatten it first then optimise it and write out netlist

  <img width="1055" height="63" alt="Screenshot 2026-05-21 014642" src="https://github.com/user-attachments/assets/856ee431-3f15-42fe-b129-64f82ddeecfb" />




