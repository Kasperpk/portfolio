# Introduction to Computer Science

> "The programmer does not differ from any other craftsman: unless he loves his tools it is highly improbable that he will ever create something of superior quality" (Edsger W. Dijkstra)

Dijkstra wrote this in his 1962 *meditations on advanced programming*, work i stumpled upon as i was transitioning into my first professional role. It struck me quite profoundly as i was coming into my first professional job out of university. I became a part of a data team and was quite technical for someone graduating with a business degree. Growing up in the 2000s and 2010s i've been accustomed to engaging with computers using the easy-to-use and intuitive interface. As i grew into i had to face many challenges and it's where i realized that there is a lot of depth below that surface level interface. Some of my colleagues could build things and talk about things that i would struggle to pick up and that was difficult for me at times. I noticed at this time that 95% of my work was done using computers a tool that i barely understood beyond simple clicking around. There was a lot of frustration and with my work becoming more technical i faced the feeling that i was in over my head with the tools i was now using and not understanding a thing of what was going on. I decided to let some of my frustration fuel curiosity about the tool i was using 95% of the time and began studying and reading about computers and computer science. I read about the history of computing and that's when i met with Dijkstra's work, one of the first professional computer scientist who worked in the early era of digital computing where many breakthroughs is the reason we have the sophisticated tools we sit with today. I studied how computers where designed and how to program them and got to know people like Alan Turing, Richard Feynman and Von Neumann. As i was reading and studying i experienced that the relationship to my work and the computer changed. I felt more comfortable using the machine and i was more forgiving when encountering new things and perhaps some unexpected errors. This is when Dijkstra's opening quote began to resonate with me as i felt a newfound appreciation for the number one tool i was using to do my work. In this book we go on the amazing discovery of computers starting at the bottom of things and the idea that inspired the modern computing systems we use today.
## The birth of computer science
In the late 1950s Richard Feynman spoke about the future of computing and the power of building complex systems from extremely simple parts. At that time computers were still rare machines and the field itself was young. Only a small number of researchers were beginning to explore what these devices might become. Among the most important of them was Alan Turing. In the 1930s Turing proposed a simple theoretical device that later became known as the _Turing machine_. The machine itself is austere: a tape, a head that reads and writes symbols, and a small set of rules that determine how it moves. Yet this spare construction captured something profound. It provided a precise model of what it means to compute. The philosopher Daniel C. Dennett reflects on this idea in an interlude on computers in his book _Intuition Pumps and Other Tools for Thinking_. Dennett explains Turing’s insight by drawing an analogy with the brain. Complex competences, he argues, can arise from very small and mindless components when they are connected in the right way. Individual neurons are simple cells. Yet when billions of them interact through structured networks they produce what Dennett calls _wonder tissue_—the remarkable abilities of perception, thought, and imagination.

The same principle appears in the theory of computation. A system built from extremely simple operations can nevertheless perform astonishingly sophisticated tasks. What looks magical at first glance often turns out to be the patient accumulation of tiny, mechanical steps. Modern computer systems are immensely complicated, but they are not magical. If we wish, we can descend through their layers of abstraction and see exactly what happens at every step. This is the path we will follow. We begin at the conceptual foundations of computation and gradually climb toward the systems we interact with every day. Computing now surrounds us. The devices in our pockets, on our desks, and even on our wrists rely on software executing billions of instructions each second. Words such as _software_, _hardware_, _bandwidth_, _gigahertz_, _artificial intelligence_, and _cybersecurity_ have entered ordinary language. We often carry a vague sense of what these terms mean, though in many cases the underlying mechanisms remain obscure.

To understand them properly we must begin from the ground up. A helpful starting point is the _register machine_, a simple computational model discussed by Dennett in his chapter _The Seven Secrets of Computer Power_.

A register machine consists of a collection of registers and a processing unit. Each register has an address and can hold a number. The processing unit executes an extremely small instruction set consisting of only three operations:

- **end**, which halts the machine
- **increment**, which adds one to the value in a register and proceeds to the next instruction
- **decrement**, which subtracts one from a register, unless the register already contains zero, in which case the machine branches to another instruction

