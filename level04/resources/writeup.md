# level04

## Perl
The "level04.pl" file is a perl CGI script.  
1. The comment `# localhost:4747` gives a hint about the port server is running on. I tried to connect to the server via a browser: `http://192.168.56.102:4747` and it's receiving request and send out response.

2. `use CGI qw{param};` loads the CGI module into the script. (The qw{param} part is not necessary. The "param()" function will still work without explicitly include it here.)  
3. `sub` is acutlly just a function.  And the tricky part is the `print \`echo $y 2>&1\`;` line. It calls the system "echo" command whit the "y" argument.  
4. `param("x")` means we'll take the value of "x" from the params.  

## `param` and query string
It's a list of parameters that will be sent by client via "query string" within an url.  
ex:  
```
http://mysite.com?abc=jason&def=huang
```
`abc=jason&def=huang` after the "?" is the query string.  It will be read by the server as key/value pairs. So in perl script, `param("abc")` will give "jason" as value. and `param("dev")` will give "huang"  
Here we pass `param("x")` into the sub x. So it means we should pass the query string as `x=some_data`.  

## Command Substitution
Our goal now is to launch "getflag" with this perl script. If we just do `http://192.168.56.102:4747?x=getflag`. This will just print out "getflag" as a string. So we need do it with command substitution method on linux commands.  
Two solutions are available:
- strait command substitution: `x=\`getflag\`` or `$(getflag)` this will call the getflag command and return the result for echo to print out.   
- Encode ";" as an URI and make the getflag been launched instead being treated as an argument of "echo".  

## Send request
Send a simple GET request via curl or just type the url inside a browser. You will get the flag sent back.  

## Takeaway
- perl script
- query string
- command substitution
