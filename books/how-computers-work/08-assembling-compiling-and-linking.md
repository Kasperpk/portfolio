With the MIPS microarchitecture we have gotten a glimpse into how sequences of instructions that make up programs by moving through states controlled by the clock signal. I've kept it to performing single instructions and to understand how entire programs run, one have to imagine extending the single instruction operation billions of times. Now the next layers of abstractions really do move into the software layer something we peeked at shortly with the introduction of symbolic versions of machine language called assembly langauge. Assemblers are the first pieces of software that allows us to express programs more human friendly but there remain one more bridge to cross before the popular `print("hello world")` can be realized and that is the software piece called a *compiler*. 

Assembly although much more forgiving still require almost a one-to-one correspondance between lines of code and machine instructions. This includes many statements that seems fairly uninteresting to the programmer such as deciding which memory addresses or registers to load and write data to. The idea to an even more abstracted version of machine language began to take form in the 1950s with IBM releasing the FORTRAN language for programming scentific and engineering applications. The problem was that when FORTRAN was released there was no compiler to translate the syntax into executable code. It took a couple of years then came the first compilers having been an extremely important challenge for the computer science community to solve. Engineering compilers is a large complex and the compilers for FORTAN showed suprising sophistication. The compilers that currently operate have thousands or even million lines of code and in that sense is the first grand piece of software that we meet. 

 ## **Learnings from studying compilers**
There are possibly many learnings to discover when it comes to compilers. As mentioned the design of compilers may have been the first really complex piece of software that we meet. For anyone interested in designing software many teachings can be found studying compilers. Programmers of compilers had to write an extensive amount of code and face many challenges that any serious software encounters. For example at some point the amount of code grows so large that cramming everything into one large file becomes impossible to manage. Therefore typical compilers are built from something like fifteen to twenty modules. Each module may hold submodules that separate out specific areas of functionality within the code. These choices are important to any larger software project. Similarly the modules then have to interact something that Andrew W. Appel elaborate on in his book. He writes that

> Some of the interfaces, such as "Abstract Syntax, IR Trees and Assem take the form of data structure and passes it to the semantic analysis phase. Other interfaces are abstract data types; the Translate interface is a set of functions that the semantic analysis phase can call, and the tokens interface takes the form of a function that the parser calls to get the next token of the input program

(p. 5, Andrew W. Appel). 
He further remarks that "coming to the right abstraction by several iterations of *think-implement-redesign* is a learning experience that should not be missed." Keith D. Cooper the author of engineering a compiler backs up Andrew's clam that the design and implementation of a compiler "is a substantial exercise in software engineering" (p. 4 Keith D. Cooper). Thirdly the actual implementation of code within those modules are tied to other ares of applied computer science. For example in language theory where Keith lists the examples of "text searching, website filtering, word processing and command-language interpreters" (p. 5 Keith D. Cooper) Is applied in artificial intelligence. Implementing these in code testes ones ability design efficient algortihms and using appropiate data structures, a fundamental part of computer science and solving programming challenges in general. Were compilers not implemented efficiently it would be detrimental to performance and so many great ideas have been spawned out of necessity for efficient algorithmic. For exampel some greedy algorithms, heuristic search, graph alogrithms, dynamic programming, finite automata have come to deal with problems "such as dynamic allocation, synchronization, naming, locality, memory hiearchy management and pipeline scheduling" (p. 4, Keith D. Cooper). We are going to return to the topic of algortihms in the next section but for now let's see more closely how compilers are designed.   
## Compiler structure
Compiler designs are as mentioned modular and in general follow design principles separating it into a 
* Front-end (scanning and parsing)
* Optimization
* Back-end (code generation)

What Keith calls the front end of the compiler is the process of scanning and parsing the source program to check if it adheres to the finite set of grammatic rules in the language. In the English language for example many sentences are constructed as *"Subject verb Object endmark"* (p. 11, Keith D. Cooper). Keith uses the example sentence "Compilers are engineered objects." The very first step involves scanning this sentence and recognizing the distinct words or tokens and classify them. Are they verbs, nouns or any other part of the speech? This is the job of the scanner, and is also called lexical analysis. In this case lexcial analysis would produce the sequence "(noun, "Compilers), (verb, "are"), "(adjective, "engineered"), (noun, "objects"), (endmark,".")" (p. 11, Keith O. Cooper). 

