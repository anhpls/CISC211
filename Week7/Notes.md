8421

0100 XOR 

![image-20250317121725221](/Users/anhpls/Library/Application Support/typora-user-images/image-20250317121725221.png)
optional for encryption

![](/Users/anhpls/Library/Application Support/typora-user-images/image-20250317120803152.png)

![image-20250317120840674](/Users/anhpls/Library/Application Support/typora-user-images/image-20250317120840674.png)




X AND Y OR Z
Init x,y, z with int 

paper then code


(X AND Y) OR Z

_start

mov eax, [x]

and eax, [y]

or eax, [z]

mov [result], eax

mov eax, 1
Int 0x80

initialize vars:
x = 10 --> 1010

y = 5 --> 0101

z = 15 --> 1111

1010





mov eax, [x]

and eax, [y]

mov ebx, [z]

or eax, ebx

mov [result], eax

![image-20250319121146489](/Users/anhpls/Library/Application Support/typora-user-images/image-20250319121146489.png)

mov eax, 10

TEST eax, 10       ;test instruction won't overwrite the eax register 
use gdb to check eax



```
section .text
        global _start

_start:
   mov eax, [x]
   and eax, [y]
   or eax, [z]
   mov [result], eax ;store eax in result

	mov eax,1
	int 0x80

section .data
    x dd 10 
    y dd 5 
		z dd 15 
    
segment .bss
    result resd 1



```

