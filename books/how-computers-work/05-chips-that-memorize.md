Many of the first computers were hardwired to run a specific program and did not have memory which to store programs. A lot have changed since then and in order to design something that looks like the all-purpose computer we know today, we need to be able to persist bits of data and instructions and switch those bits out to run another program. This is the idea of the stored program. The physical implementation of memory have had many versions throughout history just like the computer itself. Some of the earliest storeage devices i can remember where the floppy disks, CD-ROMs and USB storage. Even before that programs may be stored on something called mercury delay lines, cathode-ray tubes or rotating magnetic disks. The semiconductor invention had similar effect on the memory part of the computer with the introduction of semiconductor dynamic random-access memory (DRAM) integrated circuits in the 1970s. More recently the advent of cloud storage have paved the way for words like *big data* and cloud datawarehouses. Modern computers host memory that forms a hiearchy from the slowest and largest memory, to the smallest and fastest cache memory. Having quick access to data and instruction requires it to be located close to the CPU, which is not possible for large amounts of data, and so therefore engineers have tried to make the best of both worlds by creating a hiearchy to meet all needs. This is quite genious because programs tend to access the same data again and again and so computers have clever algorithms to locate frequently or recently used data in the cache, such that it can quickly be recomputed. Probably you have observed this magic when you have opened up a recently closed browser or something like that. To understand how this memory hierarchy works at the fundamental level, we need to examine the basic building blocks that make memory possible.

**S-R latches and flip-flops**
Combinational logic—the gates and circuits we’ve built so far—behaves a bit like a calculator: give it inputs, and almost instantly you get outputs. But computers are more than fancy calculators; they are _machines with memory_. They need to remember yesterday’s inputs to decide today’s outputs. This is where **sequential logic** comes in: circuits whose behavior depends not only on what you feed them now, but also on what they stored before.

Think of it as the difference between looking at a single frame of a movie versus following the story across time. Sequential logic gives circuits that sense of _history_. Without it, computers could never hold onto variables, count, or even step through instructions. In order to develop this temporal ability to maintain state, we must extend our computer architecture with a time dimension. At the heart of this idea is the simplest kind of “memory cell,” a circuit that can store one bit: a **latch**. The most basic example is the **S–R latch**, built from two NOR gates feeding into each other. At first glance, it looks like a tangle, but the cleverness is that its output can _persist_. Once you tell it to “set,” it stays set until you explicitly “reset” it, much like a sticky note that won’t disappear when you look away.  Figure 1.x shows an S-R latch built from two NOR gates.

![[S-R Latch.png|center]]
1.18 S-R latch combinational logic
Let's refresh our memory on how a NOR gate behaves. 

| A   | B   | Y   |
| --- | --- | --- |
| 0   | 0   | 1   |
| 1   | 0   | 0   |
| 0   | 1   | 0   |
| 1   | 1   | 0   |
Table 1.7 Truth table for NOR gate
Now consider the the following scenarios: R is 1 and S is 0. Looking at the top gate, we know that if just any of the inputs are on, then the output will be off. So Q = 0 no matter what, that also goes for S = 1. Let's summarize this

| R   | S   | Q   |
| --- | --- | --- |
| 1   | 0   | 0   |
| 1   | 1   | 0   |
Table 1.8 Partial truth table for S-R latch

Now if S = 1 and R = 0 then the bottom will output off, because S is on and since R is also off, Q will be on. Now if we turn S off will that change Q? Look at the output from the top gate that flows into the bottom gate. At the moment before turning off S, it will output a on signal that flows into the bottom gate, that means even if we turn off S the bottom NOR gate will still be off and consequently both inputs to the top gate be off. Q is persisted! 

| R   | S   | Q               |
| --- | --- | --------------- |
| 1   | 0   | 0               |
| 1   | 1   | 0               |
| 0   | 1   | 1               |
| 0   | 0   | Q<sub>t-1</sub> |
Table 1.9 Truth table for S-R latch

t's now possible to walk away from this circuit for months or days, come back and still observe the previous state for the Q value. This is the "magic" of the sequential logic behind digital storage. There are some extra things, that needs to be added to make this a practical memory cell. First there needs to be some mechanisms to control, when the circuit will latch on to an input or not. That's how real memory units work, they have load or enable signal that enables it for writes. Such a load signal is added to the module by using a multiplexer, that chooses between the previous output or the data input and may be considered a single-bit register.  Figure 1.19 shows how the inputs and outputs may be have for arbitrary values of input and load signals over five discrete clock cycles. Notice that the load and input signal needs both to be 1 for the output to emit 1 on the next clock cycle. 

![[Single bit register|center]]
Figure 1.19 1-bit register that emits the input when load signal is enabled