Once the scanning has been done, a *parser* will check if the syntax follow the rules of the language. Every high level programming language needs to have some grammar. For example does the language have some way of expressing comments? Does it allow for whitespace? In general there will be a set of rules that the parser will be checking. For example a program like the one in code example 1.7, an example of a python function declaration, the parser will recognize the reserved keyword *def*. It recognizes the *def* statement and know that the following token should follow the rules of function declaration, *functionDeclaration(arguments):*. The argument should follow the rules of argument declaration and so on. 

Code example 1.7 Function definition program python
```
def addNumber(x,y):
	z = x + y
	return z
```
If the parser meets wrong code like code block 1.7, it will detect it and return and error message to the programmer. 

Code example 1.8 Function definition with illegal syntax
```
def addNumber{x,y:5):
	z = x + y
	return z
```

### **Front end: scanning source files**
*Regular expressions* are typically used to generate scanners as these allows for writing expression that matches certain strings that are encountered. *microsyntax* is the word Keith uses to describe the lexical structure of the input programming language. "This microsyntax specifies how to group characters into words and, conversely, how to separate words that run together. In English for example the microsyntax is straightforward. Adjacent alphabetic letters are grouped together, left to right to form a word, a blank space terminates a word, as do most nonalphabetic symbols" (p. 26, Keith D. Cooper). The words that are encountered can then be validated using a dictionary lookup. Programming languages similarly have microsyntax. Identifiers are words that can take any number of characters and some of these are special *keywords* that are reservered. For example *while* and  *static* are keywords in C and Java. *def*, *for*, *return* are similar examples of keywords in Python. One way to diagrammatically show this process is to use transition state diagrams. Figure 4.1 shows such a transition state diagram with three accepting states s<sub>3</sub>, s<sub>5</sub> and s<sub>10</sub>

![](Sketches/Transition%20state%20diagram.png)
Figure 4.1 Reproduction of transition state diagram recognizer of new, not and while (page 29, Keith O. Cooper)

It could also be expressed mathematically with a formalisms know as *finite automata.* The set of words accepted by a finite automaton, *f* forms a language (p. 34, Keith D. Cooper). This expression is though not quite intuitive for people and it may be useful to instead describe the language using *regular expression language*. For example if there is a rule that *an unsigned integer is either a zero, or a nonzero digit followed by zero or more digits* than a regular expression can be written to match that. [0-9]* where the * sign means zero or more occurrences of a digit between 0 and 9, the digits available in the decimal number system. Regular expressions are typically used to construct efficient scanners that can group a source file into it's lexical elements or tokens. The next phase of the front-end is called *parsing*.
### **Front end: parsing**
Once the source code is scanned, the next stage is parsing. The parser gets the transformed and scanned source code, that have identified tokens and their catagory (part of speech). It then determines if the program adheres to the grammatic rules of the language. Before a parser can be constructed, there needs to be a formal specification of the source language and a method for determining "membership" (p. 84, Keith D. Cooper). Keith describes how by restricting the source language to a "set of context-free languages, we can ensure that the parser can efficiently answer the membership question." (p. 84, Keith D. Cooper). Assigning membership is question to which many algorithms have been proposed. For example top-down parsing *recursive-descent* and LL(1) parsers, bottom-up or canonical parsers. Context-free grammar *G* is a set of rules that describes how to form valid sentences which is a string of symbols. One way to write this is using the following format

*SheepNoise* -> baa *SheepNoise* | baa
The first rule or production reads "SheepNoise can derive the word baa followed by more SheepNoise" (p. 86, Keith). SheepNoise is a syntactic variable here used to represent all set of strings that can be derived from the grammar, also called a *nonterminal symbol*. Rule 1 states that valid strings can be a valid string followed by another valid string represented with the nonterminal symbol. Rule two is recognizing a valid string and so all valid strings in some grammar are derived by zero or more applications of rule 1, followed by rule 2. 

**Parse trees**
This SheepNoise grammar is too simple to what CFGs need and instead we use another representation. Keith considers the sentence a + b x c. How could this sentence be parsed? One way to go about this is to use a **tree**. Figure 4.2 shows a tree, a data structure that consist of one or more nodes, organized into a hierarchy. It has one root, the top and each of the other nodes have a unique *parent. 

![[Sketches/Parse tree]]
Figure 4.2 Parse tree for mathematical expression

