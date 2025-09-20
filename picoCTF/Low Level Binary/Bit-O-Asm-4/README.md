
### `Bit-O-Asm-4.md`

```markdown
# Bit-O-Asm-4: Branching and Jumps 🛣️

This final challenge introduces conditional logic using comparison (**`cmp`**) and jump (**`jle`**, **`jmp`**) instructions, which are the assembly equivalent of if-else statements.

```assembly
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710
<+29>:    jle    0x55555555514e <main+37>
<+31>:    sub    DWORD PTR [rbp-0x4],0x65
<+35>:    jmp    0x555555555152 <main+41>
<+37>:    add    DWORD PTR [rbp-0x4],0x65
<+41>:    mov    eax,DWORD PTR [rbp-0x4]
<+44>:    pop    rbp
<+45>:    ret

## Analysis

The program's execution flow depends on a comparison:

    At 

    <+15>, the value at memory location [rbp-0x4] is set to 0x9fe1a.

At 

<+22>, this value is compared (cmp) to 0x2710.

At 

<+29>, the jle instruction checks if 0x9fe1a is "less than or equal to" 0x2710. Since this is false, the jump is not taken, and execution continues to the next line.

At 

<+31>, 0x65 is subtracted (sub) from the value at [rbp-0x4]. The new value becomes 

0x9fe1a - 0x65 = 0x9FDB5.

At 

<+35>, an unconditional jump (jmp) causes the program to skip the add instruction at <+37> and go directly to <+41>.

At 

<+41>, the final value, 0x9FDB5, is moved into the eax register.

## Conversion & Flag

The resulting hexadecimal value is converted to decimal.

    Hexadecimal: 0x9FDB5 

Decimal: 654773 

Answer: picoCTF{654773} 