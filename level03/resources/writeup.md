# An executable file
run "./level03" shows "Exploit me"

## Still GIYF
- `string` command shows `setresgid`, `setresuid`, `system`, `getegid`,`geteuid` functions are used in the source code.
- `ltrace` also shows these function calls.

## script injection
Inside the system functioncall, the program calls the "/usr/bin/env echo ....."
According to the exploit method found online. We can write a shell script and make the system call it.
1. `ls -la` to make sure "level03" file is owned by other user then "level03".(it's owned by flag03)
2. `echo "/bin/bash" > /tmp/echo` to make a fake echo program in which we launch a shell.
3. `export PATH=/tmp:$PATH` to add "/tmp" in front of other path.( So the system will find the program first inside /tmp folder)
4. Launch the level03 binary again. And~~~ our shell becomes "flag03@SnowCrash:~" instead of "level03@SnoCrash:~". Successfuly escalated the user right to flag03 :D
5. Now we can run the "getflag" command and get the token