These parse trees can become increasingly complex, but are capable of expressing the way a parser could interpret a sentence. This top-down approach can be implemented algorithmically using recursive-descend algorithms, an efficient algorithms for languages with grammers that are LL(1). LL(1) means that looking one-word ahead is sufficient to validate the syntax of the sentence. Because very efficient algorithms exists for this type of grammar, it has become popular among many high-level programming languages. 

The first phase or the front-end of compiling involves these two broad steps, scanning and parsing. This has caused compiler designers some challenges already with lexical analysis and context-free-grammar and *recursive-descent* algortihms as efficient solutions to those. Thus we start by scanning the source program, grouping characters into tokens and categorizing them. Following that, tokens are parsed recursively from left to right, top to bottom making sure it fulfills the contract of the grammar of the programming language. 
### **Practical view for programmers**
Compilers look at your program to make sense of it, hence scanning and parsing. If it can will continue the process of optimizing the code, and then generate intermediate versions of it. Randal E. Bryant and David R. O'Hallaron have dedicated one chapter to *linking* in their work *Computer Systems, A Programmer's Perspective*. It offers a similar but perhaps more practical view for programmers on what compiling entails more so than designing one from the ground up as described by Keith. I want to make this transition because studying the design of compilers quickly becomes very technical and deroutes us away from the agenda. While linking is really what happens at the final stage of manipulating source code files into fully executeable, Randal and David describes the intermediate steps in ways that offers several insights that are relevant to the programmer. With focus on the C programming language they show how the source program starting from the .c extension gets compiled into  .i -> .s -> .o versions. 

To compile a C source file a compiler driver such as the GNU is needed. This driver invokes the language preprocessor, compiler, assembler, and linker. As an example the following commands can be passed to the command line interface if the GNU is installed and a C program has been written in the current directory.

Code example 1.9 compiling a C program
```
gcc -o FirstCProgram FirstCProgram.c
```

The C program in FirstCProgram contains the following source code in code example 1.10. It simply defines a function *main* and prints the string "Hello World!" and a rounded up version of the number 1.4. The program can be loaded into memory and executed with the ./Program command. This command for the FirstCProgram and it's output is shown in the code example 1.11.   

Code example 1.10 simple C program
```
#include <stdio.h>
#include <math.h>

int main() {
    printf("Hello World!\n");
    printf("%f", ceil(1.4));
    return 0;
}
```

Running the command ./FirstCProgram, invokes the operation systems *loader* function that copies the code and data into memory and transfers control to the beginning of the program.

Code example 1.11 Loading and running C program from memory
```
./FirstCProgram

Hello World!
2.000000
```

This program is not particularly useful, but what is interesting is to inspect the compilation process and the GCC compiler collection offers ways to inspect the intermediate files. Code example 1.12 shows a command to save intermediate file versions.

Code example 1.12 Saving intermediate files of a C program.
```
gcc -Wall -save-temps FirstCProgram.c -o FirstCProgram
```
The first version being the .i file, is not particularly interesting. It's a preprocessed file that contains a long series of commands ending with the lines of code as they were written in C. 

The .s file is more interesting. It contains the assembly version of the high-level program. Inspecting the assembly code reveals that even a simple program written with four lines of code in C requires many low level operations. In all it's extended to something like seventy lines of code as shown in code example 1.13. The interesting thing is that one can see that a program like this is expressed using familiar low-level operations like move, subtract and add operations. There are also some other operations that i haven't covered specifically like push, leaq but all of them are part of the instruction set architecture of the hardware. 