**Synchronizing program execution**
Now there is a challenge in computers, that some data paths are longer than others. That means if we just instruct the CPU to fetch data from to memory registers and compute the sum, then there will be some fraction of seconds where the output will be garbage. For sequential units this may be even worse, because if we have the current instruction writing some data into a register and then it moves on load from that register before data has arrived, chaos will arise. The solution to this problem Is a mechanisms for synchronizing and control the machine such that we allow data and instructions to move before making computations. In figure 1.x reproduced from the elements of computing systems there is quite a good example of how such a clock creates discrete time units that control the state of a 1-bit register. In this figure the load and input signal is set to 1 initially at t<sub>0</sub>. At the next clock cycle t<sub>1</sub>, the data input is loaded into the register. Then for two three clock cycles this register remembers this 1, until it is overwritten in t<sub>4</sub> when the load signal again has been set to 1. there that mechanisms is shown. The *clock* implemented as a oscillator that "alternates continuously between two phases labeled 0-1, *low-high* or *tick-tock*". A master clock is connected to all the subsequent memory units and ultimately propagate signals all the way down to the single-bit units and "ensure that the chip will commit to a new state, and output it, only at the end of the clock cycle." The cycle length is an important parameter for computer designers as it needs to allow for the longest possible path to take place, before progressing in the program. 

**From Bits to Blocks: Building Larger Memory**
A single flip-flop stores one bit. How do we scale up from a single flip-flop to a memory system big enough to hold an operating system, a browser, and your latest video stream all at once? The next component that can be constructed now is a *register*. A register is a group of these 1-bit registers that share a common clock and enable signal. The memory closest to the CPU are often implemented as a *register file*, a group of registers that are read and written to control by a multiplexer. There are typically two types of memory used for building large memories with billions of bits needed for modern computing, we arrange them in a highly organized grid or **two-dimensional array**.
- **SRAM (Static RAM):** This is the technology used for CPU register files or caches. It is built directly from flip-flops (typically 6 transistors per bit). It's extremely fast because it doesn't need to be refreshed, but it's expensive.
- **DRAM (Dynamic RAM):** Main memory, built from cheaper **DRAM** (dynamic RAM), that stores bits using tiny capacitors that slowly leak charge, like a bucket with a pinhole in it. To keep data alive, DRAM must be constantly _refreshed_. This refresh overhead makes it slower, but because the cells are so compact, you can pack gigabytes onto a single module.

Both types are organized into arrays where each row stores a **word** of data (e.g., 64 bits). Each row has a unique **address**. When the CPU needs data from address `0x1000`, a **decoder** circuit takes the address bits, selects the one correct row out of millions, and connects it to the data bus for reading or writing. A small number of address bits can select from a vast amount of memory. With 20 bits you can name a million locations. Figure 1.x shows a sketch of such an array. It takes an *n* bit address input and from that it can select one of 2<sup>n</sup> rows or words in the memory block and either read from it or write data into it via the data bus. 

![](RAM%20array.png|center)
Figure 1.20 Memory array building block

To create an example consider tiny 4x3 memory (4 words, 3 bits each). The size of that array would then be twelve.  To select one of `4` words, the address width can be calculated as follows.
$$
log_2(4) = 2
$$
Thus way may have the following address bits.

| Address | Data |
| ------- | ---- |
| 11      | 010  |
| 10      | 100  |
| 01      | 110  |
| 00      | 011  |
Table 1.10 Truth table for S-R latch

To route data on the data bus either to or from the memory array, we need one of the combinational logic units constructed earlier, the decoder. A 2-4 decoder to be more specific. A **2-to-4 decoder** would take the address `01` and activate only the second row, allowing the data `110` to be read or a new value to be written. 

From a simple feedback loop in two logic gates, we get a latch that can store a single bit. By adding a clock for synchronization, we create reliable flip-flops and arranging millions of these into a grid with an address decoder gives us the SRAM that powers ultra-fast CPU caches. A different, more compact design gives us the massive DRAM for main memory and by intelligently managing these different tiers in a hierarchy, a computer provides the illusion of a single, vast, and incredibly fast memory space, making our powerful modern software possible. 

**Clocks and concept of time**
I mentioned that all these chips were connected to a *master clock*. So far we have assumed that chips respond instantaneously: you input 7,2 and “subtract” into the ALU and poof the ALU output becomes 5. In reality outputs are always delayed due to the time it takes for the signal to propagate. Secondly computations take time and the more chips the more time it will take for the chip’s outputs to emerge fully from the chip’s circuitry. 


Time allows us to synchronize the operations of different chips across the system. If for example we ensure that the time delay designed allows gate outputs to stabilize we can ensure correct program executions. Cycle length is one of the most important design parameters as it has to be longer than the maximal time delays that can occur. Current technology allows us to create cycles as tiny as a billionth of a second, achieving remarkable computer speed. 

