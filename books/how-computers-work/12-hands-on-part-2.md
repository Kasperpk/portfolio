The path to understand computing systems now embark beyond things like how registers are built from lower level flip-flops or how the CPU was constructed from elementary logic gates. The computer built up so far is now considered an abstraction of cleverly designed electronic components. We've connected to the soul of the computer and now move into the bottom of the software-hiearchy that ends with putting our ideas down in high-level programming language. But what actually makes this abstraction work? That is 
* Assemblers
* Virtual Machine
* Compiler
* Operating systems
The assembler was really the first intersection between hardware and software and now we consider the next abstraction, the virtual machine.

The high level language is of course just an abstraction - it does not exists for real. It can be implemented with a *compiler* that translate the source code into a intermediate format called vm code that is designed to be executed on a virtual machine. The compiler is also an abstraction and the VM code is then assembled by a VM  translator and from there translated into machine language. This sort of workflow is seen in the figure below and what Simon calls a *two-tier* compilation process. 
![350](Compiler%20and%20VM%20translator.jpg|center)
We are quite lucky that there are compilers and VM translators that bridges the gaps there are between our high level thinking and language into something expressed at a machine level. This is the beauty and elegancy of abstractions and modularity of a system. 

**The stack machine**
The stack is the first VM abstraction that this course introduces. The stack is the most important element an is an architecture that strikes a balance between the high-level language and the low level implementation. 
![350](The%20stack%20machine%20abstraction.jpg|center)
The stack has two operations push and pop, which can be seen in the top right corner and the general operation is shown at the bottom of the figure namely to
1. Pop argument from stack
2. Compute function on the argument
3. Push result on the stack
The commands come from the high level language which is compiled into code that is implemented on a stack machine, which is also an abstraction. 
![350](Stack%20commands%20compiled.jpg|center)
The stack machine can be manipulated by the commands which falls into the following categories
* Arithmetic / logical commands
* Memory segment commands
* Branching commands
* Function commands
Above we have seen some arithmetic commands such as sub, add. 

*Pointer manipulation*
```
p1 = 256 
p1 = p1 + 3 // p1 becomes 259
*p1 = *p1 + 3 // Modifying value at address 259
p2 = p1 - 2 // p2 becomes 257
p1-- // p1 is decremented to 258
*(p2 + 1) = *p1 + *p2 // Value at address 258 becomes value at 258 + value at 257 therefore 200 + 31 = 231. 
```
The implementation in HACK of a pointer manipulation operation seen at the top in the as an abstraction. What is apparent here is that we first use the A register as a data register, then we use it to hold a memory address found at the stack pointer memory. Once we write A=M, in this case A = 258, the selected memory address automatically also becomes RAM[258], we then set that to the value of D which is 17. 
Finally we need to increment 

**VM implementaton memory segments**
We have seen the stack machines arithemtic and logic commands. Now the next part is the memory segments commands which are also an important part. It's shows that the memory of a program is divided into different segments which have different utilities. 
![350](Memory%20segment%20pointer%20manipulation.jpg|center)
The general syntax of memory segment commands can be seen below 
![350](General%20syntax%20memory%20commands.jpg|center)

![350](Memory%20segment%20implementation.jpg|center)
The VM translator is a program that will take a source file written in VM code and produces assembly code as the target language. For example push constant 17 will be translated into something like 
@17
D = A
... (additional commands)

**VM implementation on the HACK platform**
The VM translator is a program written in some high-level language, which breaks down a program in VM source code, into its lexical elements and reexpress that in HACK assembly. The lexical elements are the arithmetic and logic commands aswell as pop/push segment *i* commands. We really need a mapping between the two, just like you would like to have a mapping between french and spanish if you were to translate between those two languages. 
**Standard VM mapping**
![](Sketches/Standard%20mapping%20vm%20to%20assembly.png)

![](Sketches/Mapping%20VM%20to%20Assembly.png)

The proposed design of such an implementation is to have a
* **Parser:** That parse each VM command into its lexical elements
The parser takes an file as input and open it. It checks if there are more commands and if so it should consider what type the command is. 

* **CodeWriter:** That writes assembly code that implements the parsed command
Opens a file to write and writes the output.

* **Main:** drives the process (VM translator)
Main (VMTranslator)
Input: fileName.vm
output: fileName.asm

The main program 
1) constructs the parser to handle input file, 
2) constructs a code writer to handle output file. 
3) Marches through the input file, parsing each line and generating code from it

To test our solution, we can use the supplied VM emulator, that can simulate how the HACK computer would behave if it was real. 

### Virtual machine part ll: Program control, branching and functions
High-level languages have more than just arithemtic and logic commands. It also have capability more than moving data from different parts of memory. A cornerstone idea of programming is that "we can extend the basic language at will". This can be done by creating *functions* abstractions. That could be **sqrt**, **power**, **disc**, anything that comes to the creative mind of the programmer. 

In additon high-level programming is not always following linear order of execution as the previous programs did. We allow the program to *branch* into multiple routes by using control flow. 

**Branching**
Look at the high-level code below. This program involves a *while* loop to calculate the multiplication of two numbers. The virtual machine generates if-goto and goto commands to implement branching. In this case push *n*, push *y* and check for greater than is exactly the condition in the while loop and so that is how such a line of code would look like on the stack machine. 

**Elegancy of extending progamming with functions**
Here is an example of a high-level program that calls a function sqrt. This high-level program also uses multiplication symbol, something which is implemented in VM by making a call to the Math library of the operating system. The arguments that the function needs to operator on a pushed to the stack and the function returns to replace the values on the stack. 

The VM language features thus 
* primitive operations (add, sub..)
* abstract operations (extensibility): multiply, sqrt

The elegancy is that no matter if a built-in command or an abstract function is called, the implementation is the same. This is one of the key ideas that makes high-level-programming so powerful. It can be extended by the imagination. Push as many arguments as is needed by the function onto the stack and when the function returns it replaces those values with the return value. 

**Under the hood when calling functions**
Here is the view of implementation. It shows what happens underneath when a function is called by the caller. Inside the function *main* a call to a mult function is made with the *call* keyword. Before the call the caller needs to pass the arguments the callee needs to use onto the stack. 

**VM translator: proposed implementation**
The standard mapping on the HACK hardware platform can be seen here below. 
In the implementation there will also be some additional special symbols.
The same setup of main, parser and code writer is proposed for the implementation here. The main is going to be extended a little bit being able to take a directory as input as well as a single file. It then checks if input file is a single file or a directory. 
Extending the code writer can be quite extensive especially for the function, call and return. 
 
The first thing that SImon will consider is variables. Particularly variables need to be handled such that they will be mapped to some memory segment and number. This is done by knowing the properties of the variable which include
* name (identifier)
* type (int, char, boolean, class name)
* kind (field, static, local, argument)
* scope (class level, subroutine level)
To manage this information about variables is to use **symbol tables**. For example for the program that Simon uses in unit 5.2 

There are the following class variables and the symbol table can be reset when we compile a new class. 

| name       | type | kind   | #   |
| ---------- | ---- | ------ | --- |
| x          | int  | field  | 0   |
| y          | int  | field  | 1   |
| pointCount | int  | static | 0   |
The method distance has a surprising variable called *this*, which by design it always operates on. The type of the variable is always the name of the class to which the subroutine belongs and is always treated as argument 0. The symbol table can be reset each time we encounter a new subroutine. 

| name  | type  | kind     | #   |
| ----- | ----- | -------- | --- |
| this  | Point | argument | 0   |
| other | Point | argument | 1   |
| dx    | int   | local    | 0   |
| dy    | int   | local    | 1   |
The codewriter will handle variable declarations this when it encouters a field/static/var and add the information or properties to the symbol table.
#### Handling expressions
Generating code for expressions is a two-stage process that first constructs a parse tree like done in project 10. From the parse tree one can infer the stack machine code by turning the infix notation of an expression into the post fix notation used by the VM target language. For example the expression x + g(2,y,-z) * 5 will push the operands x, 2, y and z to the stack then call g, then push 5 to the stack, multiply, then add. This is quite elegant way of handling expressions. How do we move from the parse tree to the vm code. In this case we can use the algorithm *depth-first tree traversal* it begins from the root of the tree and goes all the way down starting from left to right and process it. Simon suggest a *codeWrite* algortihm. This code will do the following

