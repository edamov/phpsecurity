# Session fixation

The session and cookie hacking can’t breach the database or the web application itself, but it can compromise user accounts. A session is an entity triggered when users initiate contact with a web server and consists of a period of interaction between users and web application which may be authenticated using security measures like a username and password. During this session, the web application stores a cookie or file on the users’ browser which will contain information about the session like the users’ preferences, authentication data, unique codes or shopping cart information.

![](https://blogtmssl-templatemonster.netdna-ssl.com/blog/wp-content/uploads/2014/05/3.jpg)


### Защита

In order to prevent hackers from setting session ID’s prior to login, ID’s should be changed often, therefore, the session_regenerate_id() function should be used every time the user logs in, assigning them a fresh ID;
The risk of this hacking can be mitigated by revalidating a user who is about to perform important or sensitive tasks like resetting their password (i.e. by making them re-enter their old password);
If user’s password is to be stored in a session variable, it must be encrypted (using the sha1() function)
If your web application is handling sensitive information like debit and credit card numbers, then using an SSL or any other secured connection can also prevent session and cookie hacking

