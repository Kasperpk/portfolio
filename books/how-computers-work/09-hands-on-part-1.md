Alongside the study of computing systems it's interesting to also get some hands-on exercises. Myself i have tried my way with some different ones, one being assembling some of the digital building blocks using a special type of language called HDL, which stands for hardware declaration language. Implementing the chips AND, OR and NOT is perhaps the most fundamental ones. The first elementary logic gate we can create is the AND gate. The input/output relationship might be displayed in a truth table

| a   | b   | out |
| --- | --- | --- |
| 0   | 0   | 0   |
| 1   | 0   | 0   |
| 0   | 1   | 0   |
| 1   | 1   | 1   |
We can write that programmatically using the verilog package which can be installed to your PC and then used to compile these .sv files generated as a result.

```
module and_gate (
    input  logic a,
    input  logic b,
    output logic y
);
    assign y = a & b;
    
endmodule
```

Computers are built from these very elementary gates which in turn are built on the smaller transistor devices. By combining them we can construct more sophisticated gate logic such as the multiplexer or MUX gates which are essential for the behavior of computers. The multiplexer is capable of selecting one of several inputs to propogate to an output by using one or more selector bits. The number of selector bits depends on the number of inputs to select from. Let's say that $n$ is the numebr of inputs then we need $log_2(n)$ selector bits. As described in the sections, there are several use cases for this technology among them routing, data selection and control units.   

| S   | A   | B   | Y   |
| --- | --- | --- | --- |
| 0   | 0   | X   | 0   |
| 0   | 1   | X   | 1   |
| 1   | X   | 0   | 0   |
| 1   | X   | 1   | 1   |
The following boolean equation describes this truth table $y=(¬sel∧a)∨(sel∧b)$.  In verilog we can design this chip in a compact way using the operators shown here below, which could be implemented using other gates. 

```
module mux2_gate (

    input  logic s,
    input  logic a,
    input  logic b,
    output logic y
);
    assign y = (a & ~s) | (b & s);
    
endmodule
```



| in  | sel | a   | b   |
| --- | --- | --- | --- |
| 0   | 0   | 0   | 0   |
| 1   | 0   | 1   | 0   |
| 0   | 1   | 0   | 0   |
| 1   | 1   | 0   | 1   |






The **DMUX** gate or demultiplexer, is similarly a core chip that helps us construct RAM units and ALU functionality. The demultiplexer chip does the opposite of the multiplexer as it routes an input bit to one or more output places depending on a selector.  


