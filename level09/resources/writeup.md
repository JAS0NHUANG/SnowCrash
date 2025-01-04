# level09

## Seems so easy?!
```
level09@SnowCrash:~$ ls
level09  token
level09@SnowCrash:~$ cat token
f4kmm6p|=�p�n��DB�Du{��
level09@SnowCrash:~$ ./level09 token
tpmhr
```

But both "f4kmm6p|=�p�n��DB�Du{��" and "tpmhr" are not the real token...

## Try to decode the level09 executable rules
```
level09@SnowCrash:~$ ./level09 abc
ace
level09@SnowCrash:~$ ./level09 aaa
abc
level09@SnowCrash:~$ ./level09 123
135
level09@SnowCrash:~$ ./level09 000
012
level09@SnowCrash:~$ ./level09 0000000000
0123456789
level09@SnowCrash:~$ ./level09 00000000000
0123456789:
level09@SnowCrash:~$ 
```

It does some incrementation on each character.
`new char = char ascii code + index`

## Decode with a python script

```
# python2
line = open('/home/user/level09/token').read().strip()
print 'res/', ''.join(chr(ord(_) - i) for i,_ in enumerate(line))
```



