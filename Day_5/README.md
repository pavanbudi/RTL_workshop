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


* Lets simulate and sythesize<br>RTL simulation


<img width="1833" height="547" alt="Screenshot 2026-05-22 010630" src="https://github.com/user-attachments/assets/399b8b89-ec44-4ac3-8b7c-a1b24c43b3ab" />


  <img width="1687" height="380" alt="Screenshot 2026-05-22 010444" src="https://github.com/user-attachments/assets/79c0049b-93f8-4c8e-8550-36c0e5789c97" />


## Labs on "Incomplete overlapping Case"


### incomplete overlapping Case part1


* Files we use
  

  <img width="1487" height="121" alt="Screenshot 2026-05-22 011408" src="https://github.com/user-attachments/assets/d34fec08-f5e8-4614-bcf2-edd6613d0b99" />


  * Lets start `incomp_case`<br> Code and expected design
 

    <img width="1595" height="712" alt="Screenshot 2026-05-22 011821" src="https://github.com/user-attachments/assets/bd26e71c-c7a3-4535-9e17-ef2ffd45d4ca" />


* Functional simulation


<img width="1853" height="630" alt="Screenshot 2026-05-22 012024" src="https://github.com/user-attachments/assets/8d5f4c92-4cd9-4568-9fed-00dc563fac9f" />


* Synthesis output<br> We can observe that it is same as our predicted design


<img width="867" height="206" alt="Screenshot 2026-05-22 012311" src="https://github.com/user-attachments/assets/d469059d-3c22-42df-b53f-d870d5e26ac3" />


### incomplete overlapping Case part2


* Now consider `Complete CASE`


  <img width="725" height="252" alt="Screenshot 2026-05-22 012744" src="https://github.com/user-attachments/assets/28fc66c2-56bf-43cc-b8fa-7fa208115ef3" />


  <img width="1848" height="911" alt="Screenshot 2026-05-22 012842" src="https://github.com/user-attachments/assets/c666a090-df3b-4142-a6b3-1b7b934e8b8a" />


 <img width="1837" height="537" alt="Screenshot 2026-05-22 012916" src="https://github.com/user-attachments/assets/0b0277c2-9b47-46ec-9d80-c397071b50ad" />


 * Lets consider `Partial CASE Assign`


<img width="982" height="511" alt="Screenshot 2026-05-22 013354" src="https://github.com/user-attachments/assets/9c750c00-774e-44d6-8279-ca648e182242" />


 <img width="1317" height="747" alt="Screenshot 2026-05-22 013520" src="https://github.com/user-attachments/assets/1b202a4e-5f27-49a0-8a0b-569a0e2f8245" />
   


### incomplete overlapping Case part3


* Synthesize


<img width="1845" height="588" alt="Screenshot 2026-05-22 013841" src="https://github.com/user-attachments/assets/80756c11-314e-4193-b56a-d11823ea46a6" />


* Lets consider `bad CASE`<br> Here simulator gets confused and synthesizer considers latest condition(`2'b1?`)


<img width="771" height="661" alt="Screenshot 2026-05-22 014045" src="https://github.com/user-attachments/assets/970dd055-46ff-48e4-8727-51f0953c9b5c" />


* We can observe that `Y` is following neither `i2` nor `i3` due to overlapping case statements(observe from code) which shows that simulator is getting confused

  
<img width="1852" height="705" alt="Screenshot 2026-05-22 014443" src="https://github.com/user-attachments/assets/637f845f-c62d-4635-9545-34285623d7c1" />


### incomplete overlapping Case part4

* Lets simulate synthesised netlist
* We can observe that there is no confusion incase of netlist simulation as `Y` equal to `i2` for `10`, `i3` for `11`  whereas in `RTL` simultion `Y` got stucked. Therefore it is simulation mismatch
* So overlapping cases is bad way of coding
* So two cases `states` should not overlap with each other. All should be mutually exclusive

  <img width="1851" height="687" alt="Screenshot 2026-05-22 115650" src="https://github.com/user-attachments/assets/81fdda03-82b2-4902-b7cd-b3e9715924eb" />


  
