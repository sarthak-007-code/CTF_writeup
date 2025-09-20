
### `Bit-O-Asm-2.md`

```markdown
# Bit-O-Asm-2: Pointers and Memory 🧠

This challenge demonstrates how values can be stored in memory and then retrieved into a register. It introduces the concept of using a pointer, in this case, an offset from the base pointer register (**`rbp`**), to access data.

```assembly
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    mov    eax,DWORD PTR [rbp-0x4]
<+25>:    pop    rbp
<+26>:    ret

## Analysis

The process occurs in two main steps:

    <+15>: mov DWORD PTR [rbp-0x4],0x9fe1a: The hexadecimal value 0x9fe1a is stored in a memory location at an address calculated as rbp - 4.

<+22>: mov eax,DWORD PTR [rbp-0x4]: The value at that same memory location ([rbp-0x4]) is then copied into the eax register.

The final value in 

eax is therefore 0x9fe1a.

## Conversion & Flag

Converting the final hexadecimal value to decimal provides the solution.

    Hexadecimal: 0x9fe1a 

Decimal: 654874 

Answer: picoCTF{654874} 