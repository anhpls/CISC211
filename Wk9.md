1. 

```assembly
section .text
        global _start

_start:
        mov eax, 0

increase:
        test eax, 1 ;check if even
        jnz skip ;jump to skip block if odd

        mov al, byte al
        add al, '0'
        mov [tmp], al

        push eax

        ; print the character
        mov eax, 4
        mov ebx, 1
        mov ecx, tmp
        mov edx, 1
        int 0x80

        ;the following code add extra line
        mov eax, 4
        mov ebx, 1
        mov ecx, space
        mov edx, 1
        int 0x80

        pop eax
        

skip:
        inc eax
        cmp eax, 21
        jl increase

        ;exit
        mov eax,1
        int 0x80

        
segment .bss
        tmp resb 1

section .data
        space dd 10


```





2. 

```assembly
section .text
        global _start

_start:
        mov eax,[num1]
        cmp eax,[num2]  ; compare the first operand with the second operand
        jg checknum3    ; if eax > num2, jump to num3 check
        mov eax,[num2]

checknum3:
        cmp eax,[num3]
        jg checknum4    
        mov eax,[num3]

checknum4:
        cmp eax,[num4]
        jg checknum5
        mov eax,[num4]

checknum5:
        cmp eax,[num5]
        jg exit
        mov eax,[num5]

exit:
        mov [largest],eax
        
        mov eax,1
        int 0x80

section .data
        num1 dd 30
        num2 dd 20
        num3 dd 10
        num4 dd 15
        num5 dd 50

segment .bss
        largest resd 1
```