(a AND NOT sel OR (b AND sel)
Only using Nand gates we can construct the following combinational logic that performs the desired requirements. 

Similarly, a demultiplexer can be designed as multi-bit by routing its single n-bit to one of its m n-bit outputs. The selection is specified by a set of k selection bits, where k = log2m. Here the input can be routed to one of 4 outputs based on the 2 selection bits. 

The *demultiplexer* is some what diffucult to grasp, but imagine that you first select between a high or low part using one of the selector bits, then from that selection you can use another demultiplexer to select between the next level. One way to show it is to use a sketch like this and try to follow each line and convince oneself that the input bit (F) will indeed route to the correct output line based on the selectors. 

This solution below really do use a *divide and conquer* strategy as we break up the problem by starting using the least significant bit of the selector to evaluate which route to take first. 
CHIP DMux4Way {
    IN in, sel[2];
    OUT a, b, c, d;
    PARTS:
    // First level: MSB (sel[0]) — split in half
    DMux(in=in, sel=sel[1], a=hi0, b=hi1);
    // Second level: LSB (sel[1]) — split each half
    DMux(in=hi0, sel=sel[0], a=a, b=b);
    DMux(in=hi1, sel=sel[0], a=c, b=d);
}


A single bit is not giving many options for computer architects to create instructions and represent information digitally, therefore computer hardware is often designed to process multi-bit values such as bitwise AND OR function on 16, 32 or 64 bits. Values in multi bit processing can be indexed in order to access individual values such as out[3]=in[5], which sets the 3rd bit of the out to the value of the 5th bit of in. I will not cover all the API-Style descriptions here of multibit gates, but the AND gate is provided below. 

Here is the implementation for the *And16*
CHIP And16

 {
    IN a[16], b[16];
    OUT out[16];
    PARTS:
    And(a=a[0], b=b[0], out=out[0]);
    And(a=a[1], b=b[1], out=out[1]);
    And(a=a[2], b=b[2], out=out[2]);
    And(a=a[3], b=b[3], out=out[3]);
    And(a=a[4], b=b[4], out=out[4]);
    And(a=a[5], b=b[5], out=out[5]);
    And(a=a[6], b=b[6], out=out[6]);
    And(a=a[7], b=b[7], out=out[7]);
    And(a=a[8], b=b[8], out=out[8]);
    And(a=a[9], b=b[9], out=out[9]);
    And(a=a[10], b=b[10], out=out[10]);
    And(a=a[11], b=b[11], out=out[11]);
    And(a=a[12], b=b[12], out=out[12]);
    And(a=a[13], b=b[13], out=out[13]);
    And(a=a[14], b=b[14], out=out[14]);
    And(a=a[15], b=b[15], out=out[15]);
}

*16-bit OR*
Very similar to the And16 the Or16 performs bitwise OR comparisons 

CHIP Or16

 {
    IN a[16], b[16];
    OUT out[16];
    PARTS:
    Or(a=a[0], b=b[0], out=out[0]);
    Or(a=a[1], b=b[1], out=out[1]);
    Or(a=a[2], b=b[2], out=out[2]);
    Or(a=a[3], b=b[3], out=out[3]);
    Or(a=a[4], b=b[4], out=out[4]);
    Or(a=a[5], b=b[5], out=out[5]);
    Or(a=a[6], b=b[6], out=out[6]);
    Or(a=a[7], b=b[7], out=out[7]);
    Or(a=a[8], b=b[8], out=out[8]);
    Or(a=a[9], b=b[9], out=out[9]);
    Or(a=a[10], b=b[10], out=out[10]);
    Or(a=a[11], b=b[11], out=out[11]);
    Or(a=a[12], b=b[12], out=out[12]);
    Or(a=a[13], b=b[13], out=out[13]);
    Or(a=a[14], b=b[14], out=out[14]);
    Or(a=a[15], b=b[15], out=out[15]);
}

In the test script it performs Or operations on various inputs such as the one here below 
These are the decimal equivalents of the numbers 4660 and -26506 and the Or operation gives -25994. This is because the **MSB** is a 1, and is used to represent a negative number. 

*Not 16*
CHIP Not16
 {
    IN in[16];
    OUT out[16];
    PARTS:
    Not(in=in[0],  out=out[0]);
    Not(in=in[1],  out=out[1]);
    Not(in=in[2],  out=out[2]);
    Not(in=in[3],  out=out[3]);
    Not(in=in[4],  out=out[4]);
    Not(in=in[5],  out=out[5]);
    Not(in=in[6],  out=out[6]);
    Not(in=in[7],  out=out[7]);
    Not(in=in[8],  out=out[8]);
    Not(in=in[9],  out=out[9]);
    Not(in=in[10], out=out[10]);
    Not(in=in[11], out=out[11]);
    Not(in=in[12], out=out[12]);
    Not(in=in[13], out=out[13]);
    Not(in=in[14], out=out[14]);
    Not(in=in[15], out=out[15]);
}

*Mux16*
The Mux16 chip is going to evaluate 16 bits each using a single MUX chip. 
CHIP Mux16
 {
    IN sel, a[16], b[16];
    OUT out[16];
    PARTS:
    Mux(a=a[0], b=b[0], sel=sel, out=out[0]);  
    Mux(a=a[1], b=b[1], sel=sel, out=out[1]);
    Mux(a=a[2], b=b[2], sel=sel, out=out[2]);
    Mux(a=a[3], b=b[3], sel=sel, out=out[3]);
    Mux(a=a[4], b=b[4], sel=sel, out=out[4]);
    Mux(a=a[5], b=b[5], sel=sel, out=out[5]);
    Mux(a=a[6], b=b[6], sel=sel, out=out[6]);
    Mux(a=a[7], b=b[7], sel=sel, out=out[7]);
    Mux(a=a[8], b=b[8], sel=sel, out=out[8]);
    Mux(a=a[9], b=b[9], sel=sel, out=out[9]);
    Mux(a=a[10], b=b[10], sel=sel, out=out[10]);
    Mux(a=a[11], b=b[11], sel=sel, out=out[11]);
    Mux(a=a[12], b=b[12], sel=sel, out=out[12]);
    Mux(a=a[13], b=b[13], sel=sel, out=out[13]);
    Mux(a=a[14], b=b[14], sel=sel, out=out[14]);
    Mux(a=a[15], b=b[15], sel=sel, out=out[15]);
}

*Mux4Way16*
If we extend the multiplexer to select among 4 different inputs using two input select bits. 

*Mux8Way16*
The idea behind extending a multiplexer is to use the simpler building block Mux16 that evaluates two 16-bit inputs and selects one of them. So in an 8-way multiplexer you first evaluate a|b, then c|d, e|f, g|h. It also takes a selector input which is 4-bits wide. The first index is used as input in all of the first levels of multiplexers. It's a little bit more difficult to follow and understand the logic in the extended version here. Imagine sel[1]:sel3 is 0. Then at the first level, a,c,e and g inputs are selected. In the next level a and e are chosen. Then in the final layer a is chosen over e, so the final output ends up being the 16 bits in the a input. In order to select b, the inputs have to be 100, to chose c it has to be 0,1,0. 

*Things that were hard in the first part*

* The design of 8 and 4 way demux and mux
* Getting the hang of translating truth tables to logic designs.
* That demux are used for networking, so that a single cable can route signals to different places - in general fiber optic cables can distinguish between many signals using **wavelength-division multiplexing**
I think i got a hang of it more now - i obviously could design more chips now to get even better at it - but it's interesting. 


**Implementing memory chips in HDL**
Up until now we have built and studied chipsets that processes some inputs oblivious to time, they compute with the only delay being the "time it takes for the inner chip-parts to complete the computation". The modern all-purpose computer relies on chips that are able to hold or "contain" digital information. This is needed for example for execution programs that use "variables, arrays and objects - abstractions that persist data over time." 

This capability needs to be implemented in hardware, something that is not trivial. The fundamental building block for sequential units are *data flip-flop* (DFF), a time-dependent chip that can store states the states 1,0. 


Figure 3.1 from the book shows the memory hierarchy which starts from the DFF and can be transformed into the 1-bit register, to multibit registers and so on. Us humans are able to remember a word such as *dog.* This is something we normally take for granted, a reality that computer architects and engineers have had to construct from gate logic. 


The figure above 3.2 from the book explains how time is represented in digital systems as cycles. These are discrete time units unlike the more continuous that physicists and philosophers study. Synchronising operations are an important design challenge and treating time discretely allows the computation to finish before a new cycle is started. "*Cycle length* is one of the most important design parameters in a hardware platform" because if we need to ensure correct synchronisation then the cycle length must be long enough to "cover the maximum time delays that can occur in the system". 

With the nano-scale of hardware, we're now able to have cycles down to billionth of a second. The cycles are implemented as a oscillator that "alternates continuously between two phases labeled 0-1, *low-high* or *tick-tock*" A master clock is connected to all the subsequent memory units and ultimately propogate signals all the way down to the single DFFs and "ensure that the chip will commit to a new state, and output it, only at the end of the clock cycle."


The authors provide an example of how a calculation like x + y in the ALU may operate on a nearby register and a remote RAM address. Since it will take longer for the input coming from the remote RAM address to arrive, the ALU will output a wrong result for some time. As data flows from RAM to the ALU via clocks and register mechanisms, hardware designers need to built the clock such that "it is slightly longer than the time it takes for a bit to travel from the longest distance from one chip to another, plus the time it takes to complete the most time-consuming within-chip calculation". 
Constructing memory is a critical tasks for computer engineers. Knowing how to maintain a state is important for many applications that exist on computers today. We remember the word dog at time t, because we remembered it at time t-1, all the way back to the point of time when we first committed it to memory. In order to develop this temporal ability to maintain state, we must extend our computer architecture with a time dimension. Memory chips can store information that represents numbers, instructions or any other analog concept. It is what allows us to set a variable like x to “contain” a certain value and persist until we set it to another value. Memory chips differ from the ones built so far that culminated into the ALU, as they were combinational and time independent. *Sequential* chips depend not only on the inputs in the current time but also on inputs and outputs that have been processed previously.  

The memory chips that are typically used in computer architectures are
- data flip-flops (DFFs)
- registers (based on DFFs)
- Ram devices (based on registers)
- counters (based on registers)
From the simplest data flip-flops chips we can build registrs, RAM devices and counters and with the arithmetic units created earlier “comprise all the chips needed for building a complete, general-purpose computer system. 

**The single bit memory (flip-flop)**
To begin with we will built a titime-dependent logic gate that can flip and flop between two stable states: 0 and 1. Memory chips are designed to “remember”, or store information over time. The low-level devices that facilitate this storage abstraction are named flip-flop gates, of which there are several variants. In Nand to Tetris we use a variant named data flip-flop, or DFF, whose interface includes a single-bit data input and a single-bit data output

Above here is an example of a DFF chip. It takes a single bit data input and a single data bit is outputted. It has an additional input from the master clock’s signal. All DFFs in the system are connected to the master clock which forms a “huge distributed chorus line.”  At the end of each clock cycle, outputs of all the DFFs in the computer commit to their inputs from the previous cycle. At all other times the DFFs are latched, meaning that changes in their inputs have no immediate effect on their outputs.

**Adding a load signal**
Consider storing a single bit, this takes a data input and a load signal that enables the register for writes. What we can see at time 1, the input is set to 1 and the load input is also set to 1, at the next clock cycle that means that output is set to 1. The next 3 cycles latch the output to 1 even when the data input is set to 0, because the load input is turned off. At cycle 3 the load input is again turned on and the output goes to 0 in cycle 3+1. 



 The single bit memory have the following input/outputs

| in  | load | out |
| --- | ---- | --- |
| 0   | 0    | out |
| 1   | 0    | out |
| 0   | 1    | 0   |
| 1   | 1    | 1   |
`CHIP Bit {`
    `IN in, load;`
    `OUT out;`
    `PARTS:`
    `DFF(in=next, out=dfout);`
    `Mux(a=dfout, b=in, sel=load, out=next);`
    `DFF(in=next, out=out);`
`}`
To implement a single memory i 
1) used a DFF chip to hold a value which could be used as the alternative output from the multiplexer. 
2) Used a multiplexer to choose between the input and previous output
3) A third DFF chip to hold the value outputtet from the multiplexer. 

