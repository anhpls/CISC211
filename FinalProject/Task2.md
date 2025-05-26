# Task 2

By Anh Huynh



**Counter 1 to 20,000 (without Recursion)**

```assembly
SECTION .data
    filename db 'counter_fun.txt', 0
    newline db 10
    x dd 20000

SECTION .bss
    fd_out resb 4
    result resb 1

SECTION .text
   global _start

_start:
    ; --- create & open file --- 
    mov eax, 8              ; sys_creat
    mov ebx, filename
    mov ecx, 0711o          ; permissions (read/write/execute)
    int 0x80
    mov [fd_out], eax       ; store file descriptor

    ; --- call counter function and pass in x --- 
    push DWORD [x]
    call _counter
    add esp, 4

    ; --- close ---
    mov eax, 6          ; sys_close
    mov ebx, [fd_out]
    int 0x80

    ; --- exit ---
    mov eax, 1
    xor ebx, ebx
    int 0x80

;-------------------------------------------
; _counter: prints numbers from 1 to x
_counter:
    push ebp	       ; save, ebp = 0
	mov ebp, esp       ; esp points to ebp
    push ebx           ; save EBX

    mov ecx, 1         ; counter = 1
    mov edx, [ebp+8]   ; edx = x 

.count_loop:
    cmp ecx, edx       
    ja .done           ; if counter > x, done

    ; print current number
    push ecx           ; save counter
    push edx           ; save limit
    mov eax, ecx       ; number to print in EAX
    call print_num
    call print_newline
    pop edx            ; restore limit
    pop ecx            ; restore counter

    inc ecx            ; counter++
    jmp .count_loop
    
.done:
    pop ebx            ; restore EBX
    pop ebp            ; restore EBP
    ret

;-------------------------------------------
; print_num: prints EAX as ASCII
print_num:
    push ebx           ; save EBX
    push ecx           ; save ECX

    ; convert digits to ASCII
    mov ebx, 10          ; divisor
    xor ecx, ecx         ; clear digit counter

.calculate:
    xor edx, edx
    div ebx              ; EAX = quotient, EDX = remainder 
    push edx             ; save EDX (remainder digit)
    inc ecx              ; digit count++
    cmp eax, 0
    jne .calculate

.print_loop:
    pop eax
    add eax, 48          ; convert to ASCII
    mov [result], eax
    call display
    dec ecx
    jnz .print_loop

    pop ecx
    pop ebx
    ret

;-------------------------------------------
; display: prints the num in [result]
display:
    push eax
    push ebx
    push ecx
    push edx

    mov eax, 4              ; sys_write
    mov ebx, [fd_out]
    mov ecx, result
    mov edx, 1
    int 0x80

    pop edx
    pop ecx
    pop ebx
    pop eax
    ret

;-------------------------------------------
; print_newline: print newline (10)
print_newline:
    push eax
    push ebx
    push ecx
    push edx

    mov eax, 4              ; sys_write
    mov ebx, [fd_out]
    mov ecx, newline
    mov edx, 1
    int 0x80

    pop edx
    pop ecx
    pop ebx
    pop eax
    ret
```



**Counter 1 to 20,000 (with recursion)**

```assembly
SECTION .data
    filename db 'counter_rec.txt', 0
    newline db 10
    x dd 20000

SECTION .bss
    fd_out resb 4
    result resb 1

SECTION .text
   global _start

_start:
    ; --- create & open file --- 
    mov eax, 8              ; sys_creat
    mov ebx, filename
    mov ecx, 0711o          ; permissions (read/write/execute)
    int 0x80
    mov [fd_out], eax       ; store file descriptor

    ; --- call counter function and pass in x --- 
    mov eax, 1
    push DWORD [x]     ; push in x
    push eax           ; push counter (1)
    call _counter
    add esp, 8         ; clean up two arguments after function

    ; --- close ---
    mov eax, 6          ; sys_close
    mov ebx, [fd_out]
    int 0x80

    ; --- exit ---
    mov eax, 1
    xor ebx, ebx
    int 0x80

;-------------------------------------------
; _counter: using recursion, prints numbers from current counter (1) to x
; Parameters:
;     [esp+4] = current counter (1)
;     [esp+8] = limit (x)
_counter:
    push ebp	       ; save, ebp = 0
	mov ebp, esp       ; esp points to ebp
    push ebx           ; save EBX

    mov ecx, [ebp+8]    ; counter = 1
    mov edx, [ebp+12]   ; edx = x 

    cmp ecx, edx
    ja .done           ; jump done if counter > x

    ; print current number
    push ecx           ; save counter
    push edx           ; save limit
    mov eax, ecx       ; number to print in EAX
    call print_num
    call print_newline
    pop edx            ; restore limit
    pop ecx            ; restore counter

    inc ecx            ; counter++
    push edx           ; x
    push ecx           ; counter
    call _counter
    add esp, 8         ; clean up
    
.done:
    pop ebx            ; restore EBX
    pop ebp            ; restore EBP
    ret

;-------------------------------------------
; print_num: prints EAX as ASCII
print_num:
    push ebx           ; save EBX
    push ecx           ; save ECX

    ; convert digits to ASCII
    mov ebx, 10          ; divisor
    xor ecx, ecx         ; clear digit counter

.calculate:
    xor edx, edx
    div ebx              ; EAX = quotient, EDX = remainder 
    push edx             ; save EDX (remainder digit)
    inc ecx              ; digit count++
    cmp eax, 0
    jne .calculate

.print_loop:
    pop eax
    add eax, 48          ; convert to ASCII
    mov [result], eax
    call display
    dec ecx
    jnz .print_loop

    pop ecx
    pop ebx
    ret

;-------------------------------------------
; display: prints the num in [result]
display:
    push eax
    push ebx
    push ecx
    push edx

    mov eax, 4              ; sys_write
    mov ebx, [fd_out]
    mov ecx, result
    mov edx, 1
    int 0x80

    pop edx
    pop ecx
    pop ebx
    pop eax
    ret

;-------------------------------------------
; print_newline: print newline (10)
print_newline:
    push eax
    push ebx
    push ecx
    push edx

    mov eax, 4              ; sys_write
    mov ebx, [fd_out]
    mov ecx, newline
    mov edx, 1
    int 0x80

    pop edx
    pop ecx
    pop ebx
    pop eax
    ret
```



## Comparison

Time Output for counter_fun.txt

```
real    0m0.002s
user    0m0.001s
sys     0m0.000s
```



Time Output for counter_rec.txt

```
real    0m0.002s
user    0m0.000s
sys     0m0.001s
```



##### Efficiency

According to the time output for both the function and the recursive version of the function, there is a slight difference in the system execution time. It shows that the execution time for the recursive function is longer and this is due to the fact that there are more stack calls within the recursive version. The stack is being overloaded more than it is within the regular function call since the function utilizes a count loop. So in this case of printing values from 1 to x, the function call is more efficient than the recursive version. 