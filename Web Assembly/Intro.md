
WebAssembly is statically typed and precompiled, and thus it provides better performance than JavaScript.

A compiler has 3 components:
```mermaid
flowchart LR
S[Source code]-->A[Frontend]
A---|IR|B[Optimiser]
B---|Optimised IR|C[Backend]
C-->D[Machine Code]

```
- #### Front end:
	- Needs to understand the source language
	- Checks source code for syntax issues
	- Converts source code to an intermediary representation (IR) (Compiler's version of the source code)
- #### Optimiser:
	- the optimiser analyses the IR and transforms it into a much more efficient one.
	- Few compilers have multiple IRs
	- The optimizer is an IR-to-IR transformer
	- The optimizations here include removing redundant computations, eliminating dead code (code that cannot be reached), and various other optimizing options.
	- the optimizers need not be language-specific. Since they act on the IR, they can be built as a generic component and reused with multiple languages.
- #### Backend:
	- The backend focuses on producing the target language.
	- The backend receives the generated (optimized) IR and converts it into another language (such as machine code).
	- This machine code is the actual code that runs on the bare metal. In order to produce efficient machine code, the backend should understand the architecture in which the code is executed.


#### ISA (Instruction Set Architecture)
- An instruction set is a set of operations supported by a processor, and this overall design is called an **Instruction Set Architecture** (**ISA**).
- Various processors convert the ISA in different implementations.
- The ISA is an interface between the hardware and the software.
<p style="color:red;font-size:18px">Example: How the Intel x64 architecture adds two numbers using its Instruction Set Architecture (ISA)?</p>
In x64 assembly language, adding two numbers is typically done with the following steps:
1. **Load the Numbers:** The first step is to load the numbers you want to add into CPU registers. Registers are like small, super-fast storage spaces inside the computer's brain. You might load the first number into one register (let's call it Register A) and the second number into another register (Register B).
    
2. **Perform the Addition:** Now that you have the numbers in registers, you use an addition instruction provided by the ISA. In x64 assembly, this instruction is usually called "add." You tell the computer to add the contents of Register A and Register B together.
    
3. **Store the Result:** After the addition, the result is stored in another register or in memory. This is where you'll find the answer to your addition.
4. Here's a simplified example in x64 assembly code:
   <code>
	   <pre>
	   ; Load the first number (e.g., 5) into Register A
		mov rax, 5
		
		; Load the second number (e.g., 7) into Register B
		mov rbx, 7
		
		; Add the contents of Register A and Register B and store the result in Register C
		add rax, rbx
		
		; Now, the result (12) is in Register A (rax)
		</pre>
   </code>
In this code:

- We load the numbers 5 and 7 into registers `rax` and `rbx`.
- We use the `add` instruction to add the contents of `rax` and `rbx`.
- The result, 12, is now in `rax`.

#### Low Level Virtual Machine (LLVM)
LLVM is a widely-used compiler infrastructure project that provides tools, libraries, and frameworks for the development of compilers, code analyzers, and other related software.

1. **Compiler Infrastructure:** At its core, LLVM is a collection of modular and reusable components for building compilers. These components include a compiler front end (which translates source code into an intermediate representation), optimization passes, and a code generator (which translates the intermediate representation into machine code).
    
2. **Intermediate Representation (IR):** LLVM uses a unique and highly flexible intermediate representation called LLVM IR. LLVM IR is a low-level, platform-independent programming language that serves as a bridge between the source code and the target machine code. This intermediate step allows for a wide range of optimizations and analysis to be performed on the code before generating efficient machine code.
    
3. **Wide Adoption:** LLVM has gained widespread adoption and is used in various programming languages and tools. Notably, it's the foundation of the Clang C/C++ compiler, used by many developers for its fast compilation and helpful error messages. It's also used in Swift, Rust, Julia, and many other languages.
    
4. **Optimizations:** LLVM's modular architecture allows developers to write custom optimization passes that can analyze and improve code. This makes it possible to generate highly optimized machine code from the intermediate representation.
    
5. **Portability:** LLVM IR is platform-independent, which means that a compiler front end (e.g., for a new programming language) can generate LLVM IR, and LLVM can then handle the platform-specific code generation.
    
6. **Just-in-Time (JIT) Compilation:** LLVM is capable of performing Just-in-Time compilation, which means it can compile code on-the-fly as a program runs. This is especially useful for dynamic languages like Python, where performance improvements can be achieved through JIT compilation.
    
7. **Research and Education:** LLVM is used in research and education as a powerful tool for experimenting with compiler and programming language design. It provides a platform for exploring new optimization techniques and language features.
##### Diagram For Machine Code Generation Flow:
```mermaid
graph LR
    A[Source Code:Language-Specific] -->|Frontend| B[LLVM IR]
    B[LLVM IR] -->|Common Core| C[Optimization Passes]
    C[Optimization Passes] --> D[LLVM IR:Optimized]
    D -->|Common Core| E[Code Generation]
    E[Code Generation] -->|Backend| F[Machine Code:Target-Specific]

```
**The main advantages of LLVM are as follows:**

- LLVM uses a simple low-level language that looks similar to C.
- LLVM is strongly typed.
- LLVM has strictly defined semantics.
- LLVM has accurate and precise garbage collection.
- LLVM provides various optimizations that you can choose based on the requirement. It has _aggressive_, _scalar_, _inter-procedural_, _simple-loop_, and _profile-driven_ optimizations.
- LLVM provides various compilation models. They are _link time_, _install time_, _runtime_, and _offline_.
- LLVM generates machine code for various target architectures.
- LLVM provides DWARF debugging information.

<div style="background-color:#176B87;padding:5px;border-radius:10px;">
	LLVM uses @ symbol to identify global variables and % for local variables
</div>