**Counters**
Each computer have a counter, particularly a program counter which can increment the instructions such that programs can execute properly. It was a little bit more tricky to implement this, i should perhaps have looked at the HDL documentation, i didn't know that an register chip could have two output lines. 
`CHIP PC {`
    `IN in[16], reset, load, inc;`
    `OUT out[16];`
    `PARTS:`
    `Mux8Way16(a=DFF16out, b=DFF16outPlus1, c=in, d=in, e=false, f=false, g=false, h=false, sel[2]=reset,sel[1]=load, sel[0]=inc, out=DFF16in);`
    `Inc16(in=DFF16out, out=DFF16outPlus1);`
    `Register(in=DFF16in, load=true, out=DFF16out, out=out);`
`}`

**Registers**
Implementing a register is done by introducing a multiplexer. The implementation seen at the bottom first shows a invalid design (left), which doesn't have a load bit which the register interface requires. Secondly it does not come with the option to tell the DFF chip part when to draw its input from the in wire and when to draw it from the incoming out value. To create a correct design we need a multiplexer. The design can be seen on the right, the load bit can be funneled to the select bit of the inner multiplexer. If we set this bit to the value 1, the input from the in wire is propagated to the DFF, otherwise it is the output from the previous output. There is a small time delay as the loop goes through a DFF gate. Each component that builds on these smaller single bit registers, will become time-dependent chips such as the multibit registers and RAM we built from them. 

To implement the register we use the single bit memory cells and sequence them such that we can store sequences of bits or data words - here 16-bits in a single register. 

CHIP Register {

    IN in[16], load;
    OUT out[16];
    PARTS:
    Bit(in=in[0], load=load, out=out[0]);
    Bit(in=in[1], load=load, out=out[1]);
    Bit(in=in[2], load=load, out=out[2]);
    Bit(in=in[3], load=load, out=out[3]);
    Bit(in=in[4], load=load, out=out[4]);
    Bit(in=in[5], load=load, out=out[5]);
    Bit(in=in[6], load=load, out=out[6]);
    Bit(in=in[7], load=load, out=out[7]);
    Bit(in=in[8], load=load, out=out[8]);
    Bit(in=in[9], load=load, out=out[9]);
    Bit(in=in[10], load=load, out=out[10]);
    Bit(in=in[11], load=load, out=out[11]);
    Bit(in=in[12], load=load, out=out[12]);
    Bit(in=in[13], load=load, out=out[13]);
    Bit(in=in[14], load=load, out=out[14]);
    Bit(in=in[15], load=load, out=out[15]);
}

**Random access memory**
RAM is a collection or aggregate of *n* Register chips. By specifying a particular address (a number between 0 to n-1), each register in the RAM can be selected and made available for read/write operations. We can access any part of the RAM for example m by setting the address input to m and set the input to v, and assert the load bit. 

How do we realize the chips that we introduced the interface of so far? The DFF or “flip flop” can be implemented in several ways, including one that uses Nand gates only. The problem is that they require us to model feedback loops in the hardware simulator. The hardware simulator comes with a built-in DFF implementation that allows us to abstract away the complexity. 
The Hack hardware platform requires a RAM device of 16K, 16-bit registers. Each RAM chip has n registers, and the width of its address input is k=log_2n bits.  


A **RAM8** chip features 8 registers, where each RAM8’s 3 bit address input to a value between 0 and 7. The act of reading the value of a selected register can be described as follows.
1. Given some address (0-7) we access the RAM almost instantaneously because we can use a multiplexer to select a single value from the address inputs.
2. Writing a value to a selected register, we set the load value to 1, and a 16-bit in value
Larger RAMs can be built from this smaller RAM8, we just need a larger amount of bits to select the address. 

The HDL implementation shows how the demultiplexer enables us to select between the 8 register arrays. A multiplexer on the other end then can use the same addresss to choose the output among those 8 registers.  
`CHIP RAM8 {`
    `IN in[16], load, address[3];`
    `OUT out[16];`
    `PARTS:`
    `DMux8Way(in=load, sel=address, a=load0, b=load1, c=load2, d=load3, e=load4, f=load5, g=load6, h=load7);`
    `Register(in=in, load=load0, out=out0);`
    `Register(in=in, load=load1, out=out1);`
    `Register(in=in, load=load2, out=out2);`
    `Register(in=in, load=load3, out=out3);`
    `Register(in=in, load=load4, out=out4);`
    `Register(in=in, load=load5, out=out5);`
    `Register(in=in, load=load6, out=out6);`
    `Register(in=in, load=load7, out=out7);`
    `Mux8Way16(a=out0, b=out1, c=out2, d=out3, e=out4, f=out5, g=out6, h=out7, sel=address, out=out);`
`}`

The **RAM64** does look a lot like the RAM8. The difference is that it consist of 8 RAM8 sticks instead of individual registers. Now this obviously require a wider address namely log<sub>2</sub> n. This means an address width of 6. 
1) Use the first 3 bits of the address input to select among the 8 RAM8 modules. 
2) Use the remaining 3 bits and pass that to the RAM8 modules and they will by themselves select which individual register to load to. 
`CHIP RAM64 {`
    `IN in[16], load, address[6];`
    `OUT out[16];`
    `PARTS:`
    `DMux8Way(in=load, sel=address[0..2], a=load0, b=load1, c=load2, d=load3, e=load4, f=load5, g=load6, h=load7);`
    `RAM8(in=in, load=load0, address=address[3..5], out=out0);`
    `RAM8(in=in, load=load1, address=address[3..5], out=out1);`
    `RAM8(in=in, load=load2, address=address[3..5], out=out2);`
    `RAM8(in=in, load=load3, address=address[3..5], out=out3);`
    `RAM8(in=in, load=load4, address=address[3..5], out=out4);`
    `RAM8(in=in, load=load5, address=address[3..5], out=out5);`
    `RAM8(in=in, load=load6, address=address[3..5], out=out6);`
    `RAM8(in=in, load=load7, address=address[3..5], out=out7);`
    `Mux8Way16(a=out0, b=out1, c=out2, d=out3, e=out4, f=out5, g=out6, h=out7, sel=address[0..2], out=out);`
    `}`
    
Building larger RAM modules involves the same logic setup. A whole hiearchy of memory can be built like this. I also built 512 from 8 RAM64 and so on. Each time we extend the number of registers we need to have wider address so when we end at the final RAM module 16KRAM the address is 14-bit long. 
Below here is the structure of a RAM512 module that uses simple a multiplexer to select among the 64 RAM and then these chips by themselves have the circuitry to further select down to you reach a individual memory address. 


**NAND2te**

The ultimate function of the machine is to execute programs written in machine language. A machine language is an agreed-upon formalism designed to code machine instructions. 
As a programmer you don’t interact directly with machine language, as "it is a language designed to effect direct execution in, and total control of, a specific hardware platform" - unlike high-level languages whose "design goals are cross-platform compability and power of expression" (page 96).  At the machinel language level, "abstract design of humans,.. are finally reduced to physical operations performed in silicon" (page 97). It's important to understand how high-level programs are eventually executed in machine language to write more efficient programs and to come up with ways of using the hardware for solving problems. 

