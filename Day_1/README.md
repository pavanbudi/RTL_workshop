# Day-1- Introduction to Verilog RTL design and Synthesis

## Introduction to open-source simulator iverilog

### Sky130RTL D1SK1 L1 Introduction to iverilog design testbench


**What is a Simulator?**
* RTL design is implementation of specifications. So, the intend of spec is need to be verified by simulating the design.
* Simulator is a tool used to simulate the design. In this course we use an open-source hardware simulation tool like iverilog for simulating digital circuits which is written in Verilog Hardware Description Language (HDL).


**What is a Design?**
Design is the actual Verilog code or set of verilog codes which dictates the hardware for intended function to meet the required specifications.


**What is a Test-Bench?**
Test-bench is a setup used to test the design. The testbench provides the required stimulus to the design under test (DUT). The DUT is placed in the testbench. The testbench generates the stimuli (input signals) for the design and captures the output of the design, which is then compared with the expected output to verify the functionality of the design and checks the functionality.


**How Simulator Works?**
* Simulator looks for change in values of input
* Upon change of the input, output is evaluated (no change to input implies no change to output)

We have a design with primary inputs (inputs to DUT) and primary outputs (outputs from DUT). To test the primary inputs we have to provide the stimulus and for the outputs we need to observe the stimulus. For this we have "Stimulus Generator" and "Stimulus Observer". This is how a test-bench looks like.

<img width="787" height="385" alt="Screenshot 2026-05-16 014232" src="https://github.com/user-attachments/assets/95a90583-02d3-49a1-8964-e6365a9a2dd2" />


**NOTE:**
* Design has its own set of Primary inputs and Primary Outputs.
* Test Bench doesnt have any Primary Inputs or Primary Outputs. 


**iverilog Simulator Flow:**
* Give the design verilog code and testbench to iverilog.
* Any simulator looks for changes in input and dump changes in output
* Simulator (`iverilog`) takes design and testbench code and generates an output executable file called `a.out` (which has the changes in the output for the changes in the input).
* All the outputs of the simulator is Value Change Dump (VCD) format file.
* For observing the waveform we will give the `a.out` format file to GTKwave and observe the logic level changes.

<img width="898" height="497" alt="Screenshot 2026-05-16 015323" src="https://github.com/user-attachments/assets/59297727-1aec-4d01-ad09-b791044590ce" />


## Labs using iverilog and gtkwave

### Sky130RTL D1SK2 L1 Lab1 Introduction to lab

Now we will be looking at the environment setup which are needed for the course. First we will do tool setup then file setup required.
1. Open the terminal.
2. Enter into `home/vsduser/VSDSquadron_FM`
3. Clone the Workshop Repository using git clone
   ```bash
   git clone [https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git](https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git)
   ```
   <img width="752" height="432" alt="Screenshot 2026-05-14 000103" src="https://github.com/user-attachments/assets/2fbf5350-1088-4efb-aea5-4adb34c8094b" />

   
4. Now enter into directory `sky130RTLDesignAndSynthesisWorkshop`(created by cloning github) by entering
     `cd sky130RTLDesignAndSynthesisWorkshop`
5. Install Required Tools:
   ```bash
   sudo apt install iverilog
   sudo apt install gtkwave
   ```
6. Inside the `sky130RTLDesignAndSynthesisWorkshop` directory, we have 
   * `my_lib` which has folder `verilog_model` that contain all std. cell verilog models of std. cells which are present in '.lib'(std. cell library)

   
      <img width="933" height="48" alt="Screenshot 2026-05-16 092138" src="https://github.com/user-attachments/assets/b624c6ce-4c9f-4424-9c8f-278776453d14" />


      
   * `lib` which has `sky130_fd_sc_hd__tt_025C_1v80.lib` std. cell library which we will use for synthesis
   
      
     <img width="755" height="47" alt="Screenshot 2026-05-16 093254" src="https://github.com/user-attachments/assets/30a676ed-d389-4516-9767-3e5ee3c9bb80" />


      
   * `verilog_files` folder contains all our lab files like verilog source and testbench files

   
      <img width="1787" height="143" alt="Screenshot 2026-05-16 093117" src="https://github.com/user-attachments/assets/b08a8242-d53d-4a6e-b8d9-2a1a30395441" />




### Sky130RTL D1SK2 L1 Lab2 Introduction to iverilog gtkwave part1

we will see how to work with iverilog and gtkwave:

We are inside `verilog_files` folder where for every file there is a corresponding 'tb_' file associated with it. We run iverilog by passing design and testbench file of a design.

