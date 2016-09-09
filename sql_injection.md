# SQL Injection

https://phpdelusions.net/pdo/sql_injection_example

SQL injection is one of the most common types of hacking and it is specifically targeted at database-driven websites or web applications which link to and interact with databases. This attack is a type of code injection, where attackers exploit vulnerabilities in the site’s security measures to send special SQL queries to the database that can modify it and tables within it or in the worst case delete the whole database.

This attack occurs when the web-developers have failed to build in any checking or data validation functionality for the areas of the website where data from external sources can be inserted into the website. An attacker will add his own SQL statements in unprotected SQL queries that utilize data submitted by the user to look-up something in the database.


### Пример



### Защита

* For better prevention of this security issue, the data must be validated, verified and cleaned up before it can enter the application;

* All the sensitive information such as passwords should be encrypted using SHA1 or SHA;

* Technical information can sometimes contain technical details that might reveal security vulnerabilities to an attacker; therefore, it must be removed from error messages;

* An attacker specifically looks to error messages to get information such as database names, usernames and table name, hence, you should disable error messages or you can create your own custom error messages;

* You can limit the permissions granted on the database and fewer permissions results lower chances of attack;

* You may use stored procedures and previously defined cursors to abstract data access so that users do not directly access tables or views;

* You can prevent words such as ‘insert’, ‘update’, ‘drop’, and ‘union’ from being added to the database (these all being words which can alter tables and databases).

