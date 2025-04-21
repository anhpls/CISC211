1. 

```assembly
section .text
        global _start

_start:
        mov ebx, 10	;ebx = counter
        
label:
        dec ebx ;decrement
        jnz label ;if ebx != 0, jump to label

        mov eax, 1     
        xor ebx, ebx  ;clear ebx
        int 0x80
```



2. 

```assembly
section .text
        global _start

_start:
        mov eax, 0	;eax = [0]
        mov ebx, 1  ;ebx = [1]
        mov ecx, 9  ;

f_loop:
        mov edx, eax  ;edx = first index
        add edx, ebx  ;add first index to second index
        mov eax, ebx  ;eax as new first index
        mov ebx, edx  ;ebx as new second index ([first] + [second])
        loop f_loop   ;loop until ecx = 9
        
        
        mov eax, 1
        int 0x80
```



3.

```assembly
	global _start

_start:
    mov ecx, array   ; ecx = pointer
    mov eax, [ecx]   ; eax = assume [0] is max
    add ecx, 4       ; start from [1]

    mov edx, 3       ; 3 elements to check

loop_through:
    cmp edx, 0       ; loop until 0
    je exit          ; jump to done (end loop after going through all elements)

    mov ebx, [ecx]   ; current element
    cmp eax, ebx
    jge skip         ; if eax >= ebx, skip number
    mov eax, ebx     ; update max if not skipped
    
skip:
    add ecx, 4       ; move to next element by adding 4 bytes
    dec edx          ; decrease counter
    jmp loop_through

exit:
    mov [max], eax   ;move max num to max var

    mov eax, 1
    int 0x80

section .bss
    max resd 1

section .data
    array dd 5, 17, 29, 20
```



The challenges of this code assignment was part 3, where I needed to combine the use of a counter as well as a loop in order to loop through each element while the counter counts down to zero. Reaching zero would indicate to exit the program while skip would decrement the counter in addition to continuing to loop through the rest of the elements. While it loops through the elements, it compares the current index to the previous assigned of max value and if it isn't greater than or equal to, then it skips that element. The program was sort of complex but slowly it started to make sense. 