A machine language "is a agreed upon formalism of how to manipulate *memory* using a *processor* and a set of *registers*" that designers of computers have decided upon when construction the hardware circuits. It needs to specify the following: 
1) What operations are supported in the CPU such as adding, branching, logical operations and their unique machine codes
2) How to access and manipulate the collection of hardware devices that store data and instructions thus the memory
3) How to control the program - the next instruction to execute
### Operations supported
In any machine there are operations to do arithmetic, logic, flow control as well as moving data between different memory units. Inspired by Randal E. Bryants *Computer systems: a programmer's perspective*, the table below shows common patterns or formats of instructions in computers. What this table shows is that these can range in width in this case from one to ten bytes. Each instruction is unique like the address we created for the memory addressing. Hexadecimal numbers are used to enumerate the instructions where the first 4-bits of the first byte specifies a specific type of instruction. In this case 6 os related to an integer operation. Then the next four bits represeted by f specifies the type of integer operation. The next byte holds the *operands*, these are the registers which holds the input needed for the operation and such it addresses the register units. In this case 4-bits are used so there can be no more than 16 registers directly available to this CPU. Another instruction like moving data between registers, involves a data value which is a constant supplied by the instruction directly through the bytes two to nine.  



There are also instructions to branch or jump to specific addresses which is an important feature needed for many programs. This is a *control-flow* mechanisms which allows programs to unfold differently based on conditions. The jump instruction is followed by an address, which is the address of the instruction that should be supplied to the instruction register. This jump instruction may be conditional or unconditional. By inspection of this table it can be seen how writing a specific sequence of bits instructs the machine to do a specific operation. To access the stored data and instructions, the instruction needs to specify the location. 
### Symbolic language
Machine language is convient for machines but not so much for people that want to program them. To begin with programmers created a symbolic language which they could write out programs on paper such that it could be easierly understood and shared among professionals. At this time it was still a matter of mechanically controlling sets of inputs to run programs and this was tedious and laboursome. This then turned into a program itself when the first translator or assembly program was developed. 
Instead of writing 1001010101 in a executeable file, it would now be possible for programmers to use symbolic language. An assembly programis therefore a program that have to be run each time a program needs to be executed and translated and therefore it's quite important that it is efficient. For example a program in assembly that adds up two numbers might look like this

`load R1, 17       // R1 <- 17`
`load R2, 4        // R2 <- 4`
`add R1,R1,R2 // R1 <- R1 + R2`

Or a program that computes a logical operator might look like this:

`load R1, true  // R1 <- binary representation of true`
`load R2, false // R2 <- binary representation of false`
`and R1, R1, R2 // R1 <- R1 and R2 (bit-wise AND)`
We also want to write programs that involves *branching* actions. Machine languages feature several variants of conditional and unconditional goto instructions. Below is two examples of pseudocode for two programs written in the assembly language for the Hack comptuer. 

As is evident by these two programs is that there may be multiple ways of writing the syntax for example to address. In general you can address direct by providing the specific memory address (physical address) or use a symbol that represents such address. These are all equivalent but requires some more work for the assembler to work such as having a *symbol table* that maps physical addresses to symbols. 

There are some *built-in symbols* in the HACK symbolic language. For example there are 15 virtual registers 0-15 which can be labeled using R0,R1...R15. It makes the program more readable. In addition there are the two base addresses for the screen and keyboard @SCREEN, @KBD. Finally there are six symbols that are used for writing compilers and virtual machines which are 
SP, LCL, ARG, THIS, THAT. These are summrarized in the below table.

| symbol | value |
| :----: | :---: |
|   R0   |   0   |
|   R1   |   1   |
|   R2   |   2   |
|  R15   |  15   |
| SCREEN | 16384 |
|  KBD   | 24576 |
|   SP   |   0   |
|  LCL   |   1   |
|  ARG   |   2   |
|  THIS  |   3   |
|  THAT  |   4   |
### Input/output handling 
A general purpose computer have several pheripials or I/O devices which the hardware interacts with. For example it is normal to have both a screen, keyboard, mouse, internet, microphone, headset, camera and so on. All these devices needs some parts of memory where their input or output values can be stored. Below here is an example of how the HACK hardware platform allows a screen and keyboard device. The screen is a 256 x 512 screen, where it has a memory map of 8K memory blocks of 16-bit words. Each pixel can either be black (1) or white (0). Each row is 32 16-bit words, and thats why it is 512 columns. We cannot directly select an individual pixel bit, instead we have to select the entire 16-bit word and manipulate it using arithmetic and logic. The program below selects where the screen starts in memory @SCREEN and from there it manipulates all the values to black by setting it to the value -1 which is represented as 16 consecutive 1’s in binary. 
Interacting with the keyboard also provides a memory map, but in this case only a single word which represents a key pressed or a 0, if not key is pressed which gets stored there. 
### The HACK language
A HACK program is essentially a sequence of 16-bit numbers that instruct the hardware what to do. Looking at a model may help understand how the semantics work. In the HACK hardware, we have access to a data memory on the left (RAM), which contains registers of 16-bit values that can be accessed using the M address. For example M=0 sets the register to the value 0. 

The right hand side is a ROM instruction memory. In addition there is 
1) The data register denoted D, holds a 16-bit value
2) The A register which holds a 16-bit value which represens either a data or an address
3) M is the selected register
### HACK syntax
The HACK is language that have some syntax unique to this language. For example it has created two separate instructions types A and C instructions. 

**The A instruction**
The syntax of the A-instruction is: @value
This sets the A register to some 16-bit value either a *non-negative decimal constant* or *a symbol referring to such a constant*. There is one side-effect of setting the register A's value. namely that the 16-bit value becomes also the selected register thus M = RAM[A]. 
For example: @21
1) A register is set to 21 
2) RAM[21] becomes the selected RAM register (M)
Setting RAM[100] to -1
	@100 // A=100
	M = -1 // RAM[100] = -1

Before we can do any manipulation to memory we have to select that register using the A-instruction. 
The A-instruction is used for three different purposes. 
1) First, it provides the only way to enter a constant into the computer under program control. 
2) Second, it sets the stage for a subsequent C-instruction that manipulates a selected RAM register, referred to as M, by first setting A to the address of that register. 
3) Third, it sets the stage for a subsequent C-instruction that specifies a jump by first setting A to the address of the jump destination. 

**The C instruction**
The syntax of the C-instruction: dest = comp ; jump 
We compute something and then store that value or use it to decide if we need to jump to some other parts of the program. Now here is where the Hack language differs. Normally a instruction could by itself perform this operation in one single line. It could provide the instruction or opcode to subtract two values and store it in a destination. The reason for this is probably that this machine only have 16-bit instructions while the modern computers work with up to 10 bytes for example. For example the D = D + M may be written as ADD D, ADDR

The C-instruction answers three questions: 
1) what to compute (an ALU operation, denoted comp), 
2) where to store the computed value (dest), 
3) and what to do next (jump). 
Along with the A-instruction, the C-instruction specifies all the possible operations of the computer. 
### Looking at binary codes
We can write the HACK programs using symbols or they can be written directly as a sequence of 0's and 1's that is the binary version. The A-instruction in binary may look like this: 0000000000000001. 
This will mean setting the A register to the value 1, so is equivalent to @1. 

A C-instruction have the following format in binary: 
![[99 Archive/Images/NAND2Tetris/C-instruction in binary|center]]

