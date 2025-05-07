```assembly
section .text
	global _start

_start:
	push DWORD [z]     ; push z as third arugment [ebp+16]
    push DWORD [y]     ; push y as second argument [ebp+12]
    push DWORD [x]     ; push x as first argument [ebp+8]
	call _add_variables  ; call function _add_variables
    add esp, 12          ; clean stacks after returned eax from function

    mov [result], eax    ; store return value in result variable

    ; print result
    cmp eax, 9            ; compare to 9
    jg .print_number      ; if > 9 jump to print_num
    call display_2        ; if x <= 9, print with display_2
    jmp .end              ; then jump .end

.print_number:
    mov ebx, 10           ; divisor
    xor ecx, ecx          ; counter 

; % 10 to print digits
.calculate:
    xor edx, edx
    div ebx             ; eax / 10: quotient in eax, remainder in edx
    push edx            ; push digit
    inc ecx             ; increment counter
    cmp eax, 0
    jne .calculate      ; loop for all digits

; print each digit by their ASCII
.print_loop:
    pop eax             ; pop digit from stack
    add eax, 48         ; convert to ASCII
    mov [result], eax   ; store in result
    push ecx            ; push counter since display uses ecx
    call display        ; print digit
    pop ecx             ; restore counter
    dec ecx             ; decrement ecx
    jnz .print_loop     ; loop until all digits printed

.end:
    call linefeed
    call exit

;;; ;------------------------------------------------------
;;; ;------------------------------------------------------
;;; ; _add_variables: pass through variables x, y, z.
;;; ; 				  Add x+y+z and return in eax
;;; ;
;;; ;------------------------------------------------------
;;; ;------------------------------------------------------

_add_variables:
	push ebp	       ; ebp = 0
	mov ebp, esp       ; esp points to ebp

    mov eax, DWORD[ebp+8]   ; eax = x
    add eax, DWORD[ebp+12]  ; x + y
    add eax, DWORD[ebp+16]  ; x + y + z

    leave
    ret

; ------------------------------------------------------

;display multiple digits
display:
    mov eax, 4
    mov ebx, 1
    mov ecx, result
    mov edx, 1
    int 0x80
    ret

;display one digit
display_2:
    add eax, 48
    mov [result], eax
    call display
    ret

linefeed:
    mov eax, 4
    mov ebx, 1
    mov ecx, newline
    mov edx, 1
    int 0x80
    ret
	
exit:
	mov eax, 1
	int 0x80

section .bss
    result resb 1
	
section .data
	x dd 10
    y dd 20
    z dd 50

    newline db 10

```