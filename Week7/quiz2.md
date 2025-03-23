**The result is x = 350.**

```assembly
section .text
    global _start

_start:
    mov ebx, [a] ;move a to ebx
    imul ebx, [b] ;ebx = a * b

    mov ecx, [c] ;move c to ecx
    imul ecx, [d] ;ecx = c * d

    add ebx, ecx ;ebx = (a*b)+(c*d)
    mov eax, ebx ;move result of that to eax

    mov [x], eax ;store result in x

	mov eax,1
	int 0x80

section .data
    a dd 5 ;a = 5
    b dd 10 ;b = 10
    c dd 15 ;c = 15
    d dd 20 ;d = 20

segment .bss
    x resd 1
```