```
CodeWrite(exp)
	if exp is a number n:
		output "push n"
	if exp is a variable var:
		output "push var"
	if exp is "exp op exp""
		codeWrite(exp_1)
		codeWrite(exp_2)
		output "op"
	if exp is "op exp":
		codeWrite(exp)
		output "op"
	if exp "f(exp, exp, ..)":
		codeWrite(exp_1)
		codeWrite(exp_2)...
		output "call f"
```
This code will tranforms the infix notaton of an expression into the post fix that the stack machine expects. For example the following vm code
```
push x
push 5
neg
push a
push 7
call Foo.bar
add
```
Must have looked something like this to begin with
```
x + foo(-5,a,7)
```
Another example is the expression
```
let x = a + b * c;
```
To use the codewriter above we get the following result. 
```
push a
push b
+
push c
*
```
#### Handling flow of control
What is shown below is how an if statement code will be generated. We compute some expression and negate the output, if that is true we goto a label that refers to the statement otherwise we goto L2.
```
compiled (expression)
not
if-goto L1
compiled(statements1)
goto L2
Label L1
	compiled (statements2)
Label L2
```
A while loop starts with a label, compile the expression negate the output, if that is true it steps out of the loop by going to L2, otherwise it compiles the expression within the while loop and go to L1 and potentially stay in the loop.

