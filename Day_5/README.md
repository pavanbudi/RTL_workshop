# Day 5 - Optimization in synthesis


## If Case constructs


### IF CASE Constructs part1

<img width="1272" height="663" alt="Screenshot 2026-05-21 235551" src="https://github.com/user-attachments/assets/83d340a0-9af9-4ad1-9cfa-a7a23c4c170d" />


* As in design , it is not specified what to do if `cond1`,`cond2` fails. So it will try to retain value of `Y`(latch)
* It is combinational loop, to avoid it tool keeps latch which latches/stores output `Y`  when `cond1` , `cond2` fails
  
 
<img width="1337" height="713" alt="Screenshot 2026-05-22 000048" src="https://github.com/user-attachments/assets/f4e02e5b-f8f5-4de6-896b-a9d032a4f16f" />


### IF CASE Constructs part2

* We shouldn't have incomplete latches or incomplete `IF` statements unless until it is intended. Lets see following example
* Here if `EN=0`, previous value should be retained which will be done through `inferred latch` added by tool during synthesis due to incomplete `IF`. So it is fine as logic given by tool is working as per intended behaviour by tool


<img width="1367" height="603" alt="Screenshot 2026-05-22 001215" src="https://github.com/user-attachments/assets/5fd7c6db-1441-4738-84cf-27d2c11a98b3" />

* Using `CASE` with `default` avoids `inferred latches` in netlist


### IF CASE Constructs part3


<img width="1307" height="751" alt="Screenshot 2026-05-22 002054" src="https://github.com/user-attachments/assets/ca7feebd-3b0d-4155-a2b2-b9a35910aff2" />

* Whe condition is matched in `IF` , remaining are ignored whereas remaining are checked in `CASE`. So we shouldnt have `overlapping CASES`

<img width="1230" height="718" alt="Screenshot 2026-05-22 003110" src="https://github.com/user-attachments/assets/c2407335-8402-4a15-a631-9431cacc9bc4" />


 ## Labs on "Incomplete If Case"


 ### Lab Incomplete IF part1

 
* Lets see files we use and open their verilog codes

  <img width="1452" height="102" alt="Screenshot 2026-05-22 003942" src="https://github.com/user-attachments/assets/b0060dd6-024a-4ad1-9387-4c8eae7b0dcb" />


* Lets analyse `incomplete IF` by comparing RTL design simulation with Synthesized Netlist simulation

  <img width="532" height="142" alt="Screenshot 2026-05-22 004541" src="https://github.com/user-attachments/assets/e121d5cf-8437-4964-bd47-c2be2c0d056a" />


  <img width="762" height="347" alt="Screenshot 2026-05-22 004708" src="https://github.com/user-attachments/assets/8dd35468-c65a-4034-9347-3790208dc2da" />
  

* `RTL` simulation

  
  <img width="1843" height="248" alt="Screenshot 2026-05-22 004854" src="https://github.com/user-attachments/assets/570d6f64-9872-405e-8654-4d896faa3cf6" />


* Synthesis output
* We can observe that `Latch` present in output but our aim was to build a `MUX`. It is due to incomplete `IF`

  
<img width="521" height="545" alt="Screenshot 2026-05-22 004933" src="https://github.com/user-attachments/assets/78fe162b-158e-4cb9-8e3e-0a2f60a7fe79" />


### Lab Incomplete IF part2

* Now consider `incomp_if2`


  <img width="1775" height="721" alt="Screenshot 2026-05-22 010107" src="https://github.com/user-attachments/assets/cf750d14-431f-45a7-b3dd-6de761316e0a" />


* Lets simulate and sythesize
  RTL simulation


<img width="1833" height="547" alt="Screenshot 2026-05-22 010630" src="https://github.com/user-attachments/assets/399b8b89-ec44-4ac3-8b7c-a1b24c43b3ab" />


  <img width="1687" height="380" alt="Screenshot 2026-05-22 010444" src="https://github.com/user-attachments/assets/79c0049b-93f8-4c8e-8550-36c0e5789c97" />


