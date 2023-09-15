## PES ASIC CLASS
</details>
<details>
	
<summary> WEEK1  </summary>

# Basic Definition:
An Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software. The ISA acts as an interface between the hardware and the software, specifying both what the processor is capable of doing as well as how it gets done.
RISC-V is an open-source instruction set architecture used to develop custom processors for a variety of applications, from embedded designs to supercomputers. From Apps to Hardware
# Applications: 
Applications, also known as software applications or simply apps, are programs or software designed to perform specific tasks or functions for end-users. Examples include word processors, web browsers, and games
# System Software: 
System software refers to a collection of programs and utilities that manage and control a computer system's hardware and provide services to other software applications. It includes the operating system, device drivers, and system utilities.
# Compiler:
A compiler is a software tool that translates high-level programming code (source code) written by humans into machine code or intermediate code that can be executed directly by a computer's hardware or by a virtual machine.
# Assembler: 
An assembler is a program or tool that translates assembly language code, a low-level human-readable representation of machine code instructions, into machine code that can be executed by a computer's CPU.

# RTL (Register-Transfer Level): 
RTL, or Register-Transfer Level, is a level of hardware description language used to model the behavior of digital circuits at a low level of abstraction. It specifies how data moves between registers and how logic operations are performed.
Hardware: Hardware refers to the physical components of a computer system, including the CPU, memory, storage devices, input/output devices, and other electronic and mechanical components. It is the tangible, physical part of a computer system




#  LABWORK FOR RISC TOOLCHAIN
1a #Writing C program using leaf header to find sum of integers from1 to 1 to n
 #include<stdio.h>
 int main(){
   int i, sum=0, n=111;
   for (i=1;i<=n; ++i) {
   sum +=i;
   } 
  printf("Sum of numbers from 1 to %d is %d \n",n,sum);
 return 0;
  }

