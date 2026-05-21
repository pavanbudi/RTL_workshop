# Day4 - GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

## GLS, Synthesis-Simulation mismatch and Blocking/Non-blocking statements

### GLSConceptsAndFlowUsingIverilog

<img width="1636" height="892" alt="Screenshot 2026-05-21 134734" src="https://github.com/user-attachments/assets/b10b7b06-78f2-447e-ae03-c3268b690a37" />


* Here design is `Nelist` which is in form of `std. cell`
  What does `std.cell` mean, we need to tell this to `iverilog` tool. For this purpose we have to read `Gate Level Verilog Models` and give that information to tool to read

  
<img width="1895" height="967" alt="Screenshot 2026-05-21 134932" src="https://github.com/user-attachments/assets/35d4c37a-df5e-493b-9346-bb7c908622b1" />


* Gate Level Verilog Models are two types:
   1) Timing aware: we can validate functional and timing of desigm
   2) Functional aware: Only functionality can be validated


  <img width="1693" height="900" alt="Screenshot 2026-05-21 140931" src="https://github.com/user-attachments/assets/58ddde38-b049-493f-9ad7-e4f1bff6d5fb" />


### Synthesis Simulation Mismatch

<img width="557" height="225" alt="Screenshot 2026-05-21 142336" src="https://github.com/user-attachments/assets/b9ce1e42-9cf7-4604-8043-ae5fa4499a7e" />

* For code on left, synthesizer may give latch or double edge flop due to wrong sensitivity list

  <img width="868" height="500" alt="Screenshot 2026-05-21 142306" src="https://github.com/user-attachments/assets/6c29a25b-f552-4d4a-a2aa-1555ebe2b820" />


### BlockingAndNonBlockingStatementsInVerilog

<img width="1415" height="907" alt="Screenshot 2026-05-21 142947" src="https://github.com/user-attachments/assets/5b6a05e2-54bc-497a-8746-a7c2138ac5fe" />

* As order is followed in `blocking assignment` , so change of order of `Blocking Assignment` like in right side design in image then it may lead to simulatio mismatch

*  
<img width="1487" height="932" alt="Screenshot 2026-05-21 143022" src="https://github.com/user-attachments/assets/8125c005-23cf-4f85-9246-456b0b1c2e1b" />
