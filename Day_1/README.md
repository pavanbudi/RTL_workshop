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

![Test Bench Diagram](Screenshot 2026-05-16 014232.png)


**NOTE:**
* Design has its own set of Primary inputs and Primary Outputs.
* Test Bench doesnt have any Primary Inputs or Primary Outputs. 


**iverilog Simulator Flow:**
* Give the design verilog code and testbench to iverilog.
* Any simulator looks for changes in input and dump changes in output
* Simulator (`iverilog`) takes design and testbench code and generates an output executable file called `a.out` (which has the changes in the output for the changes in the input).
* All the outputs of the simulator is Value Change Dump (VCD) format file.
* For observing the waveform we will give the `a.out` format file to GTKwave and observe the logic level changes.

![Simulator Flow Diagram](Screenshot 2026-05-16 015323.png)

## Labs using iverilog and gtkwave

### Sky130RTL D1SK2 L1 Lab1 Introduction to lab

Now we will be looking at the environment setup which are needed for the course. First we will do tool setup then file setup required.
1. Open the terminal.
2. Enter into `home/vsduser/VSDSquadron_FM`
3. Clone the Workshop Repository using git clone
   ```bash
   git clone [https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git](https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git)
   ```
   ![Entering vsduser directory](Screenshot 2026-05-16 000103.png)
   
4. Now enter into directory `sky130RTLDesignAndSynthesisWorkshop`(created by cloning github) by entering
    `cd sky130RTLDesignAndSynthesisWorkshop`
5. Install Required Tools:
   ```bash
   sudo apt install iverilog
   sudo apt install gtkwave
   ```
6. Inside the `sky130RTLDesignAndSynthesisWorkshop` directory, we have 
   * `my_lib` which has folder `verilog_model` that contain all std. cell verilog models of std. cells which are present in '.lib'(std. cell library)
      
      ![Terminal showing files 1](Screenshot 2026-05-16 092138.png)
      
   * `lib` which has `sky130_fd_sc_hd__tt_025C_1v80.lib` std. cell library which we will use for synthesis
      
      ![Terminal showing files 2](Screenshot 2026-05-16 093254.png)
      
   * `erilog_files` folder contains all our lab files like verilog source and testbench files
   
      ![Terminal showing files 3](Screenshot 2026-05-16 093117.png)




### Sky130RTL D1SK2 L1 Lab2 Introduction to iverilog gtkwave part1

we will see how to work with iverilog and gtkwave:

We are inside `verilog_files` folder where for every file there is a corresponding 'tb_' file associated with it. We run iverilog by passing design and testbench file of a design.

Step 1: Compile and Simulate then we can see a file `a.out` is getting created

![Terminal showing files 3](Screenshot 2026-05-16 160623.png)

Step 2: Execute the output file `a.out` which will dump `vcd file` upon execution as we know that output of simulator is a vcd_file.

![Terminal showing files 3](Screenshot 2026-05-16 101741.png)

Step 3: Load the vcd file at the simulator by giving vcd file `td_good_mux.vcd` as input

![Terminal showing files 3](Screenshot 2026-05-16 102340.png)

A window will pop up projecting the waveform, Follow the following steps:

* Click on test bench shown at left
* Signals will be shown
* Drag and Drop the signals above empty space for signals.
* We will see the waveform for the required multiplexer.
* Click on zoom fit, to show complete waveform.

![Terminal showing files 3](Screenshot 2026-05-16 102757.png)


### Sky130RTL D1SK2 L3 Lab3 Introduction to iverilog gtkwave part2

Lets know what exactly is written inside files
Enter following commands:
![Terminal showing opening code files](Screenshot 2026-05-16 103814.png)

Now code and testbench file will be opened
![Terminal showing code and testbench files](Screenshot 2026-05-16 110752.png)

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

![tb_good_mux testbench file](Screenshot 2026-05-16 110745.png)

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

![Yosys Flow 1](Screenshot 2026-05-16 114947.png).

Verify Synthesis:
1. We read the netlist and the testbench.
2. We pass the testbench to iverilog(we can use same that we used as RTL testbench).
3. We get vcd file from iverilog.
4. Pass gtkwave to get the waveform(waveforms should match with waveforms we got for RTL Simulation).

![Verify Synthesis Flow](Screenshot 2026-05-16 115711.png)


### Sky130RTL D1SK1 L2 Introduction to Logic Synthesis part1

We will discuss about standard cell flow of logic synthesis.
1. RTL Design: RTL design is the behavioral representation of required specification. It is combination of behavioral and dataflow statements.

![RTL Code Snippet](Screenshot 2026-05-16 120348.png)

How to convert the RTL design into a actual logic circuit using Logic Synthesizer?

