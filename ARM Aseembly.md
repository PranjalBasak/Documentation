ARM processors have two main states - ARM (32 bit) and Thumb (16 bit)

Thumb-1
Thumb-2
Thumb-EE

ARM supports conditional Execution

MNEMONIC{S}{condition} {Rd}, Operand1, Operand2

Intel x86 -> Little Endian
ARM -> Big Endian

https://azeria-labs.com/arm-instruction-set-part-3/

swi 0 means software interrupt

### Kernel
- r7 handles what we do
- r0-r4 handles how we do it

- arm 32 bit system call table

Generally, LDR is used to load something from memory into a register, and STR is used to store something from a register to a memory address.

movk = move the immediate value but keep the previous

intel x86 = rax(eax(ax(ah|al
arm = x0(w0
x0 = 64 bit
w0 = 32 bit


CTFs
Xoss List

https://github.com/apoirrier/CTFs-writeups/blob/master/PicoCTF/Reversing/ARMssembly0.md
https://ctftime.org/writeup/26963
