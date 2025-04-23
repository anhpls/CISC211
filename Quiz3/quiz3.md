```assembly
section .text
	global _start

_start:
    mov ecx, [x] ; counter
    mov eax, 1   ; eax is accumulated sum of nums

nums:
    mul ecx      ; eax *= ecx 
    loop nums

    mov [result], eax   ;move eax into result

   ; print to terminal
    mov eax, 4
    mov ebx, 1
    mov edx, msg_len
    mov ecx, msg
    int 0x80

    ; exit Program
    mov eax, 1
    int 0x80

section .bss
    result resd 1

section .data
    x dd 5
    msg db 'The factorial of 5 is 120', 10
    msg_len equ $ - msg
```

