
Once the source code is scanned, the next stage is parsing. The parser gets the transformed and scanned source code, that have identified tokens and their catagory (part of speech). It then determines if the program adheres to the grammatic rules of the language. Before a parser can be constructed, there needs to be a formal specification of the source language and a method for determining "membership" (p. 84, Keith D. Cooper). Keith describes how by restricting the source language to a "set of context-free languages, we can ensure that the parser can efficiently answer the membership question." (p. 84, Keith D. Cooper). Assigning membership is question to which many algorithms have been proposed. For example top-down parsing *recursive-descent* and LL(1) parsers, bottom-up or canonical parsers. Context-free grammer *G* is a set of rules that describes how to form valid sentences which is a string of symbols. One way to write this is using the following format

*SheepNoise* -> baa *SheepNoise* | baa
The first rule or production reads "SheepNoise can derive the word baa followed by more SheepNoise" (p. 86, Keith). SheepNoise is a syntactic variable here used to represent all set of strings that can be derived from the grammar, also called a *nonterminal symbol*. Rule 1 states that valid strings can be a valid string followed by another valid string represented with the nonterminal symbol. Rule two is recognizing a valid string and so all valid strings in some grammar are derived by zero or more applications of rule 1, followed by rule 2. 

**Parse trees**
This SheepNoise grammar is too simple to what CFGs need and instead we use another representation. Keith considers the sentence a + b x c. How could this sentence be parsed? One way to go about this is to use a **tree**. A tree is a data structure that consist of one or more nodes, organized into a hiearchy. It has one root, the top and each of the other nodes have a uniqe *parent. 

![[01 Computer engineering and architecture/sketches/Parse tree]]
These parse trees can become increasingly complex, but are capable of expressing the way a parser could interprent a sentence. This top-down approach can be implemented algorithmically using recursive-descend algorithms. An efficient algorithms for languages with grammers that are LL(1). LL(1) means that looking one-word ahead is sufficient to validate the syntax of the sentence. Because very efficient algorithms exists for this type of grammar, it has become popular among many high-level programming languages. 

The first phase or the front-end of compiling involves these two broad steps, scanning and parsing. This has caused compiler designers some challenges already with lexical analysis and context-free-grammar and *recursive-descent* algortihms as efficient solutions to those. Thus we start by scanning the source program, grouping characters into tokens and categorizing them. Following that, tokens are parsed recursively from left to right, top to bottom making sure it fulfills the contract of the grammar of the programming language. 

**Compiling programs and combining files with linking**
Compilers look at your program to make sense of it, hence scanning and parsing. If it can will continue the process of optimizing the code, and then generate intermediate versions of it. Randal E. Bryant and David R. O'Hallaron have dedicated one chapter to *linking* in their work *Computer Systems, A Programmer's Perspective*. It offers a similar but perhaps more practical view for programmers on what compiling entails more so than designing one from the ground up as described by Keith. I want to make this transition because studying the design of compilers quickly  becomes very technical and deroutes us away from the agenda. While linking is really what happens at the final stage of manipulating source code files into fully executeable, Randal and David describes the intermediate steps in ways that offers several insights that are relevant to the programmer. With focus on the C programming language they show how the source program starting from the .c extension gets compiled into  .i -> .s -> .o versions. 

To compile a C source file a compiler driver such as the GNU is needed. This driver invokes the language preprocessor, compiler, assembler, and linker. As an example the following commands can be passed to the command line interface if the GNU is installed and a C program has been written in the current directory.

```
gcc -o FirstCProgram FirstCProgram.c
```

The C program in FirstCProgram contains the following source code in code example 1.1. It simply defines a function *main* and prints the string "Hello World!" and a rounded up version of the number 1.4. The program can be loaded into memory and executed with the ./Program command. This command for the FirstCProgram and it's output is shown in the code block 1.2.   
Code block 1.1: C program
```
#include <stdio.h>
#include <math.h>

int main() {
    printf("Hello World!\n");
    printf("%f", ceil(1.4));
    return 0;
}
```

Running the command ./FirstCProgram, invokes the operation systems *loader* function that copies the code and data into memory and transfers control to the begining of the program.

Code block 1.2: Output of C program
```
./FirstCProgram

Hello World!
2.000000
```

This program is not particularly useful, but what is interesting is to inspect the compilation process and the GCC compiler collection offers ways to inspect the intermediate files. Code block 1.3 shows a command to save intermediate file versions.

Code block 1.3: Saving intermediate files of a C program.
```
gcc -Wall -save-temps FirstCProgram.c -o FirstCProgram
```
The first version being the .i file, is not particularly interesting. It's a preprocessed file that contains a long series of commands ending with the lines of code as they were written in C. 

The .s file is more interesting. It contains the assembly version of the high-level program. Inspecting the assembly code reveals that even a simple program written with four lines of code in C requires many low level operations. In all it's extended to something like seventy lines of code as shown in code block 1.4. The interesting thing is that one can see that a program like this is expressed using familiar low-level operations like move, subtract and add operations. There are also some other operations that i haven't covered specifically like push, leaq but all of them are part of the instruction set architecture of the hardware. 
Code block 1.4: Assembly version of C program
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

Notice that the C program contained the function ceil() and that it imports the includes the math.h file at the top of code. What the compiler needs to do is combine these files into the source code, known as linking. In this case a math module contains functions like rounding a fractional number. Each of the files are compiled separately to .o files or *relocatable object files* before they get linked into a fully executeable object file, shown here in figure 1.1
![](01%20Computer%20engineering%20and%20architecture/sketches/Static%20linking.png)
Figure 1.1 Reproduction of figure 7.2 Static linking: The linker combines two relocatable object files to forn an executeable object file prog (p. 708 Randal E. Bryant and David R. O'Hallaron) 

A **static library** like the math library is a package of related mathematical object modules. This package can be supplied to the linker and the linker can copy the modules that are referenced in the source code. This idea is quite elegant as otherwise the compiler would need to recognize all functions. Instead application programmers can import the modules into their program and the linker ensures that the object files are combined. Randal and David goes spend time on two important aspects of what compilers are responsible for handling that is *symbol tables* and *relocation*. 

High-level programmers use symbols such as identifiers for defining functions and variables. those which the scanner is responsible for identifying. These symbols have to be tracked and allocated to specific parts of memory, such that at runtime the program will reference those memory addresses. This is done by the symbol table, which is generated at the assembler step.  

Randal and David explains that there are tree types of symbols. 
1) The global symbols that are defined in some module *m*, and can be reference by other modules. 
2) Global symbols that are ferenced by module *m* but defined by some other module.
3) Local symbols that are defined and referenced exclusively by module *m*. These corresponds to static variables and functions. 
Symbol tables are contained in a special section called the .symtab of the .o file that the assembler generates. This symbol table contains array of entries for each symbol specifying it's name, type, address, size, section and whether it's a reserved keyword or not. The address value is the offset from beginning of the section where the object is defined. 

The linker ensures that each symbol has a unique reference point. The local variables are quite straightforward as it is ensured that each has a single definition within the local module. Global symbols can be more tricky because the linker needs to make sure for example no ducplicates exists of global variables and functions across shared modules. In general there are the following rules. 

**Relocation**
Once the symbol table has been resolved and handled, each symbol reference has exactly one symbol table entry in one of its input object modules. At this point the linker knowns the exact size of the code and data sections in its input object modules. It can now perform relocation. (p. 725, Randal E. Bryant and David R. O'Hallaron) This intails
1) Relocating sections and symbol definitions
2) Relocating symbol references within sections.

![[01 Computer engineering and architecture/sketches/Relocation]]
Figure 1.4 Merging sections and symbol defnitions of multiple relcoateable object files into a fully linked executeable object file.

It merges the sections into an combined section. To relocate symbols it means providing an actual run-time address to the entries in the symbol table. These are relocated by creating relocation entries. These are placed in the object relocation file sections .rel.text and .rel.data. These operations require efficient algorithms as hinted to by Keith in his introduction to compiler design. 

Now when the program is loaded into memory it will have a structure like the one shown here below. This is how the programs data is divided into different segments, and the code itself is in another part of the memory. 

![](01%20Computer%20engineering%20and%20architecture/sketches/Run-time%20memory.png)
Figure 1.5 Reproduction of figure 7.15 *Linux x86-64 run-time memory image: Gaps due to segment alignement requirements and addressing space layout randomization (ALSR) are not shown. Not to scale* (p. 734, Randal E. Bryant & David R. O'Hallaron)

I hope it's becoming obvious how there are several insights to pick up in this abstraction that intersects high-level programs and the hardware platform. It has been shown how multiple files can be combined  with shared or static libraries. We've been educated in ways that can help us avoid programming errors and understand why for example it's not possible to define multiple global variables or functions with the same name. As these are varaibles and functions gets allocated to unique memory addresses at compiling, they have to be unique. On the other hand local variables that only exists within the module are handled at runtime by the stack and so does not have the same requirement. I hope this section have left you with an impression for how the high-level program abstraction is broken down and how it reaches the machine version, not with the use of magic, but complex software broken into separate modules following best practice software engineering principles. Reading Keiths *Engineering a compiler* makes it apparant that the design of compilers have been an important problem to solve for computer scientist and programmers, starting in the mid 1950s. Today many techniques have been developed  some of which Keith spends time on starting with a chapter on*context-senstive analysis*. Technical details can be further studied such as algorithms and techniques for code optimization and generation. 