```
Label L1
	compiled (expression)
	not
	if-goto L2
	compiled(statements)
	goto L1
Label L2

```
There are some minor complications we need to be aware of. The code generator needs to generate unique labels for the different branches. It also needs to take care of nested statements. It turns out this is already handled by the compilation engine already with the software engineering we have done so far. Compiling the other statements let, return is fairly straightforward. 
**Handling objects**
Let's remember what we are doing here, we are creating a module that can transform the human friendly syntax into the VM code that the stack machine uses. The host RAM is divided into these memory segments that the stack machine recognizes where pointers are stored to the base addresses of each segment. Objects and arrays are according to Simon stored in another part of RAM called the *heap*. The heap records all the objects and arrays that the current program seeks to manipulate. There may be millions of objects. The way this is implemented in the Jack language is to use the *pointer* segment that sets the this and that segments to the base addresses of the heap. 
```
// This segment implemented using the pointer segment, to // initialize class creation
push 8000
pop pointer 0 // sets THIS to 8000

push/pop this 0 //accesses RAM[8000] either pushing from it to the stack or pops from the stack onto this address.
push/pop this i // accesses RAM[8000+i]
```
In general we must first write VM code that anchors this and that base addresses and then we can access and manipulate objects with the this segment and the arrays with the that segment. 
#### Object construction from the callers perspective
When we create a new object such as var Point p1; refering to some class type variable, we will initialize a pointer on the stack to 0. Then if we call a let statement that calls the constructor of this class such as let p1 = Point.new(2,3); then the pointer will be set to a location in the heap where 2 and 3 then will reside. What happens is that the compiler will update a symbol table that specifies the class variables. This will be on the local segment of the stack such putting an entry into the symbol table p1 Point local 0. Once we construct the variable, we push the arguments onto the stack and call the method that may be a constructor in this case. This constructor returns the base address of the object created, puts it into the top of the stack. Now this enables us pop this value and assign it to p1 such that p1 now points to the base address of the object created. This mans that  **object construction** is a two-stage affair as Simon describes first allocating some local segment to it and then at run time when the constructors are actually called is the base address of the memory allocation the heap assigned to these local variables that now point at these addresses. 
#### Object construction from the callees perspecetive
The constructor does two things 
* Arranges the creation of a new object
* Initializes the new object to some initial state
That means it needs to have access to the objects *fields*. It can this be accessing the *this* segment. It must first anchor the this segment using the pointer segment. How does this happen? When the constructor is called, the compiler will check how many arguments it consist of and push that value onto the stack. Then the operating system API Memory.alloc is called which returns the base address of the memory it has allocated for the constructions of this object. Then it anchors the this segment as it pops the base address just found to the pointer segment 0. With the this segment anchored it is now possible to use the newly created object like assigning some variable declarationswhich are pushed on to the argument segment and then popped into the this segment. Finally the constructor will return this with push pointer 0 command. 
**Oject manipulation**
We have to know how to handle code that calls methods that operate on selected objects. Then we also have to discuss how to compile the methods themselves.
#### Object manipulation from the callers side
In essence machine languages or VM code is procedural so the object oriented syntax has to be rewritten in to this style by the compiler. 
This can be done by taking the object of which the method is called on an pass it as the first implicit argument to the subroutine. 
What we do is push the object onto the stack and then call the method. Remember that the obj in this case points to the base address of this constructed object. We then assume that the subroutine has the code that enables it to access the information in that object it will operate on. 
```
// Converting object oriented code into procedural style
// by pushing the arguments to the stack
push obj
push x1
push x2
push ...
call foo
```
#### Object manipulaton from the callees side
Methods are designed to operate on the current object which we refer to as *this* in most object oriented languages. Therefore the method can access the fields of the objects *i*-th field by accessing the this *i*. We learned that the this segment is properly anchored using the pointer segment.
```
// Jack class example code
class Point {
	field int x, y;
	static int pointCount;
	..
}

method int distance(Point other) {
	var int dx, dy
	let dx = x  - other.getx();
	let dy = y - other.gety();
	return Math.sqrt((dx*dx)) + 
					 (dy*dy));
}
```
The first lines of jack code, generates no code but instead creates and updates symbol table for the class and method level. 
![](Example%20symbol%20table.png|center)
Once this is establish we know that we have to anchor the this segment to the correct address in memory which is the address of the current object. The current object is the object that the caller passed in order to operate upon. It is always stored in argument 0, because it is the object as seen above that the method works on. Therefore we push argument 0, then pop that value to pointer 0, to set this equal to the base address of the current object. 
```
// method int distance(Point other)
// var int dx, dy
push argument 0
pop pointer 0 // THIS = argument 0

// let dx = x - other.getx()
push this 0 // Looking at the symbol table at the class-level one can see              //x is the first variable therefore stored at this 0. 

push argument 1 // push other on to the stack
call Point.getx 1
sub
pop local 0    // store result in the local 0 that represent dx 


// return Math.sqrt((dx*dx)+(dy*dy))
push local 0
push local 0
cal Math.multiply 2
push local 1
push local 1
call Math.multiply 2
add
call Math.sqrt 1
return

```
Pushing this 0 was a little bit confusing to me at first, but i guess it makes sense that now that the this segment has been anchored to the base address of the class, then the x is the first variable that is stored. Finally the 
#### Handling void methods
Void methods do not return a value, but methods must returns value to the caller. Therefore the compiler will push constant 0 and return which is a dummy value. Therefore the compiler needs to handle void methods in that way. From the callers persepctive it will need to do an extra step after call the method it will pop temp 0 which puts the returned value away from the stack. 
**Handling arrays**
#### Array construction
When the high-level programmer declare something like var Array arr; the compiler will create a local variable and initialize it to the value 0 and add a row to the symbol table. If the programmer construct this array later such as let arr = Array.new(5); the compiler will together with the OS allocate sufficient space in the heap. The base address of this block will be stored in local 0 overwriting the 0 when the variable was declared. The Array.new(n) is a standard call to a subroutine and is handled exactly like object construction. 
#### Array manipulation
pop pointer 1 sets the THAT segment and this is where it is recommend to store current array. For example we could do the following set of VM commands. 
```
// Setting RAM[8056] = 17
push 8056
pop pointer 1
push 17
pop that 0

// Assigning the 3 index of an array to the value 17
// arr[2] = 17
push arr          //push base addres
push 2            //offet
add
pop pointer 1     // store the result to pointer 1
push 17
pop that 0
```
This implementation is shown visually here below. We only use the that 0, because we constantly update the *that* segment if we want to manipulate a specific index in an array. Secondly one can notice that the VM code knowns absolutely nothing about the host RAM. It operate in a world of a VM - it cannot breach out and mess up things that are outside the virtual machine. The VM translator ensures that the code is safe and we don't know which hardware platform it will be implemented on, it could be a smartphone, laptop etc and the VM code would still compile. 