Code example 1.13: Assembly version of C program
```
	.file	"FirstCProgram.c"
	.text
	.def	printf;	.scl	3;	.type	32;	.endef
	.seh_proc	printf
printf:
	pushq	%rbp
	.seh_pushreg	%rbp
	pushq	%rbx
	.seh_pushreg	%rbx
	subq	$56, %rsp
	.seh_stackalloc	56
	leaq	48(%rsp), %rbp
	.seh_setframe	%rbp, 48
	.seh_endprologue
	movq	%rcx, 32(%rbp)
	movq	%rdx, 40(%rbp)
	movq	%r8, 48(%rbp)
	movq	%r9, 56(%rbp)
	leaq	40(%rbp), %rax
	movq	%rax, -16(%rbp)
	movq	-16(%rbp), %rbx
	movl	$1, %ecx
	movq	__imp___acrt_iob_func(%rip), %rax
	call	*%rax
	movq	%rbx, %r8
	movq	32(%rbp), %rdx
	movq	%rax, %rcx
	call	__mingw_vfprintf
	movl	%eax, -4(%rbp)
	movl	-4(%rbp), %eax
	addq	$56, %rsp
	popq	%rbx
	popq	%rbp
	ret
	.seh_endproc
	.def	__main;	.scl	2;	.type	32;	.endef
	.section .rdata,"dr"
.LC0:
	.ascii "Hello World!\12\0"
.LC2:
	.ascii "%f\0"
	.text
	.globl	main
	.def	main;	.scl	2;	.type	32;	.endef
	.seh_proc	main
main:
	pushq	%rbp
	.seh_pushreg	%rbp
	movq	%rsp, %rbp
	.seh_setframe	%rbp, 0
	subq	$32, %rsp
	.seh_stackalloc	32
	.seh_endprologue
	call	__main
	leaq	.LC0(%rip), %rcx
	call	printf
	movq	.LC1(%rip), %rax
	movq	%rax, %rdx
	movq	%rdx, %xmm0
	movapd	%xmm0, %xmm1
	movq	%rax, %rdx
	leaq	.LC2(%rip), %rcx
	call	printf
	movl	$0, %eax
	addq	$32, %rsp
	popq	%rbp
	ret
	.seh_endproc
	.section .rdata,"dr"
	.align 8
.LC1:
	.long	0
	.long	1073741824
	.ident	"GCC: (tdm64-1) 10.3.0"
	.def	__mingw_vfprintf;	.scl	2;	.type	32;	.endef
```

Notice that the C program contained the function ceil() and that it imports the includes the math.h file at the top of code. What the compiler needs to do is combine these files into the source code, known as linking. In this case a math module contains functions like rounding a fractional number. Each of the files are compiled separately to .o files or *relocatable object files* before they get linked into a fully executable object file, shown here in figure 4.3

![[Sketches/Static linking|center]]
Figure 4.3 Static linking: The linker combines two relocatable object files to form an executable object file prog 

The relocatable object files are sequences of bytes following the ELF (Executable and Linkable Format) standard. The ELF header contains important information about the system that generated the file, including:
* Object file type (relocatable, executable or shared)
* The machine type (x86-64)
* The offset of the section header table, and the size and number of entries in the section header table
* The locations and sizes of various sections as described in the header table

![[01 Computer engineering and architecture/sketches/EFL format rof explanation]]
Figure 4.4 ELF relocatable object file format

Inside each section are things like the actual machine code of the compiled program, read-only data and jump tables. Initialized global and static variables are in the data section. The BSS section holds uninitialized global and static variables — these are merely placeholders that will first at runtime be allocated to memory, while initialized global variables are allocated at compile time.

A **static library** like the math library is a package of related mathematical object modules. This package can be supplied to the linker and the linker can copy the modules that are referenced in the source code. This idea is quite elegant as otherwise the compiler would need to recognize all functions. Instead application programmers can import the modules into their program and the linker ensures that the object files are combined.

![](01%20Computer%20engineering%20and%20architecture/sketches/Linking%20with%20static%20libraries.png)
Figure 4.5 Linking with static libraries

Randal and David goes on to spend time on two important aspects of what linkers are responsible for handling: *symbol tables* and *relocation*. 

**Symbol tables**

High-level programmers use symbols such as identifiers for defining functions and variables — those which the scanner is responsible for identifying. These symbols have to be tracked and allocated to specific parts of memory, such that at runtime the program will reference those memory addresses. This is done by the symbol table, which is generated at the assembler step.  

Randal and David explain that there are three types of symbols: 
1) The global symbols that are defined in some module *m*, and can be referenced by other modules. 
2) Global symbols that are referenced by module *m* but defined by some other module.
3) Local symbols that are defined and referenced exclusively by module *m*. These correspond to static variables and functions. 

Symbol tables are contained in a special section called the .symtab of the .o file that the assembler generates. This symbol table contains an array of entries for each symbol, with each entry following this format:

![](01%20Computer%20engineering%20and%20architecture/sketches/ELF%20symbol%20table%20entry.png)
Figure 4.6 ELF symbol table entry format

The value is the offset from the beginning of the section where the object is defined. For executable object files, the value is an absolute run-time address. Below is an inspection of three entries from a symbol table for a program that creates an array and performs a sum on its elements using a sum function:

