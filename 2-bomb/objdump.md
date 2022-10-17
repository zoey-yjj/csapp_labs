## **`objdump` commands**

to find out information from an object file and help in debugging the object file. It is used for the following listed purposes:

- To retrieve archive header
- To get the offset of the file
- To get the bfdname
- To get the demangle
- To debug the file
- To disassemble the file
- To retrieve the file headers

syntax

```properties
objdump <option(s)> <file(s)>
```

usage

1. to get the file headers of and object file

    ```properties
    objdump -f filename
    ```

2. to print the object-specific file header content

    ```properties
    objdump -p filename
    ```

3. to print the section header content of the file

    ```properties
    objdump -h filename
    ```

4. to print the all header content of the file

    ```properties
    objdump -x filename
    ```

5. to print the assembler content of the section capable of execution

    ```properties
    objdump -d filename
    ```

6. to print the assembler content of all the sections of the file

    ```properties
    objdump -D filename
    ```

7. to print the complete content of all the sections of the file

    ```properties
    objdump -s filename
    ```

8. display help sections

    ```properties
    objdump --help
    ```

