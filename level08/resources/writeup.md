# level08

## Executable plus token file
`./level08` -> `./level08 [file to read]`
`./level08 token` -> `You may not access 'token'`

`ltrace ./level08 token` -> 
```
__libc_start_main(0x8048554, 2, 0xbffff7d4, 0x80486b0, 0x8048720 <unfinished ...>
strstr("token", "token")                                        = "token"
printf("You may not access '%s'\n", "token"You may not access 'token'
)                    = 27
exit(1 <unfinished ...>
+++ exited (status 1) +++
```

Create a "token" file in /tmp and read it with ./level08 executable:
`ltrace ./level08 /tmp/token`
We got the same response.

Notes:
  1. The program cat the content of the file sent as argument.  
  2. The program checks if the filename contains "token". If yes, the programe will not print the content.  
  3. We don't have access to "~/token" file.(Can't read/write/copy/remove...etc)

## Bypass rights verification via symlink
Create a symbolic link to the file: `ln -s /home/user/level08/token /tmp/tsym`
(Must use the full path.)
Then read the file with  ./level08.

