1. A challenge while performing this lab was trying to implement a TEST instruction scenario while also implementing the XOR operand without it skipping over one or the other during every execution. Figured out that I should use TEST first to check IF a register is 0, and if it's not, I can force the next register to be 0 to execute the jump evnn.

```
section .text
        global _start

_start:
        mov eax, [var1] ;move var1 to eax regis
        test eax, eax   ;test eax if eax is 0
        jz evnn         ;jump to evnn block if 0
                        ;if jump not 0, then continue

        mov ebx, [var2] ;move var2 to ebx regis
        xor ebx, ebx    ;changes ebx to 0 with xor
        jz evnn         ;jump since 0

        mov eax, 1
        int 0x80

evnn:
        mov eax, 200
        mov [result], eax ;this will print 200 in result

        mov eax,1
        int 0x80

section .data
        var1 dd 10        ;var1 = 10
        var2 dd 20        ;var2 = 20

segment .bss
        result resd 1
```
