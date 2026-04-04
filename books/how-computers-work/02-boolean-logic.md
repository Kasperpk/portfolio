# Boolean Logic and Digital Building Blocks

Earlier we introduced the register machine, a computational model closely related to Turing's universal a-machine. Such machines operate by executing primitive instructions over symbolic states. By composing a small number of simple operations in arbitrarily long sequences, they are capable of expressing complex programs. Turing's key insight was that computation could be realized by combining very simple components and sequencing step-by-step instructions. 

The next challenge faced by von Neumann and his contemporaries was therefore not theoretical but practical: how can such simple operations such as add, subtract, move, halt and copy be implemented in physical machinery? The answer emerged from an unexpected direction — 19th century mathematical logic.

One of the most influential contributors was **George Boole**, who developed a novel branch of algebra now known as **Boolean algebra**. Boole's goal was ambitious: to express reasoning itself in algebraic form. He proposed that logical statements could be reduced to binary outcomes — **true or false** — and manipulated using algebraic rules. While originally philosophical, this idea would later become the mathematical foundation of digital computing.

Boole introduced a small set of fundamental logical operations:
- AND 
- OR 
- NOT 

These operators allow logical relations to be expressed compactly. A useful way to understand Boolean expressions is through **truth tables**, which enumerate all possible inputs and their corresponding outputs. Truth tables are not merely pedagogical tools — they serve as blueprints for real circuits. Table 1.1 shows a truth table for the AND operation with inputs A and B. 

| A   | B   | A ∧ B |
| --- | --- | ----- |
| 0   | 0   | 0     |
| 0   | 1   | 0     |
| 1   | 0   | 0     |
| 1   | 1   | 1     |

Table 1.1 Truth table for a simple AND operation

The other primitive operators could similarly be represented using truth tables and when it comes to designing electronic and digital systems each logical operator has it's own symbol. The universal symbols and truth tables of the most elementary logic gates include extensions beyond the primary operators AND, OR and NOT. The extended set of logic gates are essentially all that is needed to build the complex digital systems that run computers. It's also here that we meet the first important layer of abstraction. These logic gates acts as an abstract layer ignoring how they have been materialized using actual physical and electronic components. This idea of abstraction is going to be very important for the rest of the book but also if you are going to work on professional projects in software or hardware. What's also important here is that the NOR, NAND, XOR gates can be built from the primitive gates and so these are the first **combinational units** introduced. These gates are going to be important in the design of more sophisticated units that are going to be able to perform arithmetic on binary numbers. 

Having looked at boolean logic and the elementary digital building blocks that was inspired by Boole's work we are now going to study the physical implementation of those fundamental building blocks.
