tools

- `objdump -d <file>` -> disassembler
- gdb -> debugger
- binwalk -> examines binary images for embedded files
- IDA Pro
- Ghidra
- `hexdump -C <file>`
- `strace` : Traces Linux System Calls
- `ltrace` : Traces Library Functions

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/1f094477-97cc-416c-b13f-d74c54ac1a80)

file <file>
- `set LOLO=HELLO` : Setting an environment variable
- `set` : Shows all environment variables

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/10a23952-db4c-4663-ad63-f16bec9c3165)


GDB
----
- context
- start
- run
- break main
- break *(addr)
- set $rip = addr
- set $rip = main
- skipi
- x/20xg $rip : examine 20 giant(8bytes) in hexa format
- hexdump $rsp /10 : print 10 hexdump lines from stack pointer
- set diassembly-flavor intel
Introductory/Recap: https://www.youtube.com/watch?v=nLp3hr6Jf2M

Ghidra
-------------
- Visual Studio contains PDB(Program Database) files that Ghidra get extra info [Solution: Unselect PDB while analyzing the code in Ghidra]
- RTTI Analyzer (Metadata)
- WindowsPE Propagate External Parameters
- You may consider shift deleting .text sections before analyzing the code in Ghidra
- Main function has an exit code
  
Resources
----------------
- https://0xinfection.github.io/reversing/
- https://osandamalith.com/2019/02/11/linux-reverse-engineering-ctfs-for-beginners/

Gemini Convo
-----------------
```
#include <stdio.h>
int main() {
   int i = 0;
   int n = 5;
   int sum = i + n;
   return 0;
}
```
```
main:
        push    rbp
        mov     rbp, rsp
        mov     DWORD PTR [rbp-4], 0
        mov     DWORD PTR [rbp-8], 5
        mov     edx, DWORD PTR [rbp-4]
        mov     eax, DWORD PTR [rbp-8]
        add     eax, edx
        mov     DWORD PTR [rbp-12], eax
        mov     eax, 0
        pop     rbp
        ret
```
The way I see it (x86-64 gcc):
You put immediate values to the stack frame distanced by 4 bytes, since each int var is 4 byte in this context. but since you can't just add the values stored in two memory location (btw, [rbp-4] references the memory stored at rbp-4, can be compared to the dereferncing operator * in c), you first take them to two registers edx and eax and then move their summation to the register eax and store the resulting value in the stack frame, 4 bytes away from the last used memory space, and finally just put the returning value of the function to eax only to pop rbt and ret to officially mark the end of the function

Please point out any potential mistake in my interpretation, master
Your interpretation is mostly accurate! Here's a breakdown of the assembly code with a few additional notes to clarify your understanding:

x86-64 Assembly and the Stack Frame

Stack Frames: Stack frames are sections of memory on the stack used by functions to store local variables, arguments passed to the function, and information for returning control to the calling function.
Registers rbp and rsp:
rbp: The base pointer. Traditionally used to point to the start of the current function's stack frame.
rsp: The stack pointer. Points to the current top of the stack.
Code Breakdown

```Code snippet
main:
    push    rbp            ; Save the caller's base pointer on the stack
    mov     rbp, rsp       ; Set up the base pointer for this function's frame
    mov     DWORD PTR [rbp-4], 0   ; Initialize variable 'i' to 0
    mov     DWORD PTR [rbp-8], 5   ; Initialize variable 'n' to 5
    mov     edx, DWORD PTR [rbp-4] ; Load the value of 'i' into edx
    mov     eax, DWORD PTR [rbp-8] ; Load the value of 'n' into eax
    add     eax, edx               ; Add 'i' and 'n', store result in eax
    mov     DWORD PTR [rbp-12], eax ; Store the result ('sum') on the stack
    mov     eax, 0                 ; Prepare the return value (0)
    pop     rbp                    ; Restore the caller's base pointer 
    ret                            ; Return from the function
```
Use code with caution.
Explanation

Function Prologue:

push rbp: Saves the previous value of the base pointer (from the calling function).
mov rbp, rsp: Sets up the base pointer for the current function's stack frame.
Variable Initialization:

mov DWORD PTR [rbp-4], 0: Stores the value 0 at the memory location rbp-4, effectively initializing the variable i.
mov DWORD PTR [rbp-8], 5: Stores the value 5 at the memory location rbp-8, initializing the variable n.
Calculation:

mov edx, DWORD PTR [rbp-4]: Loads the value stored in i (from the stack frame) into the edx register.
mov eax, DWORD PTR [rbp-8]: Loads the value stored in n (from the stack frame) into the eax register.
add eax, edx: Adds the values in edx and eax, storing the result in eax.
Storing the Result:

mov DWORD PTR [rbp-12], eax: Stores the value of eax (which holds the 'sum') into a new location on the stack frame.
Function Epilogue

mov eax, 0: Sets the return value of the function to 0 in the eax register.
pop rbp: Restores the base pointer to the its value in the calling function.
ret: Returns from the function, popping the return address off the stack and jumping back to the caller.
Key Points and Corrections

Dereferencing: Your understanding of [rbp-4] being similar to dereferencing a pointer in C is correct. It means "access the memory location whose address is calculated by subtracting 4 from the value in the rbp register".
Stack Allocation: Each int does indeed take up 4 bytes on the stack in this context.
Registers for Efficiency: Registers are used for calculations because accessing them is much faster than accessing values on the stack.
Let me know if you want a more in-depth explanation of any particular aspect!


CTFS
----------
- https://ctftime.org/writeup/26962
- https://www.stackzero.net/gdb-baby-step-1/
