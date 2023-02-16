# Split32

>## Notes
>
>rabin2 -i "file" --- functions in GOT  
>rabin2 -z "file" --- strings

Start examining the content of the file with rabin2 or ida.  
Then with pwngdb disassemble the function usefulFunction because when you look into it can see a call, so can be used.  

`b main` puts a brakepoint in the main function and run the program with `r`, now we can search for the string "/bin/cat flag.txt" that we found earlier using the decompilers, so now we can extract both directions, the call inside the usefulFunction and the string we wanted to execute.  
Now we need to find the size of the stack, using `cyclic int_value` for example `100`, a string gets print, copy that continue the program using `c` and paste the string from the cylic, press enter and it should have overflown the stack (if not try with bigger number)  
Next step is to use `cyclic -l "value_in_*EIP"` this value should appear before in the command line [REGISTERS], then it should print the offset needed to overflow.  

Last step is to do an one liner to make the binary.  

```console
python2 -c 'print "A"*44 +"\x1a\x86\x04\x08" + "\x30\xa0\x04\x08"' > input
```

>\x1a\x86\x04\x08 being the function direction  
>\x30\xa0\x04\x08 being the string direction

Next line to input the binary input, this should print the flag

```console
./split32 < input
```