1) The leftmost bit is the C-instruction’s op-code, which is 1. 
2) The next two bits are not used, and are set by convention to 1. 
3) The next seven bits are the binary representation of the comp field. 
4) The next three bits are the binary representation of the dest field. 
5) The rightmost three bits are the binary representation of the jump field. 

### Symbolic to binary mapping
In order to have a symbolic language we need to have a table that or some data structure that can map between each of these. In the HACK programming we always have one register selected and we have to manipulate that with an A-instruction. Therefore the number of registers is reduced to 8 really and that means 3-bit destination code is sufficient to decode which destination to write values to. 
Similarly there are eight jump instructions which can be seen in the table below. 

For example this instruction here: 1111010101101100 corresponds to AM = D|M;JLT as can be confirmed in the mapping tables above. Assembly instructions can specify memory locations (addresses) using either constants or symbols. The symbols fall into three functional categories: predefined symbols, representing special memory addresses; label symbols, representing destinations of goto instructions; and variable symbols, representing variables. 
The predefined symbols are designed to promote consistency and readability of low-level Hack programs. Example below. 
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpRDA-l0YKP7sEJH9RaEGOIKF2JJOTilhnVNY76zA2xiVj3KqvZMqo-Gc5Ejo0pug80sZqK6JTVFh_2a6z3PRvTj4xoBm7N3ePv_WyntQxxsnZToR6mTu6D7DaP8dMHRrrM6mP?key=167T_JJA07NWDA6FMMAv4q-3)
Here @7 sets the A register to 7, and @R3 sets the A register to 3. The @ signals that A is used as a data register and R3 signals that it is used as a data memory address. 
### Syntax for interacting with input/output devics
High-level programming languages offers a suite of libraries to enable text, graphics, animations, audio, video etc to interact with input and output devices. At this current level of abstraction we really use symbolic or bits. What we really have in this architecture is a designated place in the memory of the device is managed. To write a string like "Hello world!" takes quite a lot of manipulation of bits to turn on the right pixels. 

**The screen memory map**
The display memory map is a display unit of 256 by 512 black and white screen. Not surprisingly the screen memory map has been allocated around 131072 bits or around 8KRAM registers of 16-bits. How do we manipulate the pixels? It turns out that we cannot access a single bit but only 16-bits at a time. The first row is the first 32 RAM registers in the memory map and so on. So to manipulate a single bit we need to figure out which register it belongs to and manipulate it somehow using the ALU. There are two ways to set a specific pixel on and off 
1. word = Screen[32 * row + col/16]
2. word = RAM[16384 + 32 * row + col/16]
3. Set the (col % 16)th bit of word to 0 or 1
4. Commit word to the RAM
It takes quite a lot of work to control a single bit. If you want to change the bit in the fourth row and column 55 that means you will access that bit as follows
@Screen[32 * 4 + 55/16] = 128+7 = @Screen[135]

**Keyboard memory map**
The keyboard memory map is likewise a part of memory that can be updated. The difference is that this only consist of a 16-bits and so is a single register. When pressing a keyboard the ASCII value for that in binary form in the keyboard memory.
### The HACK program
For these programs it important to recognize the comments there are made to make the code understandable. Donald Knuth is a computer scientist that is involved with understanding how computers and their low level algortihms work to execute programs. He has said that
> Instead of imagining that our main task as programmers is to instruct a computer what to do, let us concentrate on explaining to human beings what we want a computer to do - Donald Knuth

**Manipulating registers and memory**
A lot of low level programming is about manipulating memory and registers. The Hack program uses the A-instruction to select a register number or symbol that **points** to a physical memory address. 

For example @10, selects the RAM[10] register. Now you can set the value of that register to some other value or compute a new value such as 
D = D + M 
M = 1
M = -1 
D = M

We can use these register and memory operations to create a small program like this one that adds two memory values and store it in a third memory address. 
![](HACK%20program%20adding%20two%20values.png|center)
When i load this into the CPU emulator i can follow the execution of the program either using the symbolic representation which has been loaded into ROM. 

![](99%20Archive/Images/NAND2Tetris/Project%204/HACK%20program%20CPU%20emulator.png)

**Branching, variables and iteration**
All machines have built-in capabilities of doing some control flow. This could be evaluating some condition that turns true or false and then directing the program of that. High-level programming languages typically have many different ways of using this capability such as pythons if,elif,else or DAX SWITCH() method. 

An example of such a program is this Signum.asm program. The syntax here uses the D;JGT jump instruction and goes to @8 if it evaluates to true, otherwise it continues the program and sets R1 = 0 in lines 13 and 14. We can make the code even more readable by using the label declaration. Examples of these programs can be found here: [Assembly programs with branching](99%20Archive/Images/Assembly%20programming/Assembly%20programs%20with%20branching.md) 

Here is an example of using a variable in a program called @temp. What the program does is, it finds some available memory register and use that register whenever the lable @temp is used in the program. It may be @16 or any other memory address. Typically the people that write assembles know which memory space can be allocated to variables and in the HACK that is from 16 and onwards. 

![](HACK%20program%20with%20variable%20declarations.png|center)
Finally we're going to inspect programs that do iterations. Imagine we want a program that computes  1 + 2 + 3 .. and so on until some condition is met and stores the result in RAM[0] or R1. The final program may look like this. 
![](HACK%20program%20with%20iterations.png|center)
The overaching key thing to take away from this section is that of how to write programs. The best practice is as follows:
![[99 Archive/Images/Assembly programming/Algorithm for writing programs]]
For example writing the program for the iteration above could be designed from this pseudocode, where you have some variable n, which you declare and then the number of iterations up until that value you sum up and store that in R1. [Pseudocode for iteration program](99%20Archive/Images/Assembly%20programming/Pseudocode%20for%20iteration%20program.md) The following link is to a sample pseudo code for an iteration program. Again it requires a lot of operation compared to a high-level equivalent. 

**Pointers**
In this file there is an example of a program that uses *pointers.* The use of pointers in that example is to manipulate an *array* which is an high-level programming abstraction. [Assembly program using pointers](99%20Archive/Images/Assembly%20programming/Assembly%20program%20using%20pointers.md)

**Input/Output**
Interacting with input and output is an important function and this file [Assembly program for interacting with input and output](99%20Archive/Images/Assembly%20programming/Assembly%20program%20for%20interacting%20with%20input%20and%20output.md) contains an example program from the course that draws a rectangle on a screen. What is obvious from this program and all the above is that writing low-level code requires alot of work! A few lines of code in a high-level language can easily translate into tens or hundreds lines of code in assembly. That may be why it seems like magic! 
If you had to write you code directly in machine language you would understand the individual operations and could connect the dots to why pressing a keyboard button shows up exactly where you expect. 


**NAND2te**
long 
The embedded versions of computers such as those in physical products such as cars, phones, watches and our homes, are special designed for the specific purpose of that device. While they share much of the same elements and structure, this book is about the all-purpose computer.
 Zooming out all computers are built of some hardware and software hiearchies but within those there can be multiple design choices and that's where embedded systems differ from all-purpose ones. The all-purpose computer is indeed a complex artifact that requires thoughtful engineering. There are many historical cites that prove that humans have formed these complex artifacts long before digital computing. To build large buildings, design big cities, develop large scale manufacturing involves handling complexity. The field of engineering and architecture study these designs and have accumulated a set of principles that we may also come learn as we study digital computers.

