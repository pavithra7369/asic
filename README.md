
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













