# Theoretical Computer Science

**The bottom of things**

The headline above echoes a remark by the physicist Richard Feynman, who in the late 1950s spoke about the future of computing and the power of building complex systems from extremely simple parts. At that time computers were still rare machines and the field itself was young. Only a small number of researchers were beginning to explore what these devices might become.

Among the most important of them was Alan Turing. In the 1930s Turing proposed a simple theoretical device that later became known as the _Turing machine_. The machine itself is austere: a tape, a head that reads and writes symbols, and a small set of rules that determine how it moves. Yet this spare construction captured something profound. It provided a precise model of what it means to compute.

The philosopher Daniel C. Dennett reflects on this idea in an interlude on computers in his book _Intuition Pumps and Other Tools for Thinking_. Dennett explains Turing's insight by drawing an analogy with the brain. Complex competences, he argues, can arise from very small and mindless components when they are connected in the right way. Individual neurons are simple cells. Yet when billions of them interact through structured networks they produce what Dennett calls _wonder tissue_ — the remarkable abilities of perception, thought, and imagination.

The same principle appears in the theory of computation. A system built from extremely simple operations can nevertheless perform astonishingly sophisticated tasks. What looks magical at first glance often turns out to be the patient accumulation of tiny, mechanical steps.

Modern computer systems are immensely complicated, but they are not magical. If we wish, we can descend through their layers of abstraction and see exactly what happens at every step.

This is the path we will follow. We begin at the conceptual foundations of computation and gradually climb toward the systems we interact with every day.

Computing now surrounds us. The devices in our pockets, on our desks, and even on our wrists rely on software executing billions of instructions each second. Words such as _software_, _hardware_, _bandwidth_, _gigahertz_, _artificial intelligence_, and _cybersecurity_ have entered ordinary language. We often carry a vague sense of what these terms mean, though in many cases the underlying mechanisms remain obscure.

To understand them properly we must begin from the ground up. A helpful starting point is the _register machine_, a simple computational model discussed by Dennett in his chapter _The Seven Secrets of Computer Power_.

A register machine consists of a collection of registers and a processing unit. Each register has an address and can hold a number. The processing unit executes an extremely small instruction set consisting of only three operations:

- **end**, which halts the machine
- **increment**, which adds one to the value in a register and proceeds to the next instruction
- **decrement**, which subtracts one from a register, unless the register already contains zero, in which case the machine branches to another instruction

At first glance such a machine seems almost useless. With only three primitive operations it appears incapable of performing any interesting task.

The surprise is that it can compute anything a modern computer can compute.

Even simple arithmetic can be implemented mechanically. Suppose we want to add the contents of two registers. We repeatedly decrement the first register and increment the second until the first register reaches zero. At that moment the machine branches to the halt instruction, leaving the result in the second register. As Dennett remarks, the machine has now added two numbers together _without knowing what numbers are or what addition means_.

From these tiny primitives we can build increasingly sophisticated routines. By combining increment, decrement, and branching we can implement subtraction, copying, comparisons, and eventually entire algorithms.

Once such routines are defined they can be reused and combined. Repetition and composition gradually give rise to more powerful procedures: multiplication through repeated addition, averaging values across registers, or computing more elaborate numerical functions.

Anything that can be represented as numbers can also be stored in the machine's registers. Images, text, sound, memory addresses, and instructions themselves are ultimately encoded as sequences of numbers. Computers do not literally read or understand these symbols, but they can manipulate them with extraordinary reliability. As Dennett puts it, computers can _sort of read_, and that modest competence turns out to be enormously powerful.

When we store instructions inside the machine's memory we obtain what is called a **stored-program computer**. The machine can now execute any sequence of instructions encoded in its registers.

From the programmer's perspective this process appears as a chain of translations. A high-level programming language is translated into assembly instructions, which in turn are encoded as machine code — long sequences of zeros and ones that the hardware can execute directly.

This idea lies at the heart of modern computing. Alan Turing described a _universal machine_ capable of reading instructions stored in its memory and executing them one by one. Every modern computer is, in essence, an implementation of this concept.

What has changed since Turing's time is not the fundamental idea but the scale and efficiency with which it is realized. Improvements in hardware, miniaturization, and architecture have allowed computers to execute these simple operations billions of times per second.

In the chapters that follow we will explore the layers of this remarkable system — an intellectual and technological achievement built on the insights of thinkers such as Turing and the engineers who followed him.
