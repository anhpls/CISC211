# Problem 1

result = (var1 + 2) / (var3 - var2)



**a.**

var1 = 5

var2 = 20

var3 = 30

result = uninitialized

answer = uninitialized



**b.**

```assembly
section .text
        global _start

_start:
        mov eax, [var1] ;move var1 to eax regs
        add eax, 2      ;eax = var1 + 2

        mov ebx, [var3] ;move var3 to ebx regs
        sub ebx, [var2] ;ebx = var3 - var2

        div ebx         ;divide (var1 + 2) / (var3 - var2)

        mov [result], eax ;store eax in result var

        mov eax, [result] ;move result to eax
        add eax, '0'      ;converting to character
        mov [answer], al  

        ;print msg to console
        mov	eax, 4       ;system call number (sys_write)
        mov	ebx, 1       ;file descriptor (stdout)
        mov	ecx, msg
        mov	edx, msg_len ;message length
        int	0x80         ;call kernel

        ;print result variable to console
        mov eax, 4
        mov ebx, 1
        mov ecx, answer
        mov edx, 1
        int 0x80

        ;exit
        mov eax, 1
        int 0x80


section .data
        var1 dd 5         ;var1 = 5
        var2 dd 20        ;var2 = 20
        var3 dd 30        ;var3 = 30

        msg db 'Result: '
        msg_len equ $ - msg

segment .bss
        result resd 1
        answer resb 1
```

**c.** 

| Register Name   | Value |
| --------------- | ----- |
| EAX (Quotient)  | 0     |
| EDX (Remainder) | 7     |



##### d. Please check my repository for the screenshot of the gdb debugger verifying the above table.



# Problem 2

Y = ab + a'b + ab'

|      | b       | b'      |
| ---- | ------- | ------- |
| a    | 1 (ab)  | 1 (ab') |
| a'   | 1 (a'b) | 0       |

**Group 1:** ab + ab' = a (b + b') = a(1) = a

**Group 2:** ab + a'b = b (a + a') = b(1) = b

Y = a + b



# Problem 3

**a.**

1. move the variable to eax
2. set ebx to 2 as the divisor

2. check to see if eax is even or odd by dividing by ebx (2)

3. check remainder in edx 
4.  if remainder is 0, then jump to evnn block
   1. evnn block: 
      1. print msg_even
      2. exit
5. if remainder is not 0, then jump to odd block
   1. odd block:
      1. print msg_odd
      2. exit
6. Exit



```assembly
section .text
        global _start

_start:
        mov eax, [var1] ;move var1 to eax regs
        xor edx, edx    ;clear edx for proper division
        mov ebx, 2      ;ebx = 2

        div ebx         ;eax = var1 / 2

        cmp edx, 0      ;check if remainder is 0
        jz evnn         ;jump to evnn block if 0
                        ;if jump not 0, then continue

odd: 
        mov eax, 4          ; sys_write
        mov ebx, 1          ; stdout
        mov ecx, msg_odd
        mov edx, len_odd
        int 0x80

        ;exit
        mov eax,1
        int 0x80

evnn:
        mov eax, 4          ; sys_write
        mov ebx, 1          ; stdout
        mov ecx, msg_even
        mov edx, len_even
        int 0x80

        ;exit
        mov eax,1
        int 0x80

        ;exit program
        mov eax, 1
        int 0x80


section .data
        var1 dd 9         ;test var1 = 9 

        msg_even db 'Even number', 0xa
        len_even equ $ - msg_even

        msg_odd db 'Odd number', 0xa
        len_odd equ $ - msg_odd

segment .bss
        result resd 1
```