At first glance such a machine seems almost useless. With only three primitive operations it appears incapable of performing any interesting task.

The surprise is that it can compute anything a modern computer can compute.

Even simple arithmetic can be implemented mechanically. Suppose we want to add the contents of two registers. We repeatedly decrement the first register and increment the second until the first register reaches zero. At that moment the machine branches to the halt instruction, leaving the result in the second register. As Dennett remarks, the machine has now added two numbers together _without knowing what numbers are or what addition means_.

From these tiny primitives we can build increasingly sophisticated routines. By combining increment, decrement, and branching we can implement subtraction, copying, comparisons, and eventually entire algorithms.
![](Non%20destructive%20add%20function.png)
Figure 1 register machine program combining three simple instructions

Once such routines are defined they can be reused and combined. Repetition and composition gradually give rise to more powerful procedures: multiplication through repeated addition, averaging values across registers, or computing more elaborate numerical functions.

Anything that can be represented as numbers can also be stored in the machine’s registers. Images, text, sound, memory addresses, and instructions themselves are ultimately encoded as sequences of numbers. Computers do not literally read or understand these symbols, but they can manipulate them with extraordinary reliability. As Dennett puts it, computers can _sort of read_, and that modest competence turns out to be enormously powerful.

When we store instructions inside the machine’s memory we obtain what is called a **stored-program computer**. The machine can now execute any sequence of instructions encoded in its registers.

![[From high level abstraction to machine version instructions|center]]
Figure 1.1 From program to assembly to machine code

From the programmer’s perspective this process appears as a chain of translations. A high-level programming language is translated into assembly instructions, which in turn are encoded as machine code—long sequences of zeros and ones that the hardware can execute directly.

This idea lies at the heart of modern computing. Alan Turing described a _universal machine_ capable of reading instructions stored in its memory and executing them one by one. Every modern computer is, in essence, an implementation of this concept. What has changed since Turing’s time is not the fundamental idea but the scale and efficiency with which it is realized. Improvements in hardware, miniaturization, and architecture have allowed computers to execute these simple operations billions of times per second. In the chapters that follow we will explore the layers of this remarkable system—an intellectual and technological achievement built on the insights of thinkers such as Turing and the engineers who followed him.
## Modern computer science 
What started with the idea of the register machine started and theoretical computer science fathered by Alan Turing has turned into a large sciencitifc area. According to the Michigan technological university computer science is the  study of computers and computational systems. Those computational systems have become very complex and as a consequence computer science has become a very specialized with niches that studies a part of the whole field. There are specializations such as

* Algorithms and data structures 
* Software engineering
* Computer architecture
* Aritifical intelligence and machine learning
* Cyber security and networking
* Human-computer interactiond

In studying these areas we follow the advice of Dijkstra and on the way strive to become more sophisticated users by for example finding answers to interesting questions such as those presented in David A. Patterson and John L Hennesy of *Computer Organization and Design*.
* How are programs written in high-level language translated into hardware and how does the hardware perform these operations?
* What is the interface between software and the hardware, and how does software instruct the hardware to perform needed functions? 
* What determines the performance of a program, and how can a programmer improve performance?
* What techniques can be used by hardware designers to improve performance?

The authors write “without understanding the answers to these questions, improving the performance of programs on modern computers or evaluating what features might make one computer better than another for a particular application will be a complex process of trial and error, rather than a scientific procedure driven by insights and analysis.” (page 9) The authors also remark that digital systems are continuously developing which means that the programmers of 1960s and 1970s dealt with totally different challenges than programmers now. The number one constraint in the early age of computing was the constraint of limited computer memory. Programmers now should understand that this motivated replacement of the simple memory model of the 1960s. Understanding where we come from allows us to better gauge where we are heading, which can be important for anyone with a technical role. Understanding these details is what it means to become a craftsman. There is also a sense of hightened enjoyment and appreciation for the tool which allows as Dijkstra says, one to produce the best work possible. In the coming pages we're going to embark on a voyage of breaking down computing systems into it's elements one layer of abstraction at a time as we try to regain some craftsmanship.
