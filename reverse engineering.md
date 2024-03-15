tools

objdump -> disassembler
gdb -> debugger
binwalk -> examines binary images for embedded files
IDA Pro
Ghidra

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


CTFS
----------
- https://ctftime.org/writeup/26962
- https://www.stackzero.net/gdb-baby-step-1/
