# level05

## "You have new mail" 
Upon logged in as user "level05". We got a message: "You hav new mail".  
There is a "mail" sent by the system. Stored inside "/var/mail" folder.  

## The mail
We found this "level05" mail with some weard content:  
`*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05`  
`su -c "sh /usr/sbin/openarenaserver" - flag05` seems understandable. But what is `*/2 * * * *`?

## Cron job
Here is the first result from our best friend: [crontab guru - every 2 minutes](https://crontab.guru/every-2-minutes).  
Does this means that the system is running the command every 2 minutes?  

## The Shell script "/usr/sbin/openarenaserver"
"/usr/sbin/openarenaserver" is a shell script:
```
#!/bin/sh

for i in /opt/openarenaserver/* ; do
  (ulimit -t 5; bash -x "$i")
  rm -f "$i"
done
```
Looks like it runs a loop through all the files inside "/opt/openarenaserver" folder. Execute them. And then delete them.  
(`man ulimit` didn't gave much information. Need to refer to other man page found online: [ulimit](https://ss64.com/bash/ulimit.html). But ulimit is probably not very important here.)  

## Another script injection
Just try to write a script and let it automaticlly been called:
`echo "getflag > /tmp/theflag" > /opt/openarenaserver/gflag`  
Check the "/tmp/theflag" file after 2 minutes.
The flag is inside!

## Takeaway
- System mail
- Cron job
