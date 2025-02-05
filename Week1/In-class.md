```
AND, OR, NOT
F.X = F
1 1 = 1 TRUE
1 0 = 0
0 1 = 0 FALSE
0 0 = 0
if one condition is false, then response is false

T F = !F = T    Not false sets to true
NAND inverts the output/result

T and T = T NAND makes it F

XOR
T T F
T F T
F T T
F F F

"NOT" means invert. decimal = base 10 dec
0111 = 1000

AND
0101    Whenever you get 0 once, you get zero
0011    <- this reads downwards
0001

XOR     Diff = True         Same = False

0010
1010
1000

These are trick tables of two inputs
Trick tables = all possible inputs to that code
Test all possible options for when creating codes
Ex: Create a username:
    Could be all numbers
    Could be Alphabet and numbers
    Could be special case / special characters

For sign-magnitude
 4 =   1 0 0
-4 = 1 1 0 0 --> have to let the computer know this is not 12
     8 4 2 1
     sign magnitude to let the comp. know that the first 1 is a sign
Sign-magnitude
4 would be represented as: 00000100
-4: 100000100
With 1's complement:
4: 00000100
-4:11111011

NEW COMMON Way of Writing a Negative Number
Step 1. Start with the equivalent positive number
Step 2. Inverting all bits - change every 0 to 1, every 1 to 0
Step 3. Add 1 to the entire inverted number,


-6      0110

+6      1001
           1
        ----
-6      1010    (2's complement. must explain or state that)

+8      1000
NOT +8  0111    (1's complement)

        1000
        0111
           1
        ----
        0010 (2's complement)

A = converts into Binary
Every keystroke has a Decimal No.
A = 65, B = 66
1  0  0  0 0 0 1    Letter A
1  0  0  0 0 1 0    Letter B
64 32 16 8 4 2 1
0  0  0  0 0 1 1    A XOR B =
1  0  0  0 0 1 0    Key
1  0  0  0 0 0 1    XOR

Compressor vs Decompressor / Encryption
XOR Same = False    Difference = True
1 time pad/1 time encryption by using a message and a key that is used only one time

```
