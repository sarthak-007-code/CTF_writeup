
### `Bit-O-Asm-3.md`

```markdown
# Bit-O-Asm-3: Assembly Arithmetic 🧮

This challenge builds on the previous concepts by adding arithmetic operations: multiplication (**`imul`**) and addition (**`add`**).

```assembly
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
<+36>:    add    eax,0x1f5
<+41>:    mov    DWORD PTR [rbp-0x4],eax
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
<+47>:    pop    rbp
<+48>:    ret

## Analysis

The value in eax is modified sequentially:

    At 

    <+29>, eax is loaded with the value at [rbp-0xc], which was set to 0x9fe1a at <+15>.

At 

<+32>, eax is multiplied (imul) by the value at [rbp-0x8], which was set to 4. The result is 

0x9fe1a * 4 = 0x27F868.

At 

<+36>, the value 0x1f5 is added (add) to eax. The result is 

0x27F868 + 0x1f5 = 0x27FA5D.

The final value in 

eax is 0x27FA5D.

## Conversion & Flag

The final hexadecimal result is converted to decimal for the flag.

    Hexadecimal: 0x27FA5D 

Decimal: 2619997 

Answer: picoCTF{2619997} 