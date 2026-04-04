At the intersection of compilers, computer architecture and operating systems sits *linking.* Understanding linking can have several positive side effects to programming, such as how to combine multiple files existing in shared or static libraries. In addition it offer insights that can help avoid programming errors such as defining multiple global variables or functions with the same name. Local variables are handled at runtime by the stack. For function calls and global variables the names needs to be unique so they can have a unique memory address. Understand how modern systems work like Microsofts OS and it's DLL files and loader that takes the exe file and loads it into memory. 

Linking is performed at the final stage of an typical four step process of manipulating source code files into fully executeable files that can be *loaded* into memory. The source file with the extension .c for example is translated into several intermediate version. 

**Compiler drivers**
Most compilation systems provide a compiler driver (p. 707) such as the GNU that invokes the language preprocessor, compiler, assembler, and linker. How i used the GNU to compile my C file. 

```
gcc -o FirstCProgram FirstCProgram.c
```

The intermediate version starts from the  .c -> .i -> .s -> .o

The .s file is the assembly version of the high-level program and can be inspected using one of the following commands

```
gcc -S FirstCProgram.c -o FirstCProgram.s

gcc -O2 -S -masm=intel FirstCProgram.c -o -
```

Below is shown **static linking** that combines two source files into a fully executable object file *prog*. 
![](01%20Computer%20engineering%20and%20architecture/sketches/Static%20linking.png)
The relocateable object files are sequences of bytes, following the ELF format. 
![[01 Computer engineering and architecture/sketches/EFL format rof explanation]]
The header contains important information about the word size and byte ordering of the system that generated the file as well as. 
* Object file type (relocatable, executeable or shared)
* The machine type (x86-64)
* The offset of the section header table, and the size and number of entries in the section header table.
* The locations and size of various sections as described in the header table.
Inside each section are things like the actual machine code of the compiled program, read-only data and jump tables. Initiliazed global and static variables are in the data section. BSS section includes uninitialized global and static variables, these are merely placeholders and will first at runetime be allocated to memory, while initialized global variables are allocated at compile. 

The linker has two overall objectives, it must perform
1) Symbol resolution
2) Relocation

**Symbol tables**
As we now high-level programmers use symbols such as identifiers for defining functions and variables. These symbols have to be tracked and allocated to specific parts of memory, such that at runtime the program will reference those memory addresses. This is done by the symbol table, which the assembler generates. 

There are tree types of symbols. 
1) The global symbols that are defined in some module m, and can be reference by other modules. 
2) Global symbols that are ferenced by module m but defined by some other module.
3) Local symbols that are defined and referenced exclusively by module m. These corresponds to static variables and functions. 
An ELF symbol table is contained in the .symtab section of the relocatable object file and contains an array of entries. The format for each entry is seen below. 

![](01%20Computer%20engineering%20and%20architecture/sketches/ELF%20symbol%20table%20entry.png)
The value is the offset from beginning of the section where the object is defined. For executable object files, the value is an absolute run-time address. (page 712). Below here is an inspection of the three last entries into a symbol table following a program that creates an array and performs sum on the elements using a sum function. 

![](01%20Computer%20engineering%20and%20architecture/sketches/Symbol%20table%20entry%20examples.png)
There are a few things to understand about how symbol resolution is done. The linker ensures that each symbol has a unique reference point. The local variables are quite straightforward as it is ensured that each has a single definition within the local module. Global symbols can be more tricky because the linker needs to make sure for example no ducplicates exists of global variables and functions across shared modules. In general there are the following rules. 

![](01%20Computer%20engineering%20and%20architecture/sketches/Linker%20resolving%20duplicate%20symbol%20names.png)
A **static library** is a package of related object modules. This package can be supplied to the linker and the linker can copy the modules that are referenced in the source code. This idea is quite elegant as otherwise the compiler would need to recognize all functions. Instead application programmers can import the modules into their program and the linker ensures that the object files are combined. 

![](01%20Computer%20engineering%20and%20architecture/sketches/Linking%20with%20static%20libraries.png)

**Relocation**
Once the symbol table has been resolved and handled, each symbol reference has exactly one symbol table entry in one of its input object modules. At this point the linker knowns the exact size of the code and data sections in its input object modules. It can now perform relocation. (page 725) This intails
1) Relocating sections and symbol definitions
2) Relocating symbol references within sections.

![[01 Computer engineering and architecture/sketches/Relocation]]
It merges the sections into an combined section. To relocate symbols it means providing an actual run-time address to the entries in the symbol table. These are relocated by creating relocation entries. These are placed in the object relocation file sections .rel.text and .rel.data. 

Here is the pseudocode for how relocations would be performed depending on if it's an PC-relative or absolute address.

![](01%20Computer%20engineering%20and%20architecture/sketches/Relocation%20algorithm.png)

**Loading executeable object files**
Running the command invokes the operation systems *loader* function that copies the code and data into memory and transfers control to the begining of the program.

```
./prog
```

The memory which the program is loaded into will have a structure like the one shown here below. This is how the programs data is divided into different segments, and the code itself is in another part of the memory. 

![](01%20Computer%20engineering%20and%20architecture/sketches/Run-time%20memory.png)

**Dynamic linking**
If you write your own modules, you can link them using *dynamic linking*. The Figure below shows the internal operations of what happens when linking the two files into a single fully linked executable in memory. 

![](01%20Computer%20engineering%20and%20architecture/sketches/Dynamic%20linking.png)

At runtime when the program is *loaded* into memory, the linking will take place as the data and code is copied into a allocated memory segment. 

- **Assembly:** `gcc -S hello.c -o hello.s`
- **Symbols:** `nm hello.o` or `nm hello`
- **Disassembly:** `objdump -d hello`
- **Linker info (libraries):** `ldd hello`
- **Full ELF/PE dump:** `readelf -a hello` or `objdump -x hello`

