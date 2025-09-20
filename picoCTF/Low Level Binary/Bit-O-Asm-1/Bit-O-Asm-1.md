# Bit-O-Asm-1: Basic Data Movement 🔢

This first challenge introduces how a value is moved directly into a register. The goal is to find the decimal value stored in the **`eax`** register at the end of the execution.

```assembly
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x4],edi
<+11>:    mov    QWORD PTR [rbp-0x10],rsi
<+15>:    mov    eax,0x30
<+20>:    pop    rbp
<+21>:    ret

## Analysis

The key instruction in the assembly dump is at offset <+15>.

    mov eax,0x30: The mov instruction moves the hexadecimal value 0x30 directly into the eax register. The subsequent instructions clean up the stack but do not alter the value in 

    eax.

## Conversion & Flag

The final step is to convert the hexadecimal value to decimal.

    Hexadecimal: 0x30 

Decimal: 48 

This gives the final flag.

Answer: picoCTF{48} 


