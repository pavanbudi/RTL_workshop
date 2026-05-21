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


 ## Labs on "Incomplete If Case"

 ### Lab Incomplete IF part1

 
<img width="1230" height="718" alt="Screenshot 2026-05-22 003110" src="https://github.com/user-attachments/assets/8ddbf8b5-ec99-4d80-bc60-fb20e9c07dbb" />
