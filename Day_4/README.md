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


### Blocking And NonBlocking Statements In Verilog

<img width="1415" height="907" alt="Screenshot 2026-05-21 142947" src="https://github.com/user-attachments/assets/5b6a05e2-54bc-497a-8746-a7c2138ac5fe" />

* As order is followed in `blocking assignment` , so change of order of `Blocking Assignment` like in right side design in image then it may lead to simulatio mismatch

 
<img width="1487" height="932" alt="Screenshot 2026-05-21 143022" src="https://github.com/user-attachments/assets/8125c005-23cf-4f85-9246-456b0b1c2e1b" />


### Caveats With Blocking Statements

* To avoid mismatches due to `Blocking Assignments`, use `Non-Blocking assignments` where order was not problem

* Code mimics a `delay/Flop` but after synthesize we won't see any `Flop`. So which leads to `synthesis Mismatch`
  

  <img width="572" height="405" alt="Screenshot 2026-05-21 144137" src="https://github.com/user-attachments/assets/6b450dad-1a40-4fa4-b122-84696f1283aa" />


  * We can see that both of them give same design after synthesis but if we simulate design, we get wrong output
    So it is important to run `Gate level Simulation (GLS)` on netlist and match it with expected result


  ## Labs on GLS and Synthesis-Simulation Mismatch

  ### Lab GLS Synth Sim Mismatch part1

  * To run GLS we need:
    1) Netlist
    2) Verilog models of std. cell library
    3) Testbench

  * Files we use for this lab
 
    <img width="1546" height="60" alt="Screenshot 2026-05-21 153545" src="https://github.com/user-attachments/assets/9c5250b9-2a46-4a12-a2c5-a5012d2516e9" />

    <img width="892" height="770" alt="Screenshot 2026-05-21 153631" src="https://github.com/user-attachments/assets/6308d80b-f9fc-4b67-a83e-8124ed4a2764" />


* Lets do RTL simulation

  <img width="1338" height="227" alt="Screenshot 2026-05-21 153847" src="https://github.com/user-attachments/assets/5600f031-fc56-42d4-bb6b-d71cc9ad15b4" />


<img width="472" height="300" alt="Screenshot 2026-05-21 153940" src="https://github.com/user-attachments/assets/f3d452c9-c386-4ac3-9e66-76590805a7b7" />


* Synthesize

  <img width="862" height="207" alt="Screenshot 2026-05-21 154136" src="https://github.com/user-attachments/assets/45f222ed-f7d0-4e0d-bfaf-b7a6cf6e1113" />

* Lets do `GLS`
  >Invoke `iverilog` with
  1) Verilog Models of std. cells
  2) Std. cell library
  3) Netlist


    <img width="1852" height="96" alt="Screenshot 2026-05-21 154616" src="https://github.com/user-attachments/assets/bfcccc46-4abe-45f6-84aa-19922e2b59d0" />

  * `GLS` output
    We can verify desig now

    <img width="862" height="382" alt="Screenshot 2026-05-21 154839" src="https://github.com/user-attachments/assets/c5d62c6f-9ffa-4a1d-9eaa-3924ebe4d1c6" />


### Lab GLS Synth Sim Mismatch part2

* Similarly lets check `bad_mux.v` which has `sensitivity list mismatch`

<img width="847" height="655" alt="Screenshot 2026-05-21 155720" src="https://github.com/user-attachments/assets/130d9b9b-c8ef-44cd-b138-389bc4b6272d" />


* RTL simulated output
* Activity on `i0`,`i1` are not selected by `always` block. Clearly we can say it is not working like `MUX` as change in `i0`,`i1` are not reflected  when `sel` is `0`,`1` respectively
* Simulation is showing like a `Flop` kind of behaviour

  <img width="862" height="382" alt="Screenshot 2026-05-21 154839" src="https://github.com/user-attachments/assets/4b5bf5b7-d8ba-4182-a5db-0808c630ade3" />


 * `GLS` result is

   <img width="872" height="317" alt="Screenshot 2026-05-21 160344" src="https://github.com/user-attachments/assets/040a4e1e-fe60-4bdf-b740-67c5e954bac9" />
 
* Comparison between `GLS` and `RTL`  

<img width="1853" height="783" alt="Screenshot 2026-05-21 160516" src="https://github.com/user-attachments/assets/b7d20c04-b52a-43d2-b7b8-beb3fd6c2a8f" />


### Synth sim mismatch blocking statement part1

* Now lets study simulation mismatch in case of blocking statement
* Open `blocking_caveat.v` file

 <img width="1277" height="63" alt="Screenshot 2026-05-21 162450" src="https://github.com/user-attachments/assets/e9e3deed-2701-4882-96db-d7d1b6e08349" />
 
<img width="307" height="78" alt="Screenshot 2026-05-21 162624" src="https://github.com/user-attachments/assets/49b2bb9b-6644-4897-a61b-c515cfadc40c" />

* As `blocking assigment` used in reverse order, during simulation output will be given as if `X` is flopped output
  

<img width="377" height="192" alt="Screenshot 2026-05-21 162712" src="https://github.com/user-attachments/assets/a7a7b20e-acb3-4019-a26e-2a5ab6c7dd1c" />


* We can observe that our `RTL` simulated output is not giving output as per our hardware. in `RTL`, previous state of `X` is considered

<img width="872" height="403" alt="Screenshot 2026-05-21 163017" src="https://github.com/user-attachments/assets/4f5b5201-e11c-4b7f-b7ce-42617ffdf06e" />


### Synth sim mismatch blocking statement part2

* Now lets see synthesized netlist

  <img width="865" height="270" alt="Screenshot 2026-05-21 184731" src="https://github.com/user-attachments/assets/df80fca7-1aa5-4f41-ae23-f946afd79e64" />


* Comparison between `GLS` and `RTL` output

  <img width="887" height="340" alt="Screenshot 2026-05-21 185059" src="https://github.com/user-attachments/assets/56589410-9035-4789-a37d-43a039574e81" />
