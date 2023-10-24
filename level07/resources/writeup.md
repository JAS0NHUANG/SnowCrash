# level07

## another executable
Run "level07" file and we just got "level07" print out.

With the tools that we learned in level0X. We can check the binary file by running `file`, `strings`, and `ltrace`. And also `ls -la` to check if it got higher privelege.  

By running `ltrace` we can see that it called `getenv()` and then maybe pass the result into the `system()` function:
```
...
getenv("LOGNAME")                                        = "level07"
...
system("/bin/echo level07 "level07
...
```

## Code injection by env modification
Since it simply take "LOGNAME" env variable add pass it to `system()` function. I try to change the LOGNAME by `export LOGNAME=flag07`. This just changed the output to "flag07". `export LOGAME=getflag` prints out "getflag". Then I have a nice idea: "Why not just pass in the "getflag" command with a `;` in front of it?"  
`export LOGNAME=";getflag"`  
And it just worked.  

## Takeaway
- System calls and shell behavior