The Von Neumann Architecture is the practical model that informs the constructions of almost all computer platforms today. It relies on the key element of the stored program. Right below is a sketch of the architecture similar to the one given in the book’s figure 5.1 in section 5.1.2. The memory is physically a sequence of registers that are addressable. 
* The data memory contains binary values which when translated to machine language and supplied to the CPU are manipulated. 
* The instruction memory is a separate part of memory. The instruction from the program memory are fetched and executed by the CPU. This instruction can hold data and this contains all the information needed to execute the instruction.
![[Von neumann architecture.png|center]]
**Fetch-execute cycle**
In order to progress in a program we need to put the content in the address of the address in the program counter into the instruction memory. This is called the **fetch-execute cycle**. 

**Fetching**: Put the location of the next instruction into the "address" of the program memory. The instruction itself by reading the memory contents at that location. The program counter holds the next instruction, which can either be manipulated by incrementing or loaded in with another value.

**Executing**: In the execute cycle, we can work with the instruction as it has been loaded into the instruction register. The information about what to do next is already in this code. Different parts of the instruction bits control, control the different parts of what needs to be done. The control part of the instruction is put onto the control bus and configures the hardware to do the desired operation. 
### The central processing unit
The hack hardware platform is designed to execute programs written in the Hack machine language. It consists of a CPU, two separate memory modules serving as instruction memory and data memory, and two memory-mapped I/O devices: a screen and a keyboard. The Hack CPU is designed to execute instructions written in the Hack machine language. In case of an A-instruction, the 16 bits of the instruction are treated as a binary value which is loaded as is into the A register. In case of a C-instruction, the instruction is treated as a capsule of control bits that specify various micro-operations to be performed by various chip-parts. 
The CPU not only execute the instruction of a program that allows us to watch videos, listen to music or buy a ticket to a event. It also can compute the next instruction that should be executed. 

If we look at the CPU is connected to an instruction memory, from where it can read and write. 
* InM: The 16 bit data input from the data memory
* Instruction: The 16-bit value of the selected instruction memory register
* Reset: 1-bit input
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXekHQW7IbATqV7qRT3FC_KkzMFo_bWuLZfaq3GlRLH0KCIfnltJo9SpHhXXFfTsFDff7faSQkXAAaGOv2-qYug5xH6uFUkn7-MbTG_9WqZnQ1BQxioP_l-F1Jfc66wDPv8z852FZA?key=167T_JJA07NWDA6FMMAv4q-3)

The output of the ALU can be written back to data memory or be held in the registers. The outM and writeM are realized by the instruction itself that has been read, and by the combinational logic in the CPU are affected instantaneously. 
**Proposed implementation**
Taking a look inside the CPU it should be able to determine which instruction should be fetched and executed next. The CPU can be seen as an orchester that work together in harmony to play a specific song. An orchester can play many songs, like an CPU can execute many programs and it is the bits of the program like the sheets of music that controls which song or program is executed. 
![[Computer architecture.png]]
This is design is one example as provided by the book follows the abstraction above, as it has three inputs and four outputs. It's also visible that this CPU is built from components we have already built earlier, so it is just a matter of piecing them together. 


# Nand2te


Machine languages are typically specified in two flavors: binary and symbolic. A binary instruction is “an agreed-upon package of micro-codes designed to be decoded and executed by some target hardware platform. When we set out to build a hardware architecture and a machine language, we can decide that a particular 32-bit instruction will cause the hardware to effect the operation “load the constant 7 into register R3.”  Modern platforms support hundreds of possible operations. The symbolic syntax may be “load R3, 7” where the binary instruction may be 1100001000000110000000000000111. This is also called a mnemonic, and the language of these is called assembly. “The assembler parses each assembly instruction into its underlying fields, for example load, R3 and 7 translates each field into its equivalent binary code, and finally assembles the generated bits into a binary instruction that can be executed by the hardware. Hence the name assembler.”

For this project we will build an assembler. What we are concerned with here is the gap, the middle part of the picture below. That is where symbolic language is transformed it it's machine version.
![[99 Archive/Images/Assembly programming/The assembler|center]]
![](99%20Archive/Images/Assembly%20to%20binary.png)
To make a program that does this, we need software. In this course we will use a high-level language like python to write the assembler for the HACK computer. The assembler is the first software layer or abstraction we have in the computer. 

The basic assempler logic has to 
Repeat: 
* Read the next assembly instruction. Ignoring whitespaces the characters should be read into an array of characters
* Break down the instruction into individual fields
* Translate to binary (also handling symbols and labels)
* Combine
* Output
In the drawing here [Assembler logic](99%20Archive/Images/Assembly%20programming/Assembler%20logic.md) i have made a sketch of it.

**Understanding the semantics and lexical elements of the assembly languages**
Implementing an assembly program requires one to understand at a deep level, the lexical elements both of the symbolic and machine version of the Instruction set architecture (ISA). It's what our minds do when we have to translate between languages, like spanish. We have to look at a word and say okay, what is the meaning of this, and how is it expressed in the target language. 

In the hack assembly program there are two major types of instructions, the A instruction and C instruction. 

**The A-instruction**
The A-instruction have the following syntax @value, where value can be 
1) A non-negative decimal constant or
2) A symbol refering to such a constant
In the binary format it would be [0]000 0000 0000 1010 for the value @10 or a symbol that refers to that constant either being a label or a variable. 

Assembly languages use symbols for three purposes:
- Labels: Assembly programs can declare and use symbols that mark various locations in the code, for example, LOOP and END. These are declareted in the program as *(label)*. 
- Variables: Assembly programs can declare and use symbolic variables, for example @i and @sum
- Predefined symbols: Assembly programs can refer to special addresses in the computer’s memory using agreed-upon symbols. The general syntax is @variablename, for example @SCREEN and @KBD. 

The assembler needs to handle the task of “remembering” what each of these symbols stands for. So SCREEN stands for the binary memory address where the SCREEN starts. Loop stands for some memory address of the instructions to go to. 

```
	@i
	M=1
	@sum
	M=0
(LOOP)
	@i
	D=M
	@R0
	D=D-M
	@STOP
```

**The C-instruction**
The C-instruction similarly have a symbolic and machine version and it follows a general pattern that allows the microarchitecture to decode it. In general it follows the pattern below

![[99 Archive/Images/NAND2Tetris/C-instruction in binary]]
Each of the components have a mapping table that can translate one version to the other and these are a part of the ISA specification for Hack. 

**Handling instructions**
Consider first to distinguish if it's an A-instruction or C-instruction. This can be decided by looking at the first character. If it's an '@' then it's an A instruction by the convention of the Hack assembly semantic, otherwise it's an C-instruction. (Here we assume programs are written correctly). 
- If A-instruction, then convert the decimal constant into binary. It may have to be looked up in the symbol table first. A decimalToBinary() subroutine could be useful here. 

- If C-instruction then decompose it's parts by splitting the string either by "=" for regular ALU operations or ";" for JMP operations. This can be realized by understanding again the semantics that define the grammatic rules of the language, we use those to make the assembler. Splitting with "=" yields the dest and comp components and these just have to be looked up in the mapping tables and then used to build a string. You get something like this
  - string =  '111' + comp_table[comp] + dest_table[dest] + '000'
  - string = '111' + comp_table[comp] + '000' + jmp_table[jmp]

