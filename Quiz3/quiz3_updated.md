```assembly
section .text
	global _start

_start:
    ; "Factorial of "
    mov eax, 4
    mov ebx, 1
    mov ecx, msg
    mov edx, msg_len
    int 0x80

    ; x as ASCII
    mov eax, [x]
    add eax, '0'
    mov [result], eax
    call display

    ; ": "
    mov eax, 4
    mov ebx, 1
    mov ecx, colon
    mov edx, 2
    int 0x80
    
    mov ecx, [x] ; counter
    mov eax, 1   ; eax is accumulated factors of nums

nums:
    mul ecx      ; eax *= ecx
    loop nums

    cmp eax, 9
    jg calculate
    call display_2
    call exit

calculate:
    mov ebx, 10
    div ebx
    push edx        ;edx holds remainder
    cmp eax, 9
    jg calculate
    push eax        ;eax holds quotient

    pop eax         
    add eax, 48
    mov [result], eax
    call display

    pop eax
    add eax, 48
    mov [result], eax
    call display

    pop eax
    add eax, 48
    mov [result], eax
    call display

    call linefeed
    call exit
   
display: 
    mov eax, 4
    mov ebx, 1
    mov ecx, result
    mov edx, 1
    int 0x80
	ret

;one digit print
display_2:
    add eax, 48
    mov [result], eax
    call display
    call linefeed
    ret

linefeed:
    mov eax, 4
    mov ebx, 1
    mov ecx, space
    mov edx, 1
    int 0x80
    ret

exit:
    mov eax, 1
    int 0x80

section .bss
    result resb 1

section .data
    x dd 5
    msg db 'Factorial of ', 0
    msg_len equ $ - msg
    colon db ': ', 0
    space db 0xa
```

