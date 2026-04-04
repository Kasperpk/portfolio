The ALU, memory chips, decoders and multiplexers are the set of building blocks that computers in modern technology share. In this section were going to see how this hardware is controlled as described by the *architecture*, also called the *instruction set architecture* (ISA) of the computer. The instruction set architecture of the machine, is the vocabolary, the language that describes how to "speak" with it. The 8000 intel series first released in 1972 had byte-sized instructions codes, while offering 255 unique encodings, the ISA had 48 nstructions among them integer operations like add and substract, logical operations such as shift, AND, OR aswell as operations to move and jump. These primitive instructions may be combined in any imaginble way and assembled to execute entire programs. Even with the simple instruction set of the first intel 8000s series, an incredible variety of programs could be designed. This is something that can be difficult to accept at first, but the fact that tens of thousands of add, jump, move, load, shift can be executed every second it can lead to very sophisticated results. Moore's law made some ambitious predictions about how rapidly computers would evolve, and opening up a microprocessor years later revels that these predictions wasen't unrealistic. In modern systems instructions are encoded using 64-bits and processors operate at multiple giga-hertz, The processor reach for even high performance through the ideas of multi-core processing and pipelining. The vocabolary of computers have naturally been extended and various dialects have been developed in different architectures such as MIPS, ARM, x86, SPARC, PowerPC and RISC-V. The number one reason for this is that there are different design goals depending on the purpose of the device, Harris and Harris (2012, p. 289)  A mobile device benefits from lower power consumption to increase battery life, something which the ARM processor architecture has proven good at. The RISC-V architecture limits the number of instructions to keep the device as small as possible, hence the name _reduced instruction set computer_. x86 and ARM processors, on the other hand, provide an increased number of instructions, offering more capability but at the cost of additional overhead even for simple operations. Ultimately computer engineers need to decide what to put into the processing unit and  how each word in the vocabolary should look like, which as we now know must be a sequence of 0's and 1's, the only input that this digital artifact will accept. Each application running on a computer uses the same chosen architecture, since it “eventually compiles into a series of simple instructions such as add, subtract, and jump” (Harris & Harris, 2012, p. 289). These machine instructions are the fundamental units of execution for a processor and consists of two primary components:

1. **Operation Code (Opcode)**: Specifies the operation to be performed
2. **Operands**: Specify the data to be operated upon

Consider a 32-bit instruction format where:
- The first 8 bits (bits 31-24) represent the opcode
- The remaining 24 bits contain operand information

For example, a 32-bit ADD instruction might be structured as:
11110101    0110           0111           1011        000000000000

In this example:
- `11110101` is the opcode for addition
- `0110` specifies the first source register 
- `0111` specifies the second source register 
- `1011` specifies the destination register
- The remaining 12 bits are unused in this instruction format

Operands can originate from three primary sources:
1. **Registers**: Fast, on-CPU storage locations (e.g., r1, r2)
2. **Memory**: Addresses pointing to data in RAM
3. **Immediate Values**: Constants embedded within the instruction itself

**Symbolic versions of machine language**
To acknowledge that the machine instruction like the 32-bit version above is an add instruction is not readily obvious, unless you have tons of experience reading and writing machine code. It must have scared some people away from programming in the early days and frustrated the many who decided to stick through it. As a response the programming community invented the much more digestible symbolic version called assembly. First written by hand, it mapped each instruction to a simple readable format looking like natural language. Later as programs were written in text editors special software called assembler, did the translation. While introducing some overhead as each program had to go through this assembly translation, it created much better conditions fpr any programmer. To get a feel for how assembly works, let's look at some simple instructions look like in assembly. The addition instruction introduced above consisting of 32-bits 11110101 0110 0111 1011 000000000000, could be expressed in RISC-V assembly as `add s11, s6, s7` which is quite intuitive once you learn the pattern. Add whatever is in registers six and seven and store the result in register eleven. Each instruction has this pattern and has to conform to it, making things as simple as possible. Searching for the MIPS architecture data card will show reveal a sheet that includes all the different instructions available and the assembly format for each. The general instruction format is shown at the bottom of the page. replicated here in figure 2.1. There are three general formats beginning with an opcode followed by operands which may be registers, memory address pointer, immediate values or whole addresses. 
![[Basic instruction formats|center]]
Figure 2.1 MIPS architecture instruction formats R, I and J.

Programming nowadays is almost exclusively done in the high-level languages like java, python, c or c++. These versions allow even closer resemblances to the real thing. For example expression addition can be done using algebraic symbols leaving us even more room for creative thinking than to learn an new syntactic way of adding two numbers. It also hand over a lot of details to the software hierarchy, something that will be studied later in the section on compilers. Consider the high-level python code in code example 1.1

Code example 1.1 python code for adding two variables
```
python

x = y + z
```

This high level program expresses a simple add instruction add instruction, which can be assembled using the add, rs, rt format. Now code example 1.2, shows how high-level programming easily can extend this with a subtraction term while keeping everyone in one line of code.

Code example 1.2 python code for adding and subtracting variables
```
python

x = y + z - u
```
At the machine level given it's vocabulary it would have have to work twice as much because it can by design only work two operands at the time. First it  adds y and z, then subtracting u from the result of the previous addition This is reflected in assembly which more closely maps to how the machine will execute the above program.

Code example 1.3 assembly instructions for code example 1.2
```
assembly

add t, y, z
sub x, t, u
```
Some other common operations are the logic operations, that chips were built for in the earlier sections. These operations are performed bitwise on registers one and two and stored in some third register. In assembly these instructions look as follows. 

Code example 1.3 assembly instrucions for common logic operations
```
assembly

and r3,r1,r2
or  r4,r1,r2
xor r5,r1,r2
not r6,r1,r2
```
The output of an AND operation on two 16-bit data values would for example produce the following results

| Byte                 | 0         | 1         |
| -------------------- | --------- | --------- |
| source register 1    | 1100 1010 | 1000 0010 |
| source register 2    | 0101 0010 | 1111 1111 |
| destination register | 0100 0010 | 1000 0010 |
Table 2.1 examples of binary addresses for source and destination registers


Bitshifting is another common operation, and that is because it can offer support for implementing efficient algortihms for things like multiplication. A program like the one in code example 1.4, may use these bitshifting operations with the mnemomic SLL. 

Code example 1.4 simple addition program of two constants in python
```
python

x = 10 * 15
```
Because of the base-two characteristic of the binary number system It turns out that shifting bit's one time to the left doubles the value of the number. Shifting the number three times increases the number by a factor of eight, thus the following assembly instructions may be generated on the backend of the high-level code in code example 1.4

Code example 1.5 assembly instructions generated from code example 1.4
```
assembly 

# Load immediate value 15 into register r1
ADD     r1,zero,15      # r1 = 15
    
# Compute 15 << 3 (15 * 8 = 120)
SLL     r2, r1, 3   # r2 = r1 << 3 = 15 * 8 = 120
    
# Compute 15 << 1 (15 * 2 = 30)
SLL     r3, r1, 1   # r3 = r1 << 1 = 15 * 2 = 30
    
# Add the results: 120 + 30 = 150
ADD     r4, r2, r3  # r4 = r2 + r3 = 120 + 30 = 150
    
# Store result in memory location for variable x
STORE   r4, x       # x = 150
```
We have now seen how instructions are represented at the machine level as sequences of 0s and 1s. The symbolic version of assembly allows us to read and write machine-level operations in a more human-readable format, but one that still retain the details of the machine instructions. Overall this helps us understand how programs translate and in fact in some cases may help choose the most efficient expressions of a program. The instruction set architecture is a useful abstraction that expressed the vocabolary of the machine, what operations it offer the programmer and how to command it at the lowest level. In the next section we will see how engineers put together digital building blocks into the *microarchitecture* that physically implements the ISA.