Step 1: Compile and Simulate then we can see a file `a.out` is getting created


<img width="1265" height="78" alt="Screenshot 2026-05-16 160623" src="https://github.com/user-attachments/assets/8910c861-b8c1-4b20-9889-12fd76581c26" />



Step 2: Execute the output file `a.out` which will dump `vcd file` upon execution as we know that output of simulator is a vcd_file.


<img width="882" height="52" alt="Screenshot 2026-05-16 101741" src="https://github.com/user-attachments/assets/bedbaa8e-f8f3-42ef-8a57-9951691dc66c" />



Step 3: Load the vcd file at the simulator by giving vcd file `td_good_mux.vcd` as input


<img width="1013" height="103" alt="Screenshot 2026-05-16 102340" src="https://github.com/user-attachments/assets/0ffac2e1-4286-4ded-8c52-477820beb4d7" />



A window will pop up projecting the waveform, Follow the following steps:

* Click on test bench shown at left
* Signals will be shown
* Drag and Drop the signals above empty space for signals.
* We will see the waveform for the required multiplexer.
* Click on zoom fit, to show complete waveform.


<img width="957" height="915" alt="Screenshot 2026-05-16 102757" src="https://github.com/user-attachments/assets/2326be81-4014-4b80-9849-95b59a792c7d" />



### Sky130RTL D1SK2 L3 Lab3 Introduction to iverilog gtkwave part2

Lets know what exactly is written inside files
Enter following commands:


<img width="1080" height="22" alt="Screenshot 2026-05-16 103814" src="https://github.com/user-attachments/assets/b7b2b796-c994-4934-b1f8-dad66b12fdbe" />


Now code and testbench file will be opened


<img width="960" height="298" alt="Screenshot 2026-05-16 110752" src="https://github.com/user-attachments/assets/b7f9cc7e-abe0-4ea9-81a2-cb09f3607376" />


```verilog
module good_mux (input i0, input i1, input sel, output reg y);
```

* The module block is defined by the name `good_mux`
* `i0`: first input
* `i1`:  second input
* `sel`:  select signal
* `y`: output declared as reg, because it will be assigned inside an always block.

```verilog
always @(*)
```

* This is a combinational `always` block.
* `@(*)` means it is sensitive to any signal used in the block changes.

```verilog
begin
```

* Begins the block of statements that will execute when triggered.

```verilog
if(sel)
    y = i1;
else
    y = i0;
```

* If the `sel` is high (1), then `i1` is assigned to `y`.
* Otherwise (`sel` is `0`), `i0` is assigned to `y`.

```verilog
end
endmodule
```

* These lines end the `always` block and the `module` respectively.

Below is the testbench `tb_good_mux.v` for the `good_mux` module.


<img width="957" height="653" alt="Screenshot 2026-05-16 110745" src="https://github.com/user-attachments/assets/7e30e7aa-eaa7-439a-88b3-8b7e000da99b" />


```verilog
timescale 1ns / 1ps 
```

* Sets simulation time unit and time precision.
* `1ns` = 1nanosecond time step
* `1ps` = precision of 1 picosecond (used for delay rounding).


```verilog
module tb_good_mux;
```

* Declares the testbench module tb_good_mux.
* Notice that testbech is not having any primary inputs or primary outputs.

Variable Declaration :
- `No ports in testbench module.`
- `So, we need internal variables to hold stimulus values and observe.`

```verilog
reg i0,i1,sel;
wire y;
```

- `Declare the inputs as reg as we need to change them in procedural block.`
- `y is declared as wire since it will be connected to the output of good_mux (Design Under Test).`

```verilog
good_mux uut (
    .i0(i0),
    .i1(i1),
    .sel(sel),
    .y(y)
);
```

* Instantiates the good_mux module.
* uut stands for Unit Under Test.
* Connect the testbench signals (i0, i1, sel, y) to the ports of good_mux.`

```verilog
initial begin
    $dumpfile("tb_good_mux.vcd");
    $dumpvars(0, tb_good_mux);
```

* Generates a VCD (Value Change Dump) file for waveform viewing.
* Dumps all variables inside the module tb_good_mux in the VCD file.

```verilog
    // Initialize Inputs
    i0 = 0;
    i1 = 0;
    sel = 0;