![](01%20Computer%20engineering%20and%20architecture/sketches/Symbol%20table%20entry%20examples.png)
Figure 4.7 Symbol table entry examples

The linker ensures that each symbol has a unique reference point. The local variables are quite straightforward as it is ensured that each has a single definition within the local module. Global symbols can be more tricky because the linker needs to make sure no duplicates exist of global variables and functions across shared modules. In general the following rules apply:

![](01%20Computer%20engineering%20and%20architecture/sketches/Linker%20resolving%20duplicate%20symbol%20names.png)
Figure 4.8 Linker rules for resolving duplicate symbol names

**Relocation**

Once the symbol table has been resolved and handled, each symbol reference has exactly one symbol table entry in one of its input object modules. At this point the linker knows the exact size of the code and data sections in its input object modules. It can now perform relocation. (p. 725, Randal E. Bryant and David R. O'Hallaron) This entails:
1) Relocating sections and symbol definitions
2) Relocating symbol references within sections.

![[Sketches/Relocation]]
Figure 4.9 Merging sections and symbol definitions of multiple relocatable object files into a fully linked executable object file.

It merges the sections into a combined section. To relocate symbols it means providing an actual run-time address to the entries in the symbol table. These are relocated by creating relocation entries, placed in the object relocation file sections .rel.text and .rel.data. These operations require efficient algorithms as hinted to by Keith in his introduction to compiler design. The pseudocode for how relocations are performed — depending on whether the reference uses a PC-relative or absolute address — is shown below:

![](01%20Computer%20engineering%20and%20architecture/sketches/Relocation%20algorithm.png)
Figure 4.10 Relocation algorithm pseudocode

**Loading executable object files**

Now when the program is loaded into memory it will have a structure like the one shown in figure 4.11. This is how the program's data is divided into different segments, with the code itself in another part of memory.

![](01%20Computer%20engineering%20and%20architecture/sketches/Run-time%20memory.png)
Figure 4.11 Linux x86-64 run-time memory image

Running the command `./prog` invokes the operating system's *loader* function, which copies the code and data into memory and transfers control to the beginning of the program.

**Dynamic linking**

If you write your own modules, you can link them using *dynamic linking*. Rather than copying object code from a library into the executable at compile time, dynamic linking defers this to load time or even run time. The figure below shows the internal operations of what happens when linking two files into a single fully linked executable in memory:

![](01%20Computer%20engineering%20and%20architecture/sketches/Dynamic%20linking.png)
Figure 4.12 Dynamic linking

At runtime when the program is *loaded* into memory, the linking takes place as the data and code is copied into an allocated memory segment. This is the mechanism behind shared libraries — on Windows these appear as .dll files, on Linux as .so files. Multiple programs can share one copy of the library in memory rather than each embedding their own copy, which is one of the key motivations for dynamic linking.

**Inspecting the pipeline yourself**

The GCC toolchain exposes the intermediate steps of the pipeline for inspection. The following commands are useful for exploring what the compiler, assembler, and linker actually produce:

- **Assembly output:** `gcc -S hello.c -o hello.s`
- **Symbol table:** `nm hello.o` or `nm hello`
- **Disassembly:** `objdump -d hello`
- **Linked libraries:** `ldd hello`
- **Full ELF dump:** `readelf -a hello` or `objdump -x hello`

Harris & Harris have a similar model showing a Linux x86-64 run-time memory on page 734 in their book. I hope it's becoming obvious how there are several insights to pick up in this abstraction that intersects high-level programs and the hardware platform. It has been shown how multiple files can be combined with shared or static libraries. We've been educated in ways that can help us avoid programming errors and understand why for example it's not possible to define multiple global variables or functions with the same name — these variables and functions get allocated to unique memory addresses at compile time, so they have to be unique. On the other hand local variables that only exist within the module are handled at runtime by the stack and so do not have the same requirement. I hope this section has left you with an impression of how the high-level program abstraction is broken down and how it reaches the machine version, not with the use of magic, but complex software broken into separate modules following best practice software engineering principles. Reading Keith's work makes it apparent that the design of compilers has been an important problem to solve for computer scientists and programmers, starting in the mid 1950s. Today many techniques have been developed, some of which Keith spends time on starting with a chapter on *context-sensitive analysis*. I will leave it to the reader to read up on further details if interested in what algorithms and techniques more specifically are used for writing compilers. 
