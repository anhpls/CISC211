```assembly
section .text
	global _start

_start:
    mov ecx, [x] ; counter
    mov eax, 1   ; eax is accumulated sum of nums

nums:
    mul ecx      ; eax *= ecx 
    loop nums

    mov [result], eax   ; move eax into result

   ; print message
    mov eax, 4
    mov ebx, 1
    mov ecx, msg
    mov edx, msg_len
    int 0x80

    ; convert to ascii
    mov eax, [result]
    add eax, '0'
    mov [result], eax

    ; print result
    mov eax, 4
    mov ebx, 1
    mov ecx, result
    mov edx, 1
    int 0x80

    ; newline
    mov eax, 4
    mov ebx, 1
    mov ecx, newline
    mov edx, 1
    int 0x80

    ; exit Program
    mov eax, 1
    int 0x80

section .bss
    result resd 1

section .data
    x dd 3
    msg db 'Factorial of 3 is ', 0
    msg_len equ $ - msg
    newline db 10
```

The output in terminal is:
"Factorial of 3 is 6"