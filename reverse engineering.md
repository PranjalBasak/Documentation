tools

objdump -> disassembler
gdb -> debugger
binwalk -> examines binary images for embedded files
IDA Pro
Ghidra

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/1f094477-97cc-416c-b13f-d74c54ac1a80)

file <file>

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
Introductory/Recap: https://www.youtube.com/watch?v=nLp3hr6Jf2M

Resources
----------------
- https://0xinfection.github.io/reversing/
- https://osandamalith.com/2019/02/11/linux-reverse-engineering-ctfs-for-beginners/


CTFS
- https://ctftime.org/writeup/26962
- https://www.stackzero.net/gdb-baby-step-1/
