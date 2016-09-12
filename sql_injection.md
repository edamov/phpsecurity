# SQL Injection

https://phpdelusions.net/pdo/sql_injection_example

https://paragonie.com/blog/2015/05/preventing-sql-injection-in-php-applications-easy-and-definitive-guide

SQL-инъекция - одна из наиболее известных атак. Эта атака представляет собой внедрение кода, в котором злоумышленники используют уязвимости сайта для отправки в базу данных специальных SQL запросов, которые могут вносить любые изменения либо в худшем случае удалить всю базу данных.

С ростом популярности PDO и ORM количество атак значительно уменьшилось. Но следует помнить, что использование PDO и так называемых `prepared statements` не всегда гарантирует полноценную защиту от инъекций.

### Пример



### Защита

* For better prevention of this security issue, the data must be validated, verified and cleaned up before it can enter the application;

* All the sensitive information such as passwords should be encrypted using SHA1 or SHA;

* Technical information can sometimes contain technical details that might reveal security vulnerabilities to an attacker; therefore, it must be removed from error messages;

* An attacker specifically looks to error messages to get information such as database names, usernames and table name, hence, you should disable error messages or you can create your own custom error messages;

* You can limit the permissions granted on the database and fewer permissions results lower chances of attack;

* You may use stored procedures and previously defined cursors to abstract data access so that users do not directly access tables or views;

* You can prevent words such as ‘insert’, ‘update’, ‘drop’, and ‘union’ from being added to the database (these all being words which can alter tables and databases).
* SQL Injection can not be prevented properly using htmlentities() or add_slashes(). Those methods are intended to ensure view context tasks. They are not intended to secure database interactions.
* https://phpdelusions.net/pdo/sql_injection_example

