# level01

## login with user "level01"
No clue at all! Again!

## Ask a student who already done the project
Yeh, how do I know I should look inside that "/etc/passwd" file if I never think of it.
Important to have a friend as a HACKER.

## [Understanding /etc/passwd file in linux](https://dev.to/kcdchennai/understanding-etcpasswd-file-in-linux-1k2d)

## The "flag01" line in passwd file
All other lines has their password marked as "x" except the line "flag01":
`flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash`
This is the "legacy" and unsecure way of storing password in linux system whitch we can exploit.

## Use `scp`
Use scp to copy file from vm to host machine:
`scp -P 4242 level01@192.168.56.102:/etc/passwd ~/`

## Install `john` and run it
`john ~/passwd -show`
The line becomes:
`flag01:abcdefg:3001:3001::/home/flag/flag01:/bin/bash`

## Takeaway
- Check "etc/passwd" or "/etc/shadow" file for hashed password info.
- Usage of "scp" command
- Usage of "john the ripper"  to crack password