```

* Initializes values to signals at time 0.

```verilog
#200 $finish;
```

- `Ends the simulation after 200 ns.`

```verilog
end
```

- `Ends the initial block.`

```verilog
always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
```

* Using this toggles the value of sel every 75 time unit
* toggles value of i0 every 10ns.
* Toggles value of i1 every 55ns.
* It is stimulus generator block.

```verilog
endmodule
```

* Ends the tb_good_mux module.



## Introduction to Yosys and Logic Synthesis

### Sky130RTL D1SK1 L1 Introduction to Yosys

Yosys is an open-source Verilog RTL synthesis tool, which takes your RTL and standard cell library as input. And gives out Netlist.

Netlist is representation of design in form of std. cells present in `.lib`.

How Yosys tool synthesizes RTL and gives Netlist?
To do so The using Yosys is as follows: We pass the design and we pass the `.lib` file which tells the library we have mapped our gates. It output Netlist

Synthesis
* We give a read_verilog command to read the design and read_liberty command to read the `.lib`.
* All the mappings done using read_verilog, read_liberty and write_verilog command is used to give netlist file.


<img width="1867" height="990" alt="Screenshot 2026-05-16 114947" src="https://github.com/user-attachments/assets/9b9b91ee-9acb-48b7-9f87-7c48d1bae1c1" />


Verify Synthesis:
1. We read the netlist and the testbench.
2. We pass the testbench to iverilog(we can use same that we used as RTL testbench).
3. We get vcd file from iverilog.
4. Pass gtkwave to get the waveform(waveforms should match with waveforms we got for RTL Simulation).


<img width="1835" height="977" alt="Screenshot 2026-05-16 115711" src="https://github.com/user-attachments/assets/a298d2ce-1ee6-4d79-be87-872383a9d1e4" />


### Sky130RTL D1SK1 L2 Introduction to Logic Synthesis part1

We will discuss about standard cell flow of logic synthesis.
1. RTL Design: RTL design is the behavioral representation of required specification. It is combination of behavioral and dataflow statements.


<img width="1212" height="882" alt="Screenshot 2026-05-16 120348" src="https://github.com/user-attachments/assets/a7a44e98-7456-4b26-bcf9-bb737ccf9174" />


How to convert the RTL design into a actual logic circuit using Logic Synthesizer?


<img width="1258" height="827" alt="Screenshot 2026-05-16 120404" src="https://github.com/user-attachments/assets/dd2a6326-c948-4505-9b2b-fd43940ad58f" />


* We need to convert RTL to gate level translation.
* The design is converted into gate and the connections are made between the gates.
* This representation is called Netlist i.e., file returned out.


<img width="606" height="882" alt="Screenshot 2026-05-16 120424" src="https://github.com/user-attachments/assets/548c49ca-6199-4e94-8904-c7f090e43701" />


What is `.lib` ?
* It is a collection of all logical modules and standard cells.
* It includes all basic logic gates like AND, OR, NOR, NAND, etc.
* It also includes different flavours of same logic gates like slow, medium and fast gates.


<img width="1367" height="882" alt="Screenshot 2026-05-16 120511" src="https://github.com/user-attachments/assets/9f139c7e-a6c6-432f-b119-f85f2c8f9972" />


Why do we need different flavours of gates?
We know combinational delay in logic path determines the max speed of operation of digital logic circuit.
Tclk > Tcq_a + Tcomb + Tsetup_b. We need cells that work fast to make Tcomb small.


<img width="1355" height="878" alt="Screenshot 2026-05-16 120551" src="https://github.com/user-attachments/assets/889c2fcb-f1ac-4f03-91f5-0500f5de9076" />

But we also need slow cells.

### Sky130RTL D1SK3 L3 Introduction to Logic Synthesis part2

Why do we need slow cells?
Just like setup time we also have hold time. The FF_B should start after FF_A starts and not before. TO ensure that there are no "HOLD" issues at DFF_B, we need cells that work slowly.Hence we need cells that work fast to meet the setup requirement and cells that work slow to meet the hold requirements. The collection forms the `.lib`


<img width="1298" height="921" alt="Screenshot 2026-05-16 121159" src="https://github.com/user-attachments/assets/1b649124-b4d3-4552-abdf-8565666c746e" />


Faster vs Slower cells:


<img width="1306" height="802" alt="Screenshot 2026-05-16 121240" src="https://github.com/user-attachments/assets/16c9cd96-974a-45eb-aef4-9d69b51a44b8" />


Selection of cells:


<img width="1256" height="835" alt="Screenshot 2026-05-16 121324" src="https://github.com/user-attachments/assets/3a822d79-47a8-4aac-a69f-40ad39219322" />


Synthesis Illustration:
First step a synthesizer is going to do is a syntactical check and then it will start mapping the design. The module maps with the top level ports of the design.

`assign out = sel ? a : b;` a Verilog continuous assignment using the ternary operator (`?:`), which is a short-hand way to write an if-else statement. If `sel` is 1, assign `a` to `out`, otherwise, assign `b` to `out`. It is basically describing a 2:1 multiplexer. Then there is a flop. where the output of mux is input of flip flop. The next code is for flip flop. This is the conversion of RTL into netlist using gates available in the `.lib`


<img width="1390" height="961" alt="Screenshot 2026-05-16 121419" src="https://github.com/user-attachments/assets/29fc0f8f-dedf-4d08-9b35-e9184634f74a" />



## Labs using Yosys and Sky130 PDKs

### Sky130RTL D1SK4 L1 Lab2 Yosys 1 good mux part1

Here we will see how to invoke Yosys and run a logic synthesis on designs. We will be reading the `.lib` file and we pass the `.v` file and run a basic synthesis flow.

To invoke yosys type `yosys`


<img width="957" height="205" alt="Screenshot 2026-05-16 122509" src="https://github.com/user-attachments/assets/b7400b72-5731-4acc-9750-011ef642b722" />


Now we have to read `.lib`
* Command used for this read is
`read_liberty -lib <path_to_lib.lib>`


<img width="942" height="136" alt="Screenshot 2026-05-16 123245" src="https://github.com/user-attachments/assets/9d903b49-8236-4a58-abe9-7ce1dc9d5801" />


* Next step is to read the design file, here we will read `good_mux.v` using the command
`read_verilog good_mux.v`


<img width="948" height="167" alt="Screenshot 2026-05-16 123400" src="https://github.com/user-attachments/assets/b921ebfe-a058-4bd5-98b6-9aeb36cbcc5c" />


* Command to execute the module `good_mux` is
`synth -top good_mux`


<img width="947" height="797" alt="Screenshot 2026-05-16 123636" src="https://github.com/user-attachments/assets/02f517eb-2f96-4ac0-b81f-0a7daf85b304" />


<img width="952" height="923" alt="Screenshot 2026-05-16 123655" src="https://github.com/user-attachments/assets/9570ef14-cf2a-4839-a887-aef1b8980f93" />


We have completed reading library(liberty file) and design, now lets map the generic library to design and generate netlist.
* Command is `abc -liberty`, where `abc` converts our RTL into gate and gate it should be coverted is specified in `-liberty` file.
          
`abc -liberty <path_to_lib.lib>`


<img width="958" height="833" alt="Screenshot 2026-05-16 124045" src="https://github.com/user-attachments/assets/bc5b898d-3510-4108-9b00-3a6fa15c4d5f" />


<img width="957" height="930" alt="Screenshot 2026-05-16 124057" src="https://github.com/user-attachments/assets/a9abd78d-ee81-43b7-a8c6-0cf0b44c39d8" />



We can see detail of logic gates which is used, and the internal signals, input and output signals from above image.
To show the graphical representation of this netlist, the command used is `show`


<img width="942" height="872" alt="Screenshot 2026-05-16 125146" src="https://github.com/user-attachments/assets/0e53cdf1-aa7a-4580-a82c-886be84498e4" />



### Sky130RTL D1SK4 L2 Lab2 Yosys 1 good mux Part3

We will now see how netlist looks.

* Command to write the synthesized gate level netlist
`write_verilog good_mux_netlist.v`


<img width="952" height="205" alt="Screenshot 2026-05-16 152048" src="https://github.com/user-attachments/assets/50c84263-0c6a-45f4-b479-9cc5b95adde6" />


* To open the file `good_mux_netlist.v`,enter command
`!gvim good_mux_netlist.v`


<img width="960" height="190" alt="Screenshot 2026-05-16 152632" src="https://github.com/user-attachments/assets/a4f36e96-e8c1-43f5-bce3-90056cad8fab" />


* Netlist file


<img width="957" height="931" alt="Screenshot 2026-05-16 152643" src="https://github.com/user-attachments/assets/475c71b8-2eee-4322-8be8-a79a29712a32" />


Note:Netlist has unnecessary attributes, we can have simple netlist by modifying switch:
command: `write_verilog -noattr goodmux_netlist.v`


<img width="908" height="343" alt="Screenshot 2026-05-16 153511" src="https://github.com/user-attachments/assets/49dd07ae-18bc-461d-8aea-db159cbbac11" />

         

Simple Netlst:


<img width="958" height="1010" alt="Screenshot 2026-05-16 153154" src="https://github.com/user-attachments/assets/a3896579-ec80-4ad9-a691-a76f4f567074" />

