 [W6 Flowchart.pdf](../../../../Downloads/W6 Flowchart.pdf) 

**Task 1:**

```
section .text
        global _start

_start:
    mov eax, 0
    sub eax, [var1] ;0 -10 = -10
    imul eax, 10 ;-10 * 10

    mov [result], eax

		mov eax,1
		int 0x80

section .data
    var1 dd 10 ; var1 is assigned 10

segment .bss
    result resb 1
```

**Task 2:**

```
section .text
        global _start

_start:
    mov eax, [var1] ;mov 10 to eax
    add eax, [var2] ;add var2
    add eax, [var3] ;add var3
    add eax, [var4] ;add var4
    mov [result], eax ;mov eax to result

		mov eax,1
		int 0x80

section .data
    var1 dd 10 ;var1 = 10
    var2 dd 5 ;var2 = 5
    var3 dd 25 ;var3 = 25
    var4 dd 40 ;var4 = 40

segment .bss
    result resd 1

```

**Task 3:**

```
section .text
        global _start

_start:
    mov eax, 0
    sub eax, [var1] ;negative var1
    imul eax, [var2] ;signed mul by var2

    mov ebx, [var3] ;var3 into ebx
    add eax, ebx ;eax = (-var1 * var2) + var3

    mov [result], eax ;store eax in result

		mov eax,1
		int 0x80

section .data
    var1 dd 10 ;var1 = 10
    var2 dd 5 ;var2 = 5
    var3 dd 25 ;var3 = 25

segment .bss
    result resd 1


```

**Task 4:**

```
section .text
        global _start

_start:
    mov ebx, [var1] ;mov 10 to ebx
    imul ebx, 2 ;ebx = var1 * 2

    mov ecx, [var2] ;mov 5 to ecx
    sub ecx, 3 ;ecx = var2 - 3 (5 - 3 = 2)

    mov eax, ebx ;eax = 20
    idiv ecx ;eax = (20)/(2)

    mov [result], eax ;store eax in result

		mov eax,1
		int 0x80

section .data
    var1 dd 10 ;var1 = 10
    var2 dd 5 ;var2 = 5

segment .bss
    result resd 1

```
