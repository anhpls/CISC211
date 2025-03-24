# Calculate the mean of the following dataset using assembly language

## Formulas

$Mean=Sum of students/number of students$

| Name      | score |
| --------- | ----- |
| Student 1 | 60    |
| Student 2 | 70    |
| Student 3 | 90    |
| Student 4 | 40    |
| Student 5 | 65    |

## What to show?

Display the result on the terminal. You might need to verify the result using gdb

```
section .text
        global _start

_start:
        mov eax, [s1]
        add eax, [s2]
        add eax, [s3]
        add eax, [s4]
        add eax, [s5]

        mov ebx, 5
        div ebx

        mov [result], eax

        ;print to terminal
        mov	eax, 4       ;system call number (sys_write)
        mov	ebx, 1       ;file descriptor (stdout)
        mov	ecx, msg     ;message to write, A pointer to the variable 'msg'

        mov eax, [result]

        mov eax, 1
        int 0x80

section .data
        s1 dd 60
        s2 dd 70
        s3 dd 90
        s4 dd 40
        s5 dd 65

        msg db "Mean Score: ", [result]
segment .bss
        result resd 1
        mean resb 1
```

# Convert the following

- Convert 575 decimal into binary and hexadecimal
- Convert 0x80 into binary

```
575 % 2 = 287 R1 1
287 % 2 = 143 R1 1
143 % 2 = 71 R1  1
71 % 2 = 35 R1   1
35 % 2 = 17 R1   1
17 % 2 = 8 R1    1
8 % 2 = 4 R0     0
4 % 2 = 2 R0     0
2 % 2 = 1 R0     0
1 % 2 = 0 R1     1

Binary: 1000111111
```

# Represent the following into negative numbers

- Convert -10 into binary using 1's and 2's complements

# Identify error(s) in the following code

```assembly
section .text
    global _start

_start:
    mov eax,10
    mov ebx,20
    add eax,ebx
    mov result,eax

    mov eax,1
    int 0x80

section .data
    result resb 1
```

# Transfer the bits into the Cache memory

- 10111
- 10000
- 11101

| Index | V   | Tag | Data  |
| ----- | --- | --- | ----- |
| ----- | -   | --- | ----- |
| ----- | -   | --- | ----- |
| ----- | -   | --- | ----- |
| ----- | -   | --- | ----- |