**Handling symbols**
One way to solve handling symbols is to use a two-pass process of parsing the file. 
1) One the first pass look for symbols that are labels checking if the string starts with '('. Then locate the name of the label by taking the string from [1 to last] after splitting it by ')'. This requires some string manipulating but is doable. Then add to the symbol table, storing its value as the line number, keeping track of where it is in the program. 
2) On second pass symbols that are defined as variables @variablename are located and added to the symbol table if they don't exists already

Interestingly enough i believe it's when this symbolic language come in that the connection to the machine hardware becomes blurry. It's kind of like if you were speaking to someone but not the same langauge and you hired a translator which all communication would go through. The connection would not be as deep as if you we're talking directly. With high-level language the communication with the machine is almost lost, a single high-level code may be tens of lines of machine code. It's here that low-level curiosity is key. It enables me to understand that what i write becomes these instructions and it may take several instructions to execute a seemingly trivial program like print("Hello World!) if we had to implement it in machine code, doing all the variable assignments, moving data, calculating, manipulating pixels on the screen - we would acknowledge the work that is actually going on.

**Proposed implementation**
1) Clean up file
   * Ignore whitespace, line comments and in-line comments
2) Parse file to handle symbols
3) Translate assembly instructions to binary

[Project 6](Project%206.md)

### The Jack programming language
> High thoughts need a high language. - Aristophanes (427-386 B.C.)  (P. 235, Simon Schocken & Noam Nisan)

The Jack programming languages is this book and courses version of the high-level languages that resembles other object oriented languages like  Java and C++, but with no support for inheritance. (p. 235, Simon schocken & Noam Nisan). 

This chapter begins with the "inevitable hello world program" which is written using the following syntax. The Jack program always begins with the Main.main function, that is a main function within a Main class. 
```
class Main {
	function void main() {
		do Output.printString("Hello World");
		do Output.println(); // new line
		return;              // return statement is mandatory
		}
}
```
What is apparent here is that the Jack program comes with a *standard class library* this library comes with extensions to the basic language. In this example two functions are used to print to the screen and a new line. The internal implementation is abstracted away here offering a standard API to the programmer. 

Another example program is provided and i have drawn the syntax out on paper below. It's a program that reads some input from a keyboard and calculates a simple average. What is also apparent is that there are different variable types, both primitive and class types. 
![](99%20Archive/Images/Jack%20program%20procedural.jpg)
There are four types of variables 
 * Static variables: class-level variables, can be manipulated by the class subroutines
 * Field variables: object properties can be manipulated by the class constructors and methods
 * Local variables: used by subroutines, for local computations
 * Parameter variables: used to pass values to subroutines, behave like local variables
 All these have to be typed and declared before they are used (Unit 3,7 minute 4)

**Extended the language using classes**
The programmer can extend the language with new types by defining a class that represent that abstract data type. One example provided in the book is a fraction abstraction. 
The important thing about creating a class is to consider: What kind of data do we want to store about the object this class will represent? (Unit 3.2)
1. The data we want to store are the *fields* or *attributes* of the class and 
2. the actions or things we want to do with the data is the *methods* of the class. 
3. A class has a special method called a *constructor* that is invoked whenever a new instance of a class is created which initialize the instance. 

```
class Fraction {
	// Fraction object has a nnumerator and a denominator
	field int numerator, denominator 

	constructor Fraction new(int x, int y)

	method int getNumerator()
	method int getDenominator()
	method Fraction plus(Fraction other)
	method void print()
	method void dispose()
	// more fraction-related methods
	...
}
```
The general structure of a class is a follows 
```
class name {
	field variable declarations // must precede the subroutine declarations
	static variable declarations // must precede the subroutine declarations
	subroutine delcarations      // Constructor, method and function declarations
}
(P. 244, Simon Schocken & Noam Nisan)
```
For subroutines if they are designed to not return any value the *void* is declared as the type. If the subroutine is a *method* or *function*, its return type can be any opf the primitive data types supproted by the language (int, char or boolean), any of the class types supplied by the standard library (String or Array) or any of the types realized by other classes in the program (e.g., Fraction or List). If the subroutine is a *constructor* it may have an arbritrary name but its type must be the same of the class to whic it belongs. (P. 244, Simon Schocken & Noam Nisan). 

Using the class could then be done in a program like this a, which reveals an "important concept of software engineering, that users of an abstraction like Fraction don't have to know anything about its implementation"  (P. 239, Simon Schocken & Noam Nisan)

Here three fraction objects are created. Then two new fractions are constructed setting a and b to the base addresses of a memory block containing the new fractions data. 
![](99%20Archive/Images/OO%20programming%20jack.jpg)
The constructor interacts with the OS to allocate memory for the new object in memory. 
To use the string class for example on could write
```
var String s;
var char c;
let s = "Hello World";
let c = s.charAt(6);
```
What happens under the hood is that the statement s = "Hello World" is compiled into s = String.new(11) and then callend the method s.appendChar(character integer code) for each character. 
**Linked list implementation**
We can also use classes to contain a collection of items, such a common one is a *list.* Creating a list class in jack may look like this. 
```
class List {
	field int data; // a list consist of an int value
	field List next; // followed by a list

	constructor List new(int car, List cdr) {
		let data = car;
		let next = cdr;
		return this;
	}
	/* Accessors */
	method int getData() {return data;}
	method List getNext() {return next;}
	/* Prints the elements of this list*/
	method void print() {
		// initializes a pointer to the first element of this list
		var List current;
		let current = this;
		// iterates through the list
		while (~(current = null)) {
		do Output.printInt(current.getData())};
		do Output.printChar(32); // prints a space
		let current = current.getNext();
	}
	return;

	/* Disposes this List */
	method void dispose() {
		//Disposes the tail of this list, recursively
		if (~(next = null)) {
			do next.dispose();
			}
			// Use an OS routine to free memory
			// held by this object
			do Memory.deAlloc(this);
			return;
			}
} // end of list declaration
```
Then we may create instances of this class
```
var List v;
let v = List.new(5,null);
let v = List.new(3,v));
let v = List.new(2,v));
do v.print(); //prints 2 3 5
do v.dispose(); // disposes list
```
Invoking a method like do v.print() will start a long process of implementation, but from the clients perspective it is just an abstraction supplied by the OS. In general the OS supplies eight classes. 
* Math.
* String: 
The String class contains a constructor for creating strings and applying different methods to this data type.
* Array:
If you want to create an array using jack programming, you will have to make a call to Array.new() for example let a = Array.new(3)
* Output
* Screen
* Keyboard
* Memory:
The memory class let's you manipulate the memory directly such as alloc and deAlloc which are used to create and dispose memory blocks. 
* Sys
**Developing apps using the Jack language**
At this point we are ready to start developing applications with the Jack language. The jack OS supplies a class that can be used to handle textual outputs which may be very useful. 
For graphic applications the screen should be viewed as a grid of 256 rows of 512 pixels each and use the supplied OS screen class. setColor can be used to draw black or white until a next setColor is set. 
The keyboard class can be used to handle inputs. The keypress method is always returning the scancode of the key that the user is currently pressing. 
The character set of the jack program. 
* Key point: High-level programmin can virtually extend the language in infinite ways making it such a powerful design. Above is seen how creating a new class enables one to create new objects and work with them programmatically - very powerful. 
* You need a scientific brain, a statistical brain and a mathematical brain to work with high level programming and you can develop serious things. 

A compilation process has two main stages: *syntax analysis* and *code generation*. Syntax analysis stage is usually divided further into two substages: *tokenizing*, the grouping of input characters into language atoms called *tokens*, and *parsing*, the grouping of tokens into structured statements that have a meaning. (p. 261,  Simon Schocken & Noam Nisan). 
![](99%20Archive/Images/Development%20plan%20of%20the%20Jack%20compiler.png)
The job of the the syntax analyzer is to *understand the structure of a program* (p. 261, Simon Schocken & Noam Nisan). 

**Lexical analysis and tokenizing**
The programming language *lexicon* is the tokens that the language recognize. In the Jack language it includes *keywords*, *symbols*, *integer constants*, *string constants* and *identifiers* (p. 262, Simon Schocken & Noam Nisan). The first tasks is to group the "stream of characters" into it's grouping also called *tokenizing*. The reason for this two step process is to modularize the process. 

**Parsing and parsing trees** 
A parser accepts an input that is a stream of tokens and attempts to build the parse tree assoicated with the given input (p. 267, Simon Schocken & Noam Nisan). Humans parse spoken and written languages, a cognitive process i won't elaborate on here.
![](Sketches/Sketches/Images%201/parse%20tree.png)
High-level computer languages can be parsed as well and that is the job of the compiler. Parsing the jack language can be Implemented diagrammatically with a parse tree can be done with different algortihms such as the *recursive descend.* 
#### Looking one or more symbols ahead
This recursive descend method fits the jack language because in the jack language, one only needs to parse from left to right and look ahead one symbol to unfold the meaning. This means that the grammatic rules of parsing the jack language is LL(1). Some languages have grammar that needs more flexibility and in those cases a top-down approach to parsing can be employed or predictive parsing. The need can happen when there is ambiguity about a production rule to choose expanding on a non-terminal. backtrack and in those cases the LL(1) fails. Let consider a classic example below. 
`if a then if b then s else s2`
What if statement does the else statement belong to? In many cases compilers will resolve this by associating the else with the innermost if statement. Consider again the syntax here
`1 + 2 * 3`
A parser that does not lookahead more than one symbol will not correctly evaluate this expression. This has led to the development of other strategies such as the LALR(1), GLR/Earley and the packrat (PEG).
#### Historical perspective
The Pascal programming language was one of the first languages and it was designed with LL(1) in mind with a clear and simple syntax. Then came more expressive langauges like C, C++, Java and Python. C uses a LALR(1) parsing strategy so does Java. Python has used the PEG parsing strategy since version 3.9 while early versions used LL(1). 

I also found this website [ANTLR Lab: learn, test, and experiment with ANTLR grammars online!](http://lab.antlr.org/) where you can see an actual parsing tree generated based on a interactive code cell which may be useful. One of the important things is to understand the lexical elements and grammatic rules of a language in order to parse it. This is more involved and technical for most professional languages and the jack program offers a look into that. 

**Jack grammar**
The Jack grammar can be seen to the left and the parse tree can be diagrammed as seen to the right. The same structure can be written as an XML file. 

**'xxx'**: used to list language tokens that appear verbatim
xxx : regular typeface represents names of non-terminals
()    : used for grouping
x|y : indicates that either x or y appear
x?   : indicates that x appears 0 or 1 times
x*   : indicates that x appears 0 or more times

These four terminals rules / elements or tokens from which the Jack program consists of.
![](99%20Archive/Images/Jack%20grammar.png)
These are sort of the rules that the language oblige to describing what statements are valid, how expressions are formed and what order tokens must follow. These rules are often written in EBNF notation (Extended Backus-Naur Form) for example class: 'class' className '{' classVarDec* subroutineDec* '}'. This rule defines the syntax of a class declaration. The keyword 'class' must appear first, then some class name, then a opening bracket, zero or more class declaration shown by the asterix. Zero or more subroutines declarations methods, functions or constructor inside the class, and a closing bracket. I found similar description here of the python grammar [PEP 617 – New PEG parser for CPython | peps.python.org](https://peps.python.org/pep-0617/) 

The EBNF rules maps directly to the recursive descend because EBNF describes grammar **top-down**, and recursive descent **parses top-down**. 
* Each EBNF production naturally maps to a **function** 
* Constructs like `*`, `?`, and `|` translate cleanly into loops, conditionals, or lookaheads.

The rules of creating an expression is bit tricky because of the term rule, we cannot know immediately what needs to happen and therefore it is the only place in the jack langauge where we have to look ahead and check the next character. 

Tokenizing by hand exercise
```
class Main {
   function void main() {
      var int i;
      let i = 2 + 3 * (4 - 1);
      return;
   }
}
```

| Token type | Token value   | Line number | Explanation                           |
| ---------- | ------------- | ----------- | ------------------------------------- |
| keyword    | class         | 1           | Begins class declaration              |
| identifer  | Main          | 1           | Name of class                         |
| symbol     | {             | 1           | Opening class body                    |
| keyword    | function      | 2           | start of subroutine                   |
| keyword    | void          | 2           | return value of function              |
| identifier | main()        | 2           | subroutine name                       |
| symbol     | {             | 2           | start of subroutine                   |
| identifer  | var           | 3           | variable declaration                  |
| identifier | int           | 3           | type of variable                      |
| identifier | i             | 3           | VarName                               |
| symbol     | ;             | 3           | symbol of ending variable declaration |
| keyword    | let           | 4           | Begins let statement                  |
| identifer  | i             | 4           | VarName                               |
| symbol     | =             | 4           | symbol of expression                  |
| identifier | 2 + 3 * (4-1) | 4           | expression                            |
| term       | 2             | 4           | term                                  |
| symbol     | +             | 4           | symbol                                |
| term       | 3             | 4           | term                                  |
| symbol     | *             | 4           | symbol                                |
| symbol     | (             | 4           | symbol                                |
| term       | 4             | 4           | term                                  |
| symbol     | -             | 4           | symbol                                |
| term       | 1             | 4           | term                                  |
| symbol     | )             | 4           | symbol                                |
| symbol     | ;             | 4           | end of let statement                  |
| keyword    | return        | 5           | return statement                      |
| symbol     | ;             | 5           | end of return statement               |
| symbol     | }             | 6           | end of function declararation         |
| symb       | }             | 7           | end of class declaration              |

**Jack analyzer**
The jack analyzer checks if we encounter a terminalElement xxx of type, keyword, symbol, integer constant, string constant or identifier. If so it generates output like the following format
```
<terminalElement>
	xxx
</terminalElement>
```
So for example
```
<keyword> method </keyword>
```
Instead if we encounter a nonTerminal element of the types class, class variable, subroutine, parameter list, subroutine body, variable declaration, statements, let statement, if statement, while statement, do statement, return statement, an expression, a aterm, or an expression list. Such an example is given below with the statement return x. 
```
return x

<returnStatement>
	<keyword>
		return
	</keyword>
	<expression>
		<term>
			<identifer> x </identifier>
		</term>
	</expression>
	<symbol> i </symbol>
</returnStatement>
```
Recieves a single filename.jack or directory containing 0 or more files. For each file it 
1. Creates a JackTokenizer from fileName.jack
2. Creates an outputfile named fileName.xml
3. Creates a compilation engine to compile the input JackTokenizer into the output file