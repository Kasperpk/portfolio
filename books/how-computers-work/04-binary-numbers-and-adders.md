In order to really understand how this is going to be possible it's useful to become acquainted with number systems and particularly the binary number system.
## The binary number system and bit manipulation
The decimal number system we have come to know have some quite elegant structures that we take for granted. One of them is the idea of positional value and the invention of the zero. Each position to the left increases the value of that digit by a factor of 10. 
![[Decimal number system]]
As shown here above this system is elegant and sophisticated. This system happens to be what we are using likely because of our 10 fingers, which has always been the number one tool for counting and doing arithmetic. 

The importan realization here is that there is nothing special about the decimal number system, other than the base 10. We can choose any base and construct a similar number system. There are hexidecimal systems with base 16 or octal systems with base 8. The binary number system is just as suitable and particularly for digital devices, since there is a one-to-one mapping between number of digits and electronic signal, just like the base 10 is very fitting for people with 10 fingers. What we need to be aware of is that with each new position, the value does not increase by a factor of 10, but instead by 2.   
![[Binary number system]]
Shown here is the number 11 in binary and the conversion to decimal is straight forward, by summing up the digits multiplied by their positional factor 2<sup>i</sup>. 

As you can see the number 11 takes up more space in a binary format given that our number of digits are limited to only two distinct values. In general we can represent 2<sup>k-1</sup> numbers, where k is the number of bits available. So if we had 8 bits we could represent up to the number 255. In practice half of the representations are reserved for negative numbers so instead we would have the range of numbers from -127 to 127. Representing up to 127 does not seem alot and computers engineers have been challenged by the fact that computers are bound by some physical laws which has limited the number of representations. The evolution of transistors and nanoscale has meant that computers can hold up to 64-bit numbers quite effortlessly, and 2<sup>64-1</sup> is such a larger number i will not write it here. 

**Converting from decimal to binary**
If we want to convert the other way around from decimal to binary, for example If we have the number 87 in decimal, the following algortihm can be used. 
1) Find the power of 2, that comes closest to the decimal number, here 64.
2) Write a 1 on the position of 64 in a sequence of bits, so 1000000 in this case. 
3) Subtract that from the orginal number and proceed again, finding the largest power of 2 that goes into the remaining, there 16 and put in 1 for this positional value so now, 1010000. 
4) The final answer becomes 1010111. 
If we were used to binary, we would obviously just look at 1010111 and know what number it is. 

### Doing arithmetic with logic circuits
Another important implication is that binary addition can be done using the same algorithm learned in elementary school. Starting form the rightmost bits or least significant bits (LSB), the stacked numbers are added and any quantity above nine is added as a resulting carry to the sum next pair of numbers. We do this until we reach the two most significant bits (MSB). 
![[Decimal addition]]
Here is an example of simple decimal arithmetic, were we use the concept of carrying over the amount of 1's that the digit over digit addition exceeds 10 to the next position. So as shown above, 8+5 = 13, 3 is kept and 1 is carried over.  It makes sense because if we isolate this calculation we have 83 + 56 and that would need another position as we move into the hundreds. 

Nothing different here with the binary system, other than the symbols are fewer. 
![[Binary addition]]
## Negative numbers
Computers also represent's negative numbers and does so with the two's complement. This represents the negative number using the postive number x using 2<sup>n</sup>-x. So for example in a 4-bit system the number 1111 would represent -1, 1110 -2, 1101 -3 and so on, so the largest half of the numbers from 8 to 15 would be reserved for the negative numbers starting with the lowest at 1111. It also means that we can only represent the positive numbers up till 2<sup>n-1</sup>-1 and the negative from -1 to -2<sup>n-1</sup> and therefore one more than the positive so here from 0-7 and -1 to - 8. 

The smart thing about this is that we can do something like -2 + -3 with the same circuitry we have. If we add 14 + 13 using the previous circuitry, and then remove the final bit then we have the correct result 11, which is -5 in two's complement. 
Another example of 7 - 5 is shown below. 
![[Two's complement addition]]
This is subtraction by addition. 

To go from 6 to -6 is can be done as follows. Take the positive number 0110, flip the bits 1001 and add 1, 1010, this is 10 in decimal and in a 4-bit system this would equate to -6. This can be designed quite straightforward in hardware. 

Maybe we're getting close to the *aha* moment that i spoke about earlier. If not yet let's then consider the truth table in table 1.3. Because the inputs/outputs of this arithmetic algorithm always does the same output for the same inputs, there is no reason we couldn't use the truth table. The truth table shows the four possible outcomes of adding two bits, without considering the carry just yet. The rules of the game are that the sum part can only be on if a or b are *exclusively* 1, otherwise it would result in carrying over the bit to the next position. The carry output on the other hand is 1 when both inputs are both 1. The revelation here is that these pattern of inputs/outputs follow exactly that modeled by the XOR gate and the AND gate. Therefore the simplest implementation of binary addition is to use the fundamental building blocks constructed previously. 

| a   | b   | sum | carry |
| --- | --- | --- | ----- |
| 0   | 0   | 0   | 0     |
| 1   | 0   | 1   | 0     |
| 0   | 1   | 1   | 0     |
| 1   | 1   | 0   | 1     |
Table 1.3 truth table for single bit binary addition

This logic is very simple to implement using the elementary building blocks introduced previously. 
This circuit has a particular name, the *halfadder* and represents the first of a hiearchy of arithmetic units. 
![[Halfadder.png]]
Figure 1.9 Logic diagram for the halfadder

You may have noticed that there are some cases that was not handled in table 1.3 and that is because we started with the simplest case which only holds for the very first addition of digits, where no carry input from the previous calculation is considered. This simplification is removed now and table 1.4 shows the truth table for the entire problem. The second pair of digits may also need to handle a carry from the previous addition and thus there are three inputs into the binary addition, a, b and a *carry*. 

| a   | b   | c   | sum | carry |
| --- | --- | --- | --- | ----- |
| 0   | 0   | 0   | 0   | 0     |
| 1   | 0   | 0   | 1   | 0     |
| 0   | 1   | 0   | 1   | 0     |
| 0   | 0   | 1   | 1   | 0     |
| 1   | 1   | 0   | 0   | 1     |
| 1   | 0   | 1   | 0   | 1     |
| 0   | 1   | 1   | 0   | 1     |
| 1   | 1   | 1   | 1   | 1     |
Table 1.4 Truth table for multibit binary addition
![[FullAdder circuit.png]]
Figure 1.10 Logic diagram for the fulladder 
This logic diagram is called the *fulladder* and you may be able to convince yourself again that this can be built from the elementary logic gates. The final part of the hiearchy of adders is the multibit adder or *ripple-carry-adder*. By sequencing *n* number of full adders, it's possible to add up any number of bits. 
![[RIpple carry adder.png]]
Figure 1.11 Logic diagram for the ripple-carry-adder

Now we have we have system which can perform the primitive operation of adding two numbers of any size. What else may we be able to implement using logical operators? Consider the combinational logic in the figure 1.12. The capability here is to compare two inputs a and b of *n* bits, bit by bit. This is called a bitwise AND operation and can be used to various things such as checking if certain bits are set or zeroing a input. 
![[Bitwise AND operation.png|center]]
Figure 1.12 combinational logic for bitwise AND
A comparitor can be implemented for example by using XNOR gates. Figure 1.13 shows a 4-bit comparitor, that can be extended to compare any *n* number of bits. 
![[4-bit comparitor.png|center]]
Figure 1.13 Combinational logic for comparetor functionality

Before building larger archictetural units, a set of chips called multiplexers and decoders needs to be introduced. The functionality of these are going to be apparent in the next layer of abstraction, but for now you just have to trust me on that. A multiplexer offers a mechanisms for *selection*. The simplest multiplexer is a 2-to-1, which means one of two data inputs gets propagated to the output terminal. In general a multiplexer is constructed to take *n* number of inputs and *log(2)n* selector bits. A truth table for a 2-1 multiplexer is shown in table 8 and in this case when the selector bit is 0, the D<sub>0</sub> is outputtet, and vice versa. 

![[Truth table 3-8 decoder.png]]
Table 1.5. Truth table for 2-to-1 multiplexor
Take a look at the following diagram and trace the input from a and b to the output and confirm that it is the case that the selector bit *s* controls the output such that when on, the a is output is propogated and when off the b output is propogated. 

Figure 1.14 Combinational logic for 2-1 multiplexer

As with other combinational units, this one can be boxed in and serve as an interface for the hardware designer. 
![[2-to-1 multiplexer.png|center]]
Figure 1.15 2-to-1 multiplexer module

Decoders work by recieving *n* inputs and outputting a signal to one outputs. For example the 2-to-4 decoder takes two inputs and selects among four outputs. A 3-to-8 decoder does the same but instead with 3 input bits have the possibility of choosing between eight output lines. 
![[3-8 decoder.png|center]]

Figure 1.16. Combinational logic 3-8 decoder as module

Why is this so useful? There are many uses of this functionality and it will become more evident later. But for starters this may be a mechanism for selecting a single address in memory or to decode the opcode of an instruction. This combinational logic is one of the modules that enable versatility in computers as the same chip can be used for a range of tasks by letting a chip like a decoder control the setting of it. 

## The arithmetic and logic unit
Now we can construct an **ALU**. This is an very important component in any computer. Von Neumann had the ALU as a core part of this architecture in his seminal paper as a part of the CPU. 

![[ALU]]
The function f is one out of family of functions, that controls what operation that ALU should be doing on the inputs. How much functionality is part of the ALU is an important design question for any CPU design. There is a trade-off here because many functionalities can be implemented in software a later stages such as multiplication and division algortihms. 
### The Hack ALU
Now the above is true for all ALU's across devices. Now we're going to look at the specific ALU for the Hack platform.

![[The Hack ALU.png]]

* Operates on two 16-bit two's complement values
* Outputs a 16-bit two's complement value
* Which function to compute is set by six 1-bit inputs
* Computes one out of a family of 18 functions
* Also outputs two 1-bit values or control signals

To compute a particular function, set the six control bits according to the following specification, which is the machine language specification of Hack. 

The functions are quite easy to implement such as 
* Set a 16-bit value to 000000000
* Set a 16-bit value to 111111111
* Negate a 16-bit value (bit-wise)
* Compute + or & on two 16-bit values

As leonardi divinci said "Simplistic is the ultimate sophistication" so keep it simple, go slow and do things right. 
## The incrementer
The computer has functionality that let's you increment a number. As we shall see later this becomes important for program executions. To build a 16-incrementer that takes a input as a 16-bit word and increments it by 1. the following parts are needed. 







