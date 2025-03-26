# Problem 1

result = (var1 + 2) / (var3 - var2)



**a.**

var1 = 5

var2 = 20

var3 = 30

result = uninitialized

answer = uninitialized



**b.**

```
section .text
        global _start

_start:
        mov eax, [var1] ;move var1 to eax regis
        add eax, 2      ;eax = var1 + 2

        mov ebx, [var3] ;move var3 to ebx regis
        sub ebx, [var2] ;ebx = var3 - var2

        div ebx         ;divide (var1 + 2) / (var3 - var2)

        mov [result], eax ;store eax in result var

        mov eax, [result] ;move result to eax
        add eax, '0'      ;converting to character
        mov [answer], al  ;move accumulator low to answer var

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
| EBX (Remainder) | 7     |



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

1. move variable to eax
2. set ebx to 2 as the divisor

2. check to see if eax is even or odd by dividing by ebx 

3. check remainder in edx 
4.  if remainder is 0, then jump to evnn block
   1. evnn block: 
      1. set eax to 2
      2. move eax to result
      3. exit
5. if remainder is not 0, then jump to odd block
   1. odd block:
      1. set eax to 1
      2. move eax to result
      3. exit



```assembly
section .text
        global _start

_start:
        mov eax, [var1] ;move var1 to eax regis
        mov ebx, 2      ;ebx = 2

        div ebx         ;eax = var1 / 2
        je evnn         ;jump to evnn block if 0
                        ;if jump not 0, then continue

        mov eax, 1
        int 0x80

evnn:
        mov eax, 2     
        mov [result], eax ;set result to 2 if even

        ;exit
        mov eax,1
        int 0x80

odd: 
        mov eax, 1     
        mov [result], eax ;set result to 1 if odd

        ;exit
        mov eax,1
        int 0x80

section .data
        var1 dd 9         ;var1 = 9

segment .bss
        result resd 1



```







