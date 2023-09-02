## PES ASIC CLASS
# DAY1
Basic Definition: An Instruction Set Architecture (ISA) is part of the abstract model of a computer that defines how the CPU is controlled by the software. The ISA acts as an interface between the hardware and the software, specifying both what the processor is capable of doing as well as how it gets done.
RISC-V is an open-source instruction set architecture used to develop custom processors for a variety of applications, from embedded designs to supercomputers. From Apps to Hardware
Applications: Applications, also known as software applications or simply apps, are programs or software designed to perform specific tasks or functions for end-users. Examples include word processors, web browsers, and games
System Software: System software refers to a collection of programs and utilities that manage and control a computer system's hardware and provide services to other software applications. It includes the operating system, device drivers, and system utilities.
Compiler: A compiler is a software tool that translates high-level programming code (source code) written by humans into machine code or intermediate code that can be executed directly by a computer's hardware or by a virtual machine.
Assembler: An assembler is a program or tool that translates assembly language code, a low-level human-readable representation of machine code instructions, into machine code that can be executed by a computer's CPU.
RTL (Register-Transfer Level): RTL, or Register-Transfer Level, is a level of hardware description language used to model the behavior of digital circuits at a low level of abstraction. It specifies how data moves between registers and how logic operations are performed.
Hardware: Hardware refers to the physical components of a computer system, including the CPU, memory, storage devices, input/output devices, and other electronic and mechanical components. It is the tangible, physical part of a computer system

LABWORK FOR RISC TOOLCHAIN
1a#Writing C program using leaf header to find sum of integers from1 to 1 to n
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


Application binary interface(ABI)
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


## DAY 1 RTL DESIGN USING VERILOG WITH SKY130 TECHNOLOGY
# **Introduction to open-source simulator iverilog**
-->Simulator
   *simulator is a tool used for checking the design
   *RTL design is checked for adherence to the spec by simulating the design
   *Simulator is a tool used for simulating the design(iverilog is the simulator here)
-->Design
   *Design is the actual verilog code or set of verilog codes which has the intended functionality to meet with required specifications
-->Testbench
     *Testbench is the setup to apply stimulus(test_vectors) to the design to check it's functionality and match it to spec
-->How Simulator Works?
   *Simulator looks for the change on input signals
   *Upon change to the input the output will be evaluated,no change in input-no change in output
   *Simulator is looking for change in the values of input.
   
   ![WhatsApp Image 2023-09-02 at 16 29 45](https://github.com/pavithra7369/asic/assets/143084423/621d6e08-28d5-4e9e-9b27-99340d98eb39)

 -->iverilog based simulation flow
 ![WhatsApp Image 2023-09-02 at 16 29 46](https://github.com/pavithra7369/asic/assets/143084423/5f5a8767-af09-4633-8363-4813dfe20400)
  VCD file-value change dump format, vcd file is used because we are looking for changes in values
  gtkwave-is used for viewing the waveform
  
  examples with testbenches
  ![WhatsApp Image 2023-09-02 at 16 43 05](https://github.com/pavithra7369/asic/assets/143084423/f358224b-06af-4b64-9e21-846920cab8aa)
 // module good_mux (input i0 , input i1 , input sel , output reg y); 
	always @ (*)
	begin
		if(sel)
		y <= i1;
		else 
		y <= i0;
	end
endmodule


`timescale 1ns / 1ps
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

--> commands used are
``` iverilog filename.v tb_filename.v
```
```./a.out      #this cwhen executed, this dumps the vcd file
```
``` gtkwave tb_filename.vcd
```
![WhatsApp Image 2023-09-02 at 16 47 01](https://github.com/pavithra7369/asic/assets/143084423/c70b5b97-cbee-4720-8392-00adf48a804e)
![WhatsApp Image 2023-09-02 at 16 47 01](https://github.com/pavithra7369/asic/assets/143084423/551e9ff7-7e4e-4988-aa50-6d93d5e0d9a2)

















