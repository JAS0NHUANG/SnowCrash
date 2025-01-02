# level00

## login with user "level00
`FIND` no clue at all!

## Found out the project intro VIDEO in intra
"FIND this first file who can run only as flag00..."  
No clue what it means? GIYF!  
Found this:[Exploit Education - Nebula](https://exploit.education/nebula/) (not so original our snow crash project XD)

## The FIND command
- `man find`. Use option `-user` to find file owned by user "uname"
- `find -user level00`
- Got loads of "permission denied" error
- add `2>/dev/null` to redirect stderr to null device
- Found a suspicious file: "/usr/sbin/john"
- "cdiiddwpgswtgt" is it's content. It is not the password for flag01. Again, GIYF! ^_^
- [dcode - Caesar Cipher](https://www.dcode.fr/caesar-cipher). Decode with the tool and it gives "nottoohardhere" as the most probable answer.
- `su` to "flag00" with the password and `getflag`

## Takeaway
- Usage of `find` command.
- Simple encoding(which is not encryption).