The general array indexing expression is arr[expression] = expression is handled in the following way. 
```
// general array access expression
push arr
push expression
add
pop pointer 1
push expression;
pop that 0
```
Unfortunately there is a problem. If we want to compile a[i] = b[j], in this case we overwrite the first index of a[i] with b[j]. In this case we need another approach.
```
// general array access expression
push a  //push the base address of a on to the stack
push i  // push index 
add     // calculate address of the array index
push b  // push base address of b on the stack
push j  // push index
add     // calculate address of the array index
pop pointer 1 // put the calculated index of b[j] on the pointer 1 segment
push that 0   // push that address on to the stack
pop temp 0    // store it in temp 0
pop pointer 1 // put the calculated index of a[i] on the pointer 1 segment
push temp 0   // push the stored address on the stack
pop that 0    // write to the index of a[i] the value at index b[j]
```
**Standard mapping over the virtual machine**
When compiling subroutines it depends on if its a method, function or constructor. 
* If it's a method then the compiled VM code must set the base of the *this* segment to *argument* 0. So that the method starts running it establish access to the object which it has to operate on. 
* When compiling constructors we have to create space in memory for the object we seek to create, we set the base of this block to the this segment. The compiled VM code must return the object's base address to the caller. 
* When compiling void functions or void methods we need to return the value constant 0. The caller then has to remove it from the stack, by pop temp 0. 
When compiling subroutines calls, the caller must push the arguments on to the stack and call the subroutine for its effect. If the subroutine is a method, the caller must push a reference to the object which the method is supposed to operate on. Next the caller must pushi *arg1*, *arg2* an then call the method. 
Compiling constants such as null is mapped on the constant 0, false is mapped on the constant 0, true is mapped on the constant -1. 
OS services allow one to use for example the Math classes such that one can do multiply, divide, strings. We use the Memory.alloc() whenever we want to create an object and Memory.dealloc() to remove the object again. 
**Completing the compiler: proposed implementation**
Now the program needs to not generate XML code, but VM code. The following modules are proposed
* JackCompiler
This module focuses mainly on SymbolTable and WMWriter. The Jack compiler has a main function that initialize the program and can take an input such as a file or a directory, containing one or more .jack files. 
* JackTokenizer
* SymbolTable
* VMWriter
* CompilationEngine
#### The symbol table
The symbol tables are in two scopes, one for a class and one for a subroutine. The symbol table class will have a class level and subroutine level symbol table. Each variable is given a running index within its score and kind. Starting at 0 and then incrementing by 1 each time a new symbol is added and then reset to 0 when starting a new scope. These operations have to be handled by the symbol table. This class will more particularly have 
![](Symbol%20table%20API.png|center)
It can be implemented using two separate *hash tables* one for the class scope and one for the subroutine scope. 
#### The VM writer
![](VM%20writer%20API.png|center)
#### The compilation engine
We have to change the compilation somewhat in this step to change the compilation engine to write VM code instead of writing XML. 
![](Compilation%20engine%20API%201.png|center)
![](Compilation%20engine%20API%202.png|center)
#### Perspectives
1) Jack is very simple compared to other high-level programming languages, what would be the difference between a compiler for a more advanced programming language?
Most programming languages feature rich and versatile data type systems such as allocating different memory sizes for each type and conversion between them. Another significant difference is that jack does not support inheritance. Java for example needs to also consider which class an object is a part of. Jack also has no public fields which makes code generation far simpler than other. 



