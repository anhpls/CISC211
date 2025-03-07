**W5A First AL Program**

```
section	.text
   global _start		;must be declared for linker (ld)
   				;global is used to export the _start label. 
   				;This will be the entry point to the program. 

_start:	            ;tells linker entry point
   mov	eax,4       ;system call number (sys_write)
   mov	ebx,1       ;file descriptor (stdout)
   mov	ecx,msg     ;message to write, A pointer to the variable 'msg' 
   mov	edx,len     ;message length
   int	0x80        ;call kernel
	
   mov	eax,1       ;system call number (sys_exit)
   int	0x80        ;call kernel

section	.data
;msg2 db 'Hello, world!', 0xa
msg db 'This is the first line',0xa,'I am a coded to print these lines',0xa,'This is my last line',0xa  
                                ;strings to be printed 
                                ;Declare a label "msg" which has 
                              	;our string we want to print. 
                              	;for reference: 0xa = "\n" (line feed) 
                              	;db = define byte
len equ $ - msg     		;length of the string
				;len" will calculate the current 
				;offset minus the "msg" offset. 
				;this should give us the size of "msg".
                    		;len equals current offset - msg

```

