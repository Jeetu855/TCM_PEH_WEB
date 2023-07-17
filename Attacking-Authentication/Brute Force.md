
wrodlist: /usr/share/seclists/xeto_top_1000

1)Burp Intruder

![[Pasted image 20230717230859.png]]

2)ffuf

save the post request that we are sending in a txt file and replace the password parameter with FUZZ

![[Pasted image 20230717231212.png]]

![[Pasted image 20230717231529.png]]

faster than burp intruder coz burp community has rate limits




![[Pasted image 20230717231730.png]]

```sh
ffuf -request authLab1.txt -request-proto http -w /usr/share/seclists/SecLists-master/Passwords/xato-net-10-million-passwords-10000.txt -fs 1814
```

![[Pasted image 20230717231748.png]]