![image](https://github.com/pavithra7369/asic/assets/143084423/8ea3e3ed-bccb-4517-be05-5d4939c223be)

 to get the output we use gcc compiler
 
 ![image](https://github.com/pavithra7369/asic/assets/143084423/91ac5138-57b9-4b6b-b08a-4c840ae1a881)
 
Using the RISC-V GCC compiler, we compiled the C program. riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o p1.o p1.c Using ls -ltr p1.c we can check that the object file is created.

![image](https://github.com/pavithra7369/asic/assets/143084423/93da6b2c-c8a3-46e8-8faa-8b6a0f76788a)

to get dissembled ALP code use: riscv64-unknown-elf-objdump -d p1.o | less
In order to view the main section, type /main

![image](https://github.com/pavithra7369/asic/assets/143084423/b9202056-49b6-412d-b58f-2c640ff17033)

the byte information increments by 4 bytes,
number of instructions =1084/4

Spike Simulation and Debug: spike pk p1.o is used to check whether the instructions produced are right to give the correct output.
spike -d pk p1.c is used for debugging.

1b.Write a C program p2 that shows the maximum and minimum values of 64 bit signed numbers

![image](https://github.com/pavithra7369/asic/assets/143084423/70ea471f-02f6-4412-9b1f-7953d2bac52c)

after compiling

![image](https://github.com/pavithra7369/asic/assets/143084423/675cb8c6-e0f2-4da9-8450-2a62243a167d)

1c.Write a C program p3 that shows the maximun and minimum values of 64 bit unsigned numbers

![image](https://github.com/pavithra7369/asic/assets/143084423/585f71cf-bbfe-4025-b04a-803f9a7ab667)

after compiling

![image](https://github.com/pavithra7369/asic/assets/143084423/ca7c3286-7a23-4de3-b32c-e20328e58f13)


# Application binary interface(ABI)
ABI (application binary interface), as the name says, is an interface, that helps programs access system hardware and services.
ABI defines how your code is stored inside the library file, so that any program using your library can locate the desired function and execute it.
Each register has a specific name called ABI name which access the internal registers of internal registers.

Labwork
Write C code in one file and your assembly code in a separate file. In the assembly file, we declared assembly functions with appropriate signatures that match the calling conventions of your platform.
C Program - Sum of numbers from 1 to 9:
![image](https://github.com/pavithra7369/asic/assets/143084423/ffeb1c5f-fac0-45b2-bf37-2abefc7f3a5f)

assembly code

![image](https://github.com/pavithra7369/asic/assets/143084423/b94e6ba2-d773-4b2b-97ba-545858901e97)

Compilation: To compile C code and Asseembly file use the command
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o p3.o p3.c load.s this would generate object file p3.o
Execution: To execute the object file run the command spike pk p3.o

![image](https://github.com/pavithra7369/asic/assets/143084423/a296774b-3f68-4b6c-a2f0-a8cc4f064c02)

</details>
<details>
<summary>	WEEK 2 DAY 1:RTL DESIGN USING VERILOG WITH SKY130 TECHNOLOGY </summary>

# Installation
> git clone https://github.com/YosysHQ/yosys.git

> cd yosys

> sudo apt install make

> sudo apt-get update

> sudo apt-get install build-essential clang bison flex  libreadline-dev gawk tcl-dev libffi-dev git  graphviz xdot pkg-config python3 libboost-system-dev libboost-python-dev libboost-filesystem-dev zlib1g-dev

> make config-gcc

> make

> sudo make install

> sudo apt install gtkwave

![WhatsApp Image 2023-09-02 at 19 12 29](https://github.com/pavithra7369/asic/assets/143084423/fc6ba69b-1112-44da-98b0-c0f24f826f73)

+ Yosys installation
  
   $ git clone https://github.com/YosysHQ/yosys.git
  
   $ cd yosys-master
  
   $ sudo apt install make
  
   $ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
  
  $ make
  
  $ sudo make install
  
  ![WhatsApp Image 2023-09-02 at 19 17 44](https://github.com/pavithra7369/asic/assets/143084423/d1cb3e7f-4330-45fb-ad21-f2b0aa514ba3)

  + Iverilog installation command
    > sudo apt-get install iverilog

    ![WhatsApp Image 2023-09-02 at 19 20 27](https://github.com/pavithra7369/asic/assets/143084423/99e68623-0f7f-4062-8efc-bac965a30b80)

  + gtkwave simulator installation command
    > sudo apt-get install gtkwave

    ![WhatsApp Image 2023-09-02 at 19 22 38](https://github.com/pavithra7369/asic/assets/143084423/0646e0cf-e994-41f1-a483-9f6727a287b9)



## **Introduction to open-source simulator iverilog**
__Simulator__
   + simulator is a tool used for checking the design
   
   + RTL design is checked for adherence to the spec by simulating the design
   
   + Simulator is a tool used for simulating the design(iverilog is the simulator here)
   
__Design__
   + Design is the actual verilog code or set of verilog codes which has the intended functionality to meet with required specifications
   
__Testbench__
     + Testbench is the setup to apply stimulus(test_vectors) to the design to check it's functionality and match it to spec
     
__How Simulator Works?__
   + Simulator looks for the change on input signals
   + Upon change to the input the output will be evaluated,no change in input-no change in output
   + Simulator is looking for change in the values of input.
   
   ![WhatsApp Image 2023-09-02 at 16 29 45](https://github.com/pavithra7369/asic/assets/143084423/621d6e08-28d5-4e9e-9b27-99340d98eb39)

 __iverilog based simulation flow__
 ![WhatsApp Image 2023-09-02 at 16 29 46](https://github.com/pavithra7369/asic/assets/143084423/5f5a8767-af09-4633-8363-4813dfe20400)
  VCD file-value change dump format, vcd file is used because we are looking for changes in values
  gtkwave-is used for viewing the waveform
  
_examples with testbenches_
  ![WhatsApp Image 2023-09-02 at 16 43 05](https://github.com/pavithra7369/asic/assets/143084423/f358224b-06af-4b64-9e21-846920cab8aa)
  
 
    module good_mux (input i0 , input i1 , input sel , output reg y); 
  
    always @ (*)
 
     begin
		if(sel)
		y <= i1;
		else 
		y <= i0;
	end
      endmodule
      

      timescale 1ns / 1ps
    module tb_good_mux;
    // Inputs
    reg i0,i1,sel;
    // Outputs
    wire y;
  		// Instantiate the Unit Under Test (UUT), name based instantiation
	good_mux uut (.sel(sel),.i0(i0),.i1(i1),.y(y));
	//good_mux uut (sel,i0,i1,y);  //order based instantiation
    initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
     end
    always #75 sel = ~sel;
    always #10 i0 = ~i0;
    always #55 i1 = ~i1;
    endmodule

**we have stimulus generator,we dont have stimulus observer,we arre directly dumping the vcd file and observing the output.**

## simulation
**commands used are**
> iverilog filename.v tb_filename.v

>./a.out      #this cwhen executed, this dumps the vcd file

> gtkwave tb_filename.vcd
 
![WhatsApp Image 2023-09-02 at 16 47 01](https://github.com/pavithra7369/asic/assets/143084423/c70b5b97-cbee-4720-8392-00adf48a804e)

![WhatsApp Image 2023-09-02 at 17 02 13](https://github.com/pavithra7369/asic/assets/143084423/99377cec-3618-4696-9820-52b74b68dd5c)

when multiplexer's select line=0, the output is following I0,when select line =1,the output follows I1
To look into what is exactly written in this file use the following command
gvim tb_good_mux.v -o good_mux.v

![WhatsApp Image 2023-09-02 at 17 09 36](https://github.com/pavithra7369/asic/assets/143084423/c79ddabd-79a4-400d-af11-e79a2ef75a82)


## synthesis
  Introduction to yosys
 **Synthesizer**
  + Tool used for converting the RTL to netlist
  + Yosys is the synthesizer in this course

![WhatsApp Image 2023-09-02 at 17 16 58](https://github.com/pavithra7369/asic/assets/143084423/85768ab1-2d4d-4f61-aba8-ba40aa572a16)

>read_verilog command is to read the design
>read_liberty to read .lib files
>write_verilog is to write netlist file
>Netlist is representation of design in cells present in .lib

**Verify the synthesis**

![WhatsApp Image 2023-09-02 at 17 21 04](https://github.com/pavithra7369/asic/assets/143084423/d342605e-586e-450b-94fb-5868e3f1c2ac)

+ The set of primary inputs/primary outputs will remain same between RTL design and synthesized netlist

**RTL design:**

Behavioural representation of required specification

**Synthesis:**

 It is RTL to gate level translation,this file is given out as a file called netlist
 
**.lib**

.lib is a collection of logical modules,there are different flavours of same gate.

-->We reqire different flavours of the same gate for example a 2 input AND gate with slow,medium and faster version.
In general fast version of gates are required for maximum speed of operation of a digital circuit, and slow version of gates are required to 
ensure no "hold" issues.This collection of logical modules form .lib

![WhatsApp Image 2023-09-02 at 17 41 52](https://github.com/pavithra7369/asic/assets/143084423/1bab7205-351f-48d9-85ec-84f70c8a9a4e)

**-->Faster cells vs Slower cell**, faster calls require more silicon area and power but they have less delay, slower cells require less silicon area and power but delay is comparitively more. Faster cells have wider transistors when compared to slower cells.

**-->Selection of cell**
We'll need to guide the Synthesizer to choose the flavour of cells that is optimum for implementation of logic circuit.More use of faster cells leads to more power consumption and silicon area and hold time violations may occur. More use of slower cells may make the circuit sluggish and may not meet the required performance.
So, the guidance offfered to synthesizer is "constraints"

![WhatsApp Image 2023-09-02 at 17 44 10](https://github.com/pavithra7369/asic/assets/143084423/963b38ca-3b0c-4570-b652-fb0ce33825d8)

+The synthesis process,first synthtical check is performed and then design is mapped.*

# Invoking Yosys 

> read_liberty -lib /path to .lib file    
*It reads all the components in the .lib file*

> read_verilog good_mux.v   
*This will read the desgn verilog file*

![WhatsApp Image 2023-09-02 at 17 51 40](https://github.com/pavithra7369/asic/assets/143084423/b0ce7301-3007-47b8-a480-182030b2df60)

> synth -top good_mux    
*synthsesizes the design*

![WhatsApp Image 2023-09-02 at 17 54 01](https://github.com/pavithra7369/asic/assets/143084423/ebbf93c5-eb31-427d-b99d-60e83b117e17)

![WhatsApp Image 2023-09-02 at 17 55 29](https://github.com/pavithra7369/asic/assets/143084423/58e64428-4511-4b21-9b31-9fff3e6b96b4)

> abc -liberty /path to .lib file 
*this command generates the netlist file based on .lib file*

![WhatsApp Image 2023-09-02 at 17 58 52](https://github.com/pavithra7369/asic/assets/143084423/52a3ca14-8519-4dcc-bcb7-616dc622a687)

>show 
*to see the synthsized output*

![WhatsApp Image 2023-09-02 at 18 00 10](https://github.com/pavithra7369/asic/assets/143084423/01f0240e-3397-41ed-9607-2f30f85aeb41)

*The synthesised output*

 ![WhatsApp Image 2023-09-02 at 18 07 42](https://github.com/pavithra7369/asic/assets/143084423/787c7a51-cc1c-4f65-82dd-93eaba24766a)
 
> write_verilog good_mux_netlist.v
  * To write the netlist*
   
> !gvim good_mux_netlist.v
*to extract the structue of file*

![WhatsApp Image 2023-09-02 at 18 13 01](https://github.com/pavithra7369/asic/assets/143084423/55d90739-f6dc-4967-9a50-068965a5e167)

![WhatsApp Image 2023-09-02 at 18 25 03](https://github.com/pavithra7369/asic/assets/143084423/0cdec9d7-089a-49f7-904f-a95a78bacfea)

*To get the netlist in a simple way switch to commands below*
> write_verilog -noattr good_mux_netlist.v
 >!gvim good_mux_netlist.v

![WhatsApp Image 2023-09-02 at 18 27 58](https://github.com/pavithra7369/asic/assets/143084423/2d62b0ed-9192-4699-b355-4301ac24fe3d)

 </details>
<details>
<summary>	DAY2 TIMING LIBS, HIERARCHIAL, FLAT SYNTHESIS, EFFICIENT FLOP CODING STYLES </summary>
+ Introduction to timing dot libs
Command to extract .lib
> gvim /path

![WhatsApp Image 2023-09-02 at 19 35 04](https://github.com/pavithra7369/asic/assets/143084423/af63bcbd-49eb-4ded-a3f3-e0ffe02a2c0d)

![WhatsApp Image 2023-09-02 at 19 35 04](https://github.com/pavithra7369/asic/assets/143084423/d3f34acf-0bec-4b9f-8156-abf1b1f98544)

 if neede Use :syn off to remove the colour 
 
![WhatsApp Image 2023-09-02 at 19 37 49](https://github.com/pavithra7369/asic/assets/143084423/86e50b01-9f5a-4452-b560-178a2697a85c)

+ The first line represents the name of the library

+ PVT --> Process Voltage Temperature ,
  important for design to work . in the above library that is... sky130_fd_sc_hd__tt_025C_1v80

+ tt stands for typical process

+ 025c tands for temperature

+ 1v80stands for voltage

the command :/cell marks the main cells

![WhatsApp Image 2023-09-02 at 20 12 56](https://github.com/pavithra7369/asic/assets/143084423/1b7803b8-2380-418a-99ce-15d7fbbdee40)


+ what does the library contains?
here are some features:
different flavour of different cells and different flavour of same cells.
leakage_power
area number
power port information
each input pin information
transition and delay associated with the cell
timing information etc.

# **Lab hirearchial synthesis and flat synthesis**

     module sub_module2 (input a, input b, output y);
	assign y = a | b;
     endmodule

    module sub_module1 (input a, input b, output y);
	assign y = a&b;
    endmodule


    module multiple_modules (input a, input b, input c , output y);
    wire net1;
    sub_module1 u1(.a(a),.b(b),.y(net1));  //net1 = a&b
    sub_module2 u2(.a(net1),.b(c),.y(y));  //y = net1|c ,ie y = a&b + c;
    endmodule

+ command used for multiple modules are
  # Hierarchical Synthesis
> gvim multiple_modules.v

![WhatsApp Image 2023-09-02 at 21 20 24](https://github.com/pavithra7369/asic/assets/143084423/955f7671-b22c-43b2-9e0b-dc3751ad6c55)

![WhatsApp Image 2023-09-02 at 21 19 06](https://github.com/pavithra7369/asic/assets/143084423/1576f0b5-0914-42dd-baba-80b35f8de3b7)

Commands used:
> yosys --> to invoke yosys

> read_liberty -lib /path

> read_verilog multiple_modules.v

> synth -top multiple_modules

> abc -liberty /path

> show multiple_modules

![WhatsApp Image 2023-09-02 at 21 22 52](https://github.com/pavithra7369/asic/assets/143084423/c452a358-03d4-4019-9b0c-a9a1ad504969)

![WhatsApp Image 2023-09-02 at 21 23 54](https://github.com/pavithra7369/asic/assets/143084423/6c70307d-b199-4116-b4f4-b597b643e8f5)

![WhatsApp Image 2023-09-02 at 21 24 37](https://github.com/pavithra7369/asic/assets/143084423/e9af85dd-680b-47e1-a8f5-bbbdcec9b0d0)

![WhatsApp Image 2023-09-02 at 21 24 56](https://github.com/pavithra7369/asic/assets/143084423/f8072ea0-357e-48c1-abe8-5fdd17bc868f)

![WhatsApp Image 2023-09-02 at 21 27 10](https://github.com/pavithra7369/asic/assets/143084423/d5667545-6418-4d83-87dd-011450778192)

to view the netlist commands used:

> write_verilog -noattr multiple_modules_hier.v

> !gvim multiple_modules_hier.v

![WhatsApp Image 2023-09-02 at 21 31 24](https://github.com/pavithra7369/asic/assets/143084423/db26a7ac-ede1-4e79-953d-82ad20414139)

![WhatsApp Image 2023-09-02 at 21 31 35](https://github.com/pavithra7369/asic/assets/143084423/320d2ad9-3631-44e3-97a0-a9cff70f88ac)

![WhatsApp Image 2023-09-02 at 21 36 21](https://github.com/pavithra7369/asic/assets/143084423/aad97fa8-bbb5-4f07-90fa-e5f4e433ba0e)

![WhatsApp Image 2023-09-02 at 21 56 40](https://github.com/pavithra7369/asic/assets/143084423/b284ba9e-aa50-4dba-825f-9f866f30aa44)

# Flat Synthesis

> flatten
is the command to write flat netlist

![WhatsApp Image 2023-09-02 at 21 56 40](https://github.com/pavithra7369/asic/assets/143084423/2f22bb3f-23dd-41e0-9727-f0d9bbda25c8)

![WhatsApp Image 2023-09-02 at 21 31 24](https://github.com/pavithra7369/asic/assets/143084423/416151c6-b2ab-4de7-bcb1-a4427046eebb)

![WhatsApp Image 2023-09-02 at 21 31 35](https://github.com/pavithra7369/asic/assets/143084423/022bef66-4756-405e-bc36-aec074bc7a89)

+ the hirearchies of submodule1 and submodule2 are preserved

![WhatsApp Image 2023-09-02 at 21 36 21](https://github.com/pavithra7369/asic/assets/143084423/475aac57-4304-480c-9413-8d759b336673)

+ when we flatten a module we see the structure completely

To obtain only sub_module1 :
invoke yosys

> read_liberty -lib /path

> read_verilog multiple_modules.v

> synth -top <module1_name>

> abc -liberty /path

> show

![WhatsApp Image 2023-09-02 at 21 43 59](https://github.com/pavithra7369/asic/assets/143084423/5013a767-f40d-4dc3-b6f5-455af757e59f)

![WhatsApp Image 2023-09-02 at 21 44 13](https://github.com/pavithra7369/asic/assets/143084423/af8d9e14-1f8d-4319-9ac4-723c755e36b1)

the sub_module1 is shown below:

![WhatsApp Image 2023-09-02 at 21 44 26](https://github.com/pavithra7369/asic/assets/143084423/2d98b40a-4601-43ee-b070-e6b0c6245076)

->Reasons for using submodules
+ sub module level synthesis is used when we have multiple instance of same module

+ divide and conquer

  # **Various flop coding styles and optimization**
  
   + flip flops are sequencing elements, they distinguish the current token from the prrevious token or data,without flip flops the next token might catch up with previous token,garbling both. Thus flip flops are used to store the value of glitches.
   +  flip flops are edge triggered the output of the flop changes only on the edge of the clock,means if the input is glitching the output will be stable,meaning the stable output is given next combinational circuit then the output of the combinational circuit will also be stable.

** How to code the flip flops **
To initialize the flop ,there are control pins on the flop like reset or set

these reset and set can either be synchronous or asynchronous

+ **ASYNCHRONOUS**
> **asynchronous reset**:
 _module dff_asyncres_

    module dff_asyncres ( input clk ,  input async_reset , input d , output reg q );
    always @ (posedge clk , posedge async_reset)
    begin
	      if(async_reset)
		    q <= 1'b0;
	      else	
		     q <= d;
    end
    endmodule

![WhatsApp Image 2023-09-03 at 08 15 19](https://github.com/pavithra7369/asic/assets/143084423/fbf5252b-73b3-4e8b-b5eb-e5790c123b18)

![WhatsApp Image 2023-09-03 at 08 11 56](https://github.com/pavithra7369/asic/assets/143084423/3817902f-02c4-47a3-b236-2e3752a0e41b)

![WhatsApp Image 2023-09-02 at 19 35 18](https://github.com/pavithra7369/asic/assets/143084423/46d613fc-8538-4b99-92ce-bb275c89c963)

![WhatsApp Image 2023-09-02 at 22 34 45](https://github.com/pavithra7369/asic/assets/143084423/ebad393c-4f54-4ee5-9cce-449104973a01)

 > **asynchronous set:**
 _module dff_asyn_set_

    module module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
         always @ (posedge clk )
         begin
	           if (sync_reset)
		         q <= 1'b0;
	           else	
		         q <= d;
         end
         endmodule

![WhatsApp Image 2023-09-02 at 22 34 46](https://github.com/pavithra7369/asic/assets/143084423/109cde00-af5c-4593-81f7-198f1efdf654)

  ![WhatsApp Image 2023-09-02 at 22 34 44](https://github.com/pavithra7369/asic/assets/143084423/9b8b8b41-35c3-4200-8166-d8debcb114c7)

![WhatsApp Image 2023-09-02 at 22 34 47](https://github.com/pavithra7369/asic/assets/143084423/cc110b21-5562-4668-aee7-4fa5b80daeab)

![WhatsApp Image 2023-09-02 at 22 34 45](https://github.com/pavithra7369/asic/assets/143084423/0ddcb26f-0b49-4e94-9f2c-344f381f11b8)

+ **Synchronous**
  > **Synchronous reset*
  _module dff_syncres_
   
      module dff_syncres ( input clk , input async_reset , input sync_reset , input d , output reg q );
         always @ (posedge clk )
         begin
	    if (sync_reset)
		  q <= 1'b0;
	    else	
		  q <= d;
          end
      endmodule

![WhatsApp Image 2023-09-03 at 08 26 36](https://github.com/pavithra7369/asic/assets/143084423/9c40f5a7-8a11-47f6-ba27-d0deb084b14f)

![WhatsApp Image 2023-09-03 at 08 24 13](https://github.com/pavithra7369/asic/assets/143084423/0ae75cc3-c973-43ec-ab38-7b2b01170bf8)

![WhatsApp Image 2023-09-02 at 15 04 36](https://github.com/pavithra7369/asic/assets/143084423/8a25a483-a9dc-43df-a6b1-8fbf0f3ea6c1)

  ![WhatsApp Image 2023-09-02 at 15 04 36](https://github.com/pavithra7369/asic/assets/143084423/37f25efe-0b73-49b4-8b74-95d3e5a19ec8)

+ **module mul2**

      module mul2 (input [2:0] a, output [3:0] y);
      assign y = a * 2;
      endmodule

  ![WhatsApp Image 2023-09-03 at 08 38 11](https://github.com/pavithra7369/asic/assets/143084423/3dfd84a5-1a96-4c3f-b350-fe97122beadc)

![WhatsApp Image 2023-09-03 at 08 38 10](https://github.com/pavithra7369/asic/assets/143084423/94f44513-422b-4911-a373-09ade64fd2ad)

![WhatsApp Image 2023-09-03 at 08 38 07](https://github.com/pavithra7369/asic/assets/143084423/22338f65-18ff-4ddc-ae4d-2eaf7808d450)

![WhatsApp Image 2023-09-03 at 08 38 10](https://github.com/pavithra7369/asic/assets/143084423/235239e4-0898-4ae1-b13f-cf62105888e0)

  ![WhatsApp Image 2023-09-03 at 08 38 07](https://github.com/pavithra7369/asic/assets/143084423/83d9eb13-e747-44f8-9416-253e6fc9b613)

![WhatsApp Image 2023-09-03 at 08 38 12](https://github.com/pavithra7369/asic/assets/143084423/c954b288-fa48-42e4-afde-30e8eb5ced68)

![WhatsApp Image 2023-09-03 at 08 38 10](https://github.com/pavithra7369/asic/assets/143084423/3682e3ec-6924-444e-ac21-cef55a2dc33e)

+ **special case**
  in this case the realtion is  a*9=y
  
![WhatsApp Image 2023-09-03 at 08 38 08](https://github.com/pavithra7369/asic/assets/143084423/30b32cb9-d7b8-4f1b-a5df-1a639fc8f111)

![WhatsApp Image 2023-09-03 at 08 38 09](https://github.com/pavithra7369/asic/assets/143084423/99962e9e-9f36-4022-a178-0daad2dfc057)

![WhatsApp Image 2023-09-03 at 08 38 09](https://github.com/pavithra7369/asic/assets/143084423/93279214-b534-4d43-8d47-63898623731e)

![WhatsApp Image 2023-09-03 at 08 38 09](https://github.com/pavithra7369/asic/assets/143084423/6d4dc4d2-b0ab-4990-a43c-1c94420e0886)

![WhatsApp Image 2023-09-03 at 08 38 12](https://github.com/pavithra7369/asic/assets/143084423/fc723b4b-71dd-46ed-a758-857b88e7f477)


</details>
<details>
<summary> Day 3: COMBINATIONAL AND SEQUENTIAL OPTIMIZATIONS </summary>

 **Introduction to logic optimizations**
 
 > **Combinational logic optimization**
   > squeezing the logic to get most optimized logic-->area and power savings
   > constant propagation --> direct optimization
      > example:-
    ![WhatsApp Image 2023-09-03 at 09 05 19](https://github.com/pavithra7369/asic/assets/143084423/b2c845aa-04de-44d1-91cb-044f4d655201)
           In the above example if A is 0, we can effectively write th eentire logic circuit as inverter.This will directly reduce the number of 
           transistors required as  Y=(AB+C)' requires 8 transistors and a inverter circuit requires 2 MOS transistors, thus consuming less area and less 
           power.
   > boolean logic optimization --> using K-map
      > example:- 
   ![image](https://github.com/pavithra7369/asic/assets/143084423/076abf30-bf0e-4b72-b84d-94f863f356cb)
    As seen in the above example a boolean logic can be reduced, and thus the reduced equation requires less MOS transistors and less area and power 
    comparitively.

 > **Sequential logic optimizations**
   >  sequential constant propogation
       > example:-
        ![image](https://github.com/pavithra7369/asic/assets/143084423/79ad8b33-2f01-4d19-8af1-48c4e4e46b7b)
        in the above example, Y=1 irrespective of clock,reset,Q,A.
       > example:-
           ![image](https://github.com/pavithra7369/asic/assets/143084423/049c3feb-1aa9-4eed-83ea-6ad97eeb6fae)
         every flop with D input is not a sequential constant ,for clock to become sequential constant Q pin should always take constabt value.
    

   > Advanced optimization
     > state optimization - optimization of unused states
     > retiming -technique to improve performance of logic circuit
     > sequential logic cloning (floor plan Aware synthesis) - cloning is done when we are doing physical aware synthesis

**LAB- combinational logic optimizations**
command to do the optimizations is opt_clean -purge
1) opt_check

       module opt_check (input a , input b , output y);
       assign y = a?b:0;
       endmodule
   
![image](https://github.com/pavithra7369/asic/assets/143084423/913d45d0-faa7-456b-95b5-0473ca8a4738)

![image](https://github.com/pavithra7369/asic/assets/143084423/691c297a-44a0-4fcc-a2ce-5e7e0220dd44)

![image](https://github.com/pavithra7369/asic/assets/143084423/4ff3c139-73f5-44ab-a29d-5b3f239e45c5)

2)opt_check2
     
    module opt_check2 (input a , input b , output y);
     assign y = a?1:b;
    endmodule

![image](https://github.com/pavithra7369/asic/assets/143084423/83ebc849-703f-4723-94b6-8a0c6bb678bf)

![image](https://github.com/pavithra7369/asic/assets/143084423/09760d21-c3ff-4137-a742-41f7f74153d0)

 3)opt_check3
 
 ![WhatsApp Image 2023-09-03 at 11 34 52](https://github.com/pavithra7369/asic/assets/143084423/faba49c7-9b8f-46fe-848c-300eecf25fd8)

 ![WhatsApp Image 2023-09-03 at 11 36 59](https://github.com/pavithra7369/asic/assets/143084423/49b9f218-bb95-4b78-8631-92743c365c0a)

![WhatsApp Image 2023-09-03 at 11 38 09](https://github.com/pavithra7369/asic/assets/143084423/baed4345-4d79-4db4-80e1-c88aea63c2c3)

4)opt_check4

    module opt_check4 (input a , input b , input c , output y);
        assign y = a?(b?(a & c ):c):(!c);
    endmodule
![WhatsApp Image 2023-09-03 at 11 44 59](https://github.com/pavithra7369/asic/assets/143084423/0a5e5aec-ac76-478a-af0d-ce106174e8fd)

   ![WhatsApp Image 2023-09-03 at 11 46 05](https://github.com/pavithra7369/asic/assets/143084423/596be5b5-b3a2-475d-ac90-acd8d960fb2e)
 
![WhatsApp Image 2023-09-03 at 11 46 38](https://github.com/pavithra7369/asic/assets/143084423/5175d944-224b-4d42-bc85-23122880e0e6)

5)multiple_modules_opt

        module sub_module1(input a , input b , output y);
               assign y = a & b;
        endmodule

        module sub_module2(input a , input b , output y);
         assign y = a^b;
        endmodule

        module multiple_module_opt(input a , input b , input c , input d , output y);
        wire n1,n2,n3;
        sub_module1 U1 (.a(a) , .b(1'b1) , .y(n1));
        sub_module2 U2 (.a(n1), .b(1'b0) , .y(n2));
        sub_module2 U3 (.a(b), .b(d) , .y(n3));

        assign y = c | (b & n1); 
        endmodule
![image](https://github.com/pavithra7369/asic/assets/143084423/fb6b5007-7331-4525-9a0f-8c3d21ff134c)

![image](https://github.com/pavithra7369/asic/assets/143084423/705cc412-e1d0-4f0b-a4be-94ad27f720f1)

synthseis after command flatten

![image](https://github.com/pavithra7369/asic/assets/143084423/145b43a7-14d3-4d36-8ef8-1d93722339e9)


  6)multiple_module_opt2

                      module sub_module(input a , input b , output y);
 	                     assign y = a & b;
                      endmodule
 
                      module multiple_module_opt2(input a , input b , input c , input d , output y);
 	                    wire n1,n2,n3;
 	                    sub_module U1 (.a(a) , .b(1'b0) , .y(n1));
 	                    sub_module U2 (.a(b), .b(c) , .y(n2));
 	                    sub_module U3 (.a(n2), .b(d) , .y(n3));
 	                    sub_module U4 (.a(n3), .b(n1) , .y(y));
                      endmodule


![image](https://github.com/pavithra7369/asic/assets/143084423/3dd84fa7-8dd4-4ee4-909d-34fbb9514110)

synthesis after command flatten

![image](https://github.com/pavithra7369/asic/assets/143084423/29c59d52-4dae-47a6-8f78-a35b2dd41102)

     
   **LAB-sequential logic optimization**
   1)dff_const1
    Files are present in
    > ls dff*const

 ![WhatsApp Image 2023-09-03 at 10 20 01](https://github.com/pavithra7369/asic/assets/143084423/3929f6c1-6410-4153-b3c1-29b47b558c1c)

 ![WhatsApp Image 2023-09-03 at 10 18 48](https://github.com/pavithra7369/asic/assets/143084423/3eb60013-3e7e-4b7b-b1f3-45f03ef4b263)
 
![WhatsApp Image 2023-09-03 at 10 33 37](https://github.com/pavithra7369/asic/assets/143084423/6fc44c65-e9f8-41d1-a009-703db81738fa)

   ![WhatsApp Image 2023-09-03 at 10 28 12](https://github.com/pavithra7369/asic/assets/143084423/772b267f-7f78-4525-8d4a-1564e5ef82eb)
 
![WhatsApp Image 2023-09-03 at 10 29 57](https://github.com/pavithra7369/asic/assets/143084423/8fb9e666-1a9f-4bed-b3ae-e65780315ccb)

2)dff_const2
        
    module dff_const2(input clk, input reset, output reg q);
 	              always @(posedge clk, posedge reset)
 	              begin
 		         if(reset)
 			         q <= 1'b1;
 		         else
 			         q <= 1'b1;
 	               end
                endmodule
![WhatsApp Image 2023-09-03 at 10 38 47](https://github.com/pavithra7369/asic/assets/143084423/a99c6409-f870-49be-85c1-f26cd19c2b58)

![WhatsApp Image 2023-09-03 at 10 38 09](https://github.com/pavithra7369/asic/assets/143084423/46fd81d5-a295-477c-82ee-e615e448dd8a)

![WhatsApp Image 2023-09-03 at 10 35 03](https://github.com/pavithra7369/asic/assets/143084423/f2b0ccfc-68b4-4479-8b9c-4a0456a65573)

![WhatsApp Image 2023-09-03 at 10 41 18](https://github.com/pavithra7369/asic/assets/143084423/6fec596d-2071-47c0-a93b-94e5bf25d1c7)

![WhatsApp Image 2023-09-03 at 10 42 27](https://github.com/pavithra7369/asic/assets/143084423/377a97bc-2061-41b8-b732-0f3ed7aa8fb1)

3)dff_const3

    module dff_const3(input clk, input reset, output reg q);
 	reg q1;
 
 	always @(posedge clk, posedge reset)
 	begin
 		if(reset)
 		begin
 			q <= 1'b1;
 			q1 <= 1'b0;
 		end
 		else
 		begin
 			q1 <= 1'b1;
 			q <= q1;
 		end
 	end
 	endmodule

  ![WhatsApp Image 2023-09-03 at 11 00 52](https://github.com/pavithra7369/asic/assets/143084423/a44cde51-120f-40d0-96c8-b9c19e49f57f)

![WhatsApp Image 2023-09-03 at 11 04 30](https://github.com/pavithra7369/asic/assets/143084423/954687f0-6cc2-400f-8b5a-21931ce250ed)

![WhatsApp Image 2023-09-03 at 11 05 19](https://github.com/pavithra7369/asic/assets/143084423/44e7dae7-70d2-4a47-b9bb-fcc9afa2562d)

4)dff_const4
        
	module dff_const4(input clk, input reset, output reg q); reg q1;

 	always @(posedge clk, posedge reset)
 	begin
 		if(reset)
 		begin
 			q <= 1'b1;
 			q1 <= 1'b1;
 		end
 	else
 		begin
 			q1 <= 1'b1;
 			q <= q1;
 		end
 	end
 	endmodule
![WhatsApp Image 2023-09-03 at 11 10 04](https://github.com/pavithra7369/asic/assets/143084423/9840e1b3-5cee-470b-86de-026fb17e05a9)

![WhatsApp Image 2023-09-03 at 11 09 34](https://github.com/pavithra7369/asic/assets/143084423/8aaeaa50-c64e-4db7-b5f3-f87184b95d01)

![WhatsApp Image 2023-09-03 at 11 11 37](https://github.com/pavithra7369/asic/assets/143084423/e220a9d3-52d7-4c90-890b-e9b1c5496a86)

![WhatsApp Image 2023-09-03 at 11 12 11](https://github.com/pavithra7369/asic/assets/143084423/5986b0e1-1495-4bdd-8fbe-50077027d01e)

5)dff_const5

     module dff_const5(input clk, input reset, output reg q);
     reg q1;
    always @(posedge clk, posedge reset) 
    begin
    if(reset) begin q <= 1'b0; q1 <= 1'b0; 
    end 
    else 
    begin q1 <= 1'b1; q <= q1; 
    end
    end endmodule

![WhatsApp Image 2023-09-03 at 11 17 56](https://github.com/pavithra7369/asic/assets/143084423/f941d0be-6006-4374-bba7-077d72d49b8e)

![WhatsApp Image 2023-09-03 at 11 17 23](https://github.com/pavithra7369/asic/assets/143084423/a087a973-d4bb-4c26-a6fc-5142549493d9)

![WhatsApp Image 2023-09-03 at 11 19 10](https://github.com/pavithra7369/asic/assets/143084423/3de66b4e-f0ee-4b4b-911c-03176d5fe03d)

![WhatsApp Image 2023-09-03 at 11 20 26](https://github.com/pavithra7369/asic/assets/143084423/3fd6986e-e5a6-4bc4-9a74-2f47c279f3d3)

**Sequential optimizations for unused outputs**
1)counter_opt

 		module counter_opt (input clk , input reset , output q);
 		reg [2:0] count;
 		assign q = count[0];
 		always @(posedge clk ,posedge reset)
 		begin
 			if(reset)
 				count <= 3'b000;
 			else
 				count <= count + 1;
 		end
 		endmodule

   ![WhatsApp Image 2023-09-03 at 12 34 15](https://github.com/pavithra7369/asic/assets/143084423/55bb3c3d-aadf-4f89-ae8e-46d96135ff8f)

![WhatsApp Image 2023-09-03 at 12 33 24](https://github.com/pavithra7369/asic/assets/143084423/ddb0fe79-77a7-47f0-abd6-763966b44ea6)

![image](https://github.com/pavithra7369/asic/assets/143084423/50ad19a1-ac36-45c5-9249-22c1d5be4a8e)

![WhatsApp Image 2023-09-03 at 12 37 59](https://github.com/pavithra7369/asic/assets/143084423/1dbd3b08-a1a9-4a7e-83cf-20d173069e77)

![WhatsApp Image 2023-09-03 at 12 39 24](https://github.com/pavithra7369/asic/assets/143084423/dee2572d-8e38-439f-8053-ba0456a0a6b7)


2)module counter_opt2

 			module counter_opt (input clk , input reset , output q);
 					reg [2:0] count;
 					assign q = {count[2:0]==3'b100};
 					always @(posedge clk ,posedge reset)
 					begin
 					if(reset)
 						count <= 3'b000;
 					else
 						count <= count + 1;
 					end
 			endmodule

![image](https://github.com/pavithra7369/asic/assets/143084423/474e4c19-6e2c-4b82-9cf1-71370af00c71)

![image](https://github.com/pavithra7369/asic/assets/143084423/e4e9bfe1-077b-425f-889c-7828a9aba519)

</details>
<details> 
	<summary> Day 4:GLS,BLOCKING VS NON-BLOCKING AND SYNTHESIS-SIMULATION MISMATCCH </summary>

**GLS, Synthesis-Simulation mismatch and Blocking, Non-blocking statements**

+  What is GLS?

  Running the test bench with netlist as design under test
  netlist is logically same as RTL code,input and output in netlist and RTL code are same therefore nerlist will fit in the testbench


+ why GLS?

  verify the logical correctness of gesign after synthesis
  Ensuring the timing of the design is met, for this GLS need to be run with delay annotation.

+  GLS using IVERILOG

![image](https://github.com/pavithra7369/asic/assets/143084423/3cbf6dd3-50c5-4f10-9057-49f7a2293e53)

> The design in the above block contains netlist,it has standard cells, but these standarrd cell's meaning should be given to the tool, so we give gate level verilog modules.
> we validate the functionality of netlist, for synthesis and simulation mismatches.

+ Synthesis Ans Simulation Mismatch
  
  missing sensitivity list
  blocking vs Non blocking Assignments
  Non standard verilog code
Example:

	  module mux(
	  input i0,input i1,input sel,ouput reg y);
       always@(sel)
	  begin
	  if(sel)
	       y=i1;
	  else
	       y=i0;
	  end 
	  endmodule
 +  simulator looks for change in input only then there is change in input
+ Blocking and non blocking statements
 > Blocking (=)
   + executes the statements in the order it is written
   + so the first statement is evaluated beforee the second statement


>  Non-blocking (<=)
   + executes parallely .order doesnot matches
   + executes all the RHS when always block is entered and assigns to LHS.


+ Caveats with Blocking Statements
//In this case q=q0 and then q0=d
 
      module code (input clk,input reset,input d,output regd);
      reg q0;
      always@(posedge clk,posedge reset)
      begin
       if(reset)
        begin q0=1'b0; q=1'b0;
       end
      else 
      begin
      q=q0
      q0=d;
      end 
      endmodule
//In this case the order is changed which leads to wrong output, This is where synthesis mismatch occurs
     
	 module code (input clk,input reset,input d,output regd);
	  reg q0;
	  always@(posedge clk,posedge reset)
	  begin
	  if(reset)
	  begin
	   q0=1'b0;
	   q=1'b0;
	  end
	  else
	  begin
	   q0=d;
	   q=q0;
	  end 
	  endmodule
   
  **Labs-GLS and Synthesis-Simulation Mismatch**

    module ternary_operator_mux (input i0 , input i1 , input sel , output y);
		assign y = sel?i1:i0;
	endmodule

 ![WhatsApp Image 2023-09-03 at 13 59 30](https://github.com/pavithra7369/asic/assets/143084423/b0b027a7-0d3d-4180-9310-de9aa2d9ad93)

  ![WhatsApp Image 2023-09-03 at 13 58 51](https://github.com/pavithra7369/asic/assets/143084423/024efa71-a572-4eec-ae99-cf8eabc01f73)

![WhatsApp Image 2023-09-03 at 14 01 27](https://github.com/pavithra7369/asic/assets/143084423/bfb8448b-a5f1-4506-ae20-b44cd1e6323a)

![WhatsApp Image 2023-09-03 at 14 01 00](https://github.com/pavithra7369/asic/assets/143084423/d817c9e7-c46f-4f40-b5e1-781cf76bd704)

+ Netlist simulation
  
 ![WhatsApp Image 2023-09-03 at 14 13 27](https://github.com/pavithra7369/asic/assets/143084423/f090cb3e-feb2-45d0-bb68-31c7e47038fe)

![WhatsApp Image 2023-09-03 at 14 14 03](https://github.com/pavithra7369/asic/assets/143084423/a3d80f1b-b503-4222-8c31-59cdd3767585)

Example2: this is going show the simulation synthesis mismatch


	module bad_mux (input i0 , input i1 , input sel , output reg y);
		always @ (sel)
		begin
			if(sel)
				y <= i1;
			else 
				y <= i0;
		end
	endmodule

 ![WhatsApp Image 2023-09-03 at 14 18 55](https://github.com/pavithra7369/asic/assets/143084423/4ff06f77-cf12-453e-8451-08d80ab2e94e)

![WhatsApp Image 2023-09-03 at 14 18 29](https://github.com/pavithra7369/asic/assets/143084423/4e2b6e04-e222-40c2-a15c-c9ae261305aa)

![WhatsApp Image 2023-09-03 at 14 20 41](https://github.com/pavithra7369/asic/assets/143084423/2ec21fe3-1580-4039-beab-3b0760092233)

![WhatsApp Image 2023-09-03 at 14 21 16](https://github.com/pavithra7369/asic/assets/143084423/ebe573e3-1714-4412-806a-17310c08ccb2)

In the below picture, we can see that, sel=0, so the output y=i0, and i0 in this case is 1 but we are getting output where y=0.This is due to synthesis simulation mismatch.

![WhatsApp Image 2023-09-03 at 14 27 56](https://github.com/pavithra7369/asic/assets/143084423/ec31f971-30c9-46ae-aebc-7b531ec160e4)

**Lab-GLS and Synthesis-Simulation Mismatch for blocking statement**

example1

    module blocking_caveat (input a , input b , input c, output reg d);
    reg x; 
    always @ (*)
    begin d = x & c;
    x = a | b; 
    end
    endmodule
    
simulation

 ![WhatsApp Image 2023-09-03 at 14 35 30](https://github.com/pavithra7369/asic/assets/143084423/f125c12f-0139-4ec6-b6e1-2690bd1c37c9)
   
![WhatsApp Image 2023-09-03 at 14 36 36](https://github.com/pavithra7369/asic/assets/143084423/53291e85-74ee-4d9e-aaa8-9892dadec4cc)

synthesis

![WhatsApp Image 2023-09-03 at 14 42 18](https://github.com/pavithra7369/asic/assets/143084423/cbf6ce59-dfd8-47a4-9cf3-32e634b90867)

![WhatsApp Image 2023-09-03 at 14 42 51](https://github.com/pavithra7369/asic/assets/143084423/fef9d970-6da6-4c88-a485-87948408e600)

In the below picture we can see that when a is low b is low the ouput is low,because it is taking instantenous value, this is called synthesis mismatch due to blocking statement(=)

![WhatsApp Image 2023-09-03 at 14 40 35](https://github.com/pavithra7369/asic/assets/143084423/a514d93b-3abc-4049-981a-6c13adbc83a1)

</details>
<details>
	 <summary> WEEK3 DAY 1:Inceptioon ofopen-source EDDA,openLANE and Sky130PDK </summary>
  