![Logic Synthesizer Flow](Screenshot 2026-05-16 120404.png)

* We need to convert RTL to gate level translation.
* The design is converted into gate and the connections are made between the gates.
* This representation is called Netlist i.e., file returned out.

![Netlist Representation](Screenshot 2026-05-16 120424.png)

What is `.lib` ?
* It is a collection of all logical modules and standard cells.
* It includes all basic logic gates like AND, OR, NOR, NAND, etc.
* It also includes different flavours of same logic gates like slow, medium and fast gates.

![.lib Diagram](Screenshot 2026-05-16 120511.png)

Why do we need different flavours of gates?
We know combinational delay in logic path determines the max speed of operation of digital logic circuit.
Tclk > Tcq_a + Tcomb + Tsetup_b. We need cells that work fast to make Tcomb small.

![Tcomb Diagram](Screenshot 2026-05-16 120551.png)

But we also need slow cells.

### Sky130RTL D1SK3 L3 Introduction to Logic Synthesis part2

Why do we need slow cells?
Just like setup time we also have hold time. The FF_B should start after FF_A starts and not before. TO ensure that there are no "HOLD" issues at DFF_B, we need cells that work slowly.Hence we need cells that work fast to meet the setup requirement and cells that work slow to meet the hold requirements. The collection forms the `.lib`

![Hold Time Diagram](Screenshot 2026-05-16 121159.png)

Faster vs Slower cells:

![Faster vs Slower Cells Slide](Screenshot 2026-05-16 121240.png)

Selection of cells:

![Selection of Cells Slide](Screenshot 2026-05-16 121324.png)

Synthesis Illustration:
First step a synthesizer is going to do is a syntactical check and then it will start mapping the design. The module maps with the top level ports of the design.

`assign out = sel ? a : b;` a Verilog continuous assignment using the ternary operator (`?:`), which is a short-hand way to write an if-else statement. If `sel` is 1, assign `a` to `out`, otherwise, assign `b` to `out`. It is basically describing a 2:1 multiplexer. Then there is a flop. where the output of mux is input of flip flop. The next code is for flip flop. This is the conversion of RTL into netlist using gates available in the `.lib`

![Synthesis Illustration Flow](Screenshot 2026-05-16 1121419.png)

## Labs using Yosys and Sky130 PDKs

### Sky130RTL D1SK4 L1 Lab2 Yosys 1 good mux part1

Here we will see how to invoke Yosys and run a logic synthesis on designs. We will be reading the `.lib` file and we pass the `.v` file and run a basic synthesis flow.

To invoke yosys type `yosys`

![Yosys Invocation](Screenshot 2026-05-16 122509.png)

Now we have to read `.lib`
* Command used for this read is
`read_liberty -lib <path_to_lib.lib>`

![Read Liberty Output](Screenshot 2026-05-16 123245.png)

* Next step is to read the design file, here we will read `good_mux.v` using the command
`read_verilog good_mux.v`

![Read Verilog Output](Screenshot 2026-05-16 123400.png)

* Command to execute the module `good_mux` is
`synth -top good_mux`

![Synth Top Output 1](Screenshot 2026-05-16 123636.png)

![Synth Top Output 2](Screenshot 2026-05-16 123655.png)

We have completed reading library(liberty file) and design, now lets map the generic library to design and generate netlist.
* Command is `abc -liberty`, where `abc` converts our RTL into gate and gate it should be coverted is specified in `-liberty` file.
          
`abc -liberty <path_to_lib.lib>`

![ABC Liberty Output 1](Screenshot 2026-05-16 124045.png)

![ABC Liberty Output 2](Screenshot 2026-05-16 124057.png)

We can see detail of logic gates which is used, and the internal signals, input and output signals from above image.
To show the graphical representation of this netlist, the command used is `show`

![Show Netlist Graphical View](Screenshot 2026-05-16 125146.png)

### Sky130RTL D1SK4 L2 Lab2 Yosys 1 good mux Part3

We will now see how netlist looks.

* Command to write the synthesized gate level netlist
`write_verilog good_mux_netlist.v`

![Write Verilog Output](Screenshot 2026-05-16 152048.png)

* To open the file `good_mux_netlist.v`,enter command
`!gvim good_mux_netlist.v`

![Cat Netlist Error Output](Screenshot 2026-05-16 152632.png)

* Cat the netlist file

![Cat Netlist Success Output](Screenshot 2026-05-16 152643.png)

Note:Netlist has unnecessary attributes, we can have simple netlist by modifying switch:
command: `write_verilog -noattr goodmux_netlist.v`

![Entering command for getting simple netlist and showing it](Screenshot 2026-05-16 153511.png)         

Simple Netlst:

![Simple Netlist Output ](Screenshot 2026-05-16 153154.png)
