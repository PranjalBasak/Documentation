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
