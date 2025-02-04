# Week 1: Introduction to Computer Systems

[ASCII Table](https://www.lookuptables.com/text/ascii-table)

Hexadecimal
My name:
416e68204875796e68
Anh Huynh

8 bits = 1 byte
2 words (2 x 8) = 16 bits
10 bytes = 8 bits \* 10 bytes = 80 bits

```
NAND
both have to be true to = true

NOR

    true + true = false
    true + false = false
    false + true = false
    false + false = true

XOR
evaluates true when only one is true. if both are true or both are false, the output is false
T + T = F
T + F = T
F + T = T
F + F = F
```

---

bitwise NOT / bitwise complement performs the negation of each bit
0 = 1
1 = 0

```
Example: NOT   0111  (decimal 7)
          1000  (decimal 8)
```

section .text
global \_start ;must be declared for linker (ld)
;global is used to export the \_start label.
;This will be the entry point to the program.

\_start: ;tells linker entry point
mov eax,4 ;system call number (sys_write)
mov ebx,1 ;file descriptor (stdout)
mov ecx,msg ;message to write, A pointer to the variable 'msg'
mov edx,len ;message length
int 0x80 ;call kernel
mov eax,1 ;system call number (sys_exit)
int 0x80 ;call kernel

section .data
msg db 'Hello, world!', 0xa ;string to be printed
;Declare a label "msg" which has
;our string we want to print.
;for reference: 0xa = "\n" (line feed)
;db = define byte
len equ $ - msg ;length of the string
;len" will calculate the current
;offset minus the "msg" offset.
;this should give us the size of "msg".
;len equals current offset - msg
