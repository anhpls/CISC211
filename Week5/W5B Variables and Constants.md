**W5B Variables and Constants**

1. Flowchart not required for this assignment
2. Challenges were within gdb and creating a watch variable of result to check if result was properly moved into eax.

```section .text
section .text
        global _start

_start:
        mov eax, [var1] ;move var1 to eax
        mov ebx, [var2] ;move var2 to ebx
        add eax, ebx    ;add eax and ebx
        mov [result], eax ;move result into eax

        mov eax,1	;set eax register to 1 (do not remove this line)
        int 0x80	;interrupt 0x80 (do not remove this line)

segment .bss        ;use this space for uninitialized variable (result)
    result resb 4

segment .data       ;use this space for initialized variables (var1 and var2)
	var1 dd 10      ;initialized var1 to 10
    var2 dd 15      ;initialized var2 to 15
```
