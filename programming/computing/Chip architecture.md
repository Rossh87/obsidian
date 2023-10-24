1. https://www.redhat.com/en/topics/linux/ARM-vs-x86
2. https://phoenixnap.com/kb/x64-vs-x86#:~:text=A%2032%2Dbit%20processor%20on,memory%20a%20computer%20can%20utilize.&text=Introduced%20in%201978.

Overview: ARM and x86-based chips can be made to perform comparably in most ways; there are supercomputers based on each. But in current consumer markets, ARM devices are favored for applications where power consumption and cooling are the main constraints (e.g. phones), x86 is common for applications where performance is the main concern (e.g. desktop computers, servers). But this is not universally true: Apple M1 chips are ARM-based.

Key differences:
1. x86 hardware is manufactured specifically by Intel and AMD; ARM Holdings licenses its designs to multiple chip manufacturers
2. Components of x86 systems have separate controllers on separate components; components of ARM systems are integrated on the same physical substrate (SoC, or system-on-a-chip) 
3. x86 CPUs use complex instruction set (CISC: variable length instructions), where single instructions can complete entire operations. ARM CPUs use reduced instruction set (RISC: fixed 32-bit instructions), with lower-level instructions that need to be combined to perform discrete tasks. CISC needs more transistors, which = more space/power, and more expensive and complicated hardware generally. RISC is harder for the assembly programmer and/or compiler.
4. In reality the differences are smaller than they seem, because modern CPUs all internally convert instruction to micro-ops, which is what actually gets executed.
5. Host of other differences involving use of registres, chip-specific ISA extensions, etc.

X64 is a modern extension of X86, based on 64-bit rather than 32-bit words. In most cases, 64-bit is strictly more performant than 32-bit architecture, but it does consume more power, and backwards-compatibility with older 32-bit devices can be spotty in some domains.