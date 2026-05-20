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


  <img width="1461" height="492" alt="Screenshot 2026-05-21 010540" src="https://github.com/user-attachments/assets/0423de2d-6241-4506-b1b7-0a07a283f097" />


