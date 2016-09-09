# Path Traversal (or Directory Traversal)

Directory traversal is a method of exploiting web applications by accessing files beyond the document root directory that allows attackers to view restricted files and interact with the web server by executing commands. This attack occurs through a browser and is accomplished by the hacker entering a URL into the address bar which takes him out of the root directory and into the main server directories; this generally takes some guesswork on the part of the hacker, but can actually be done quite easily. The attack can also be done through input portals on the front end of the web application.


### Защита

You should validate and sanitize all user input correctly by removing all suspect data and filtering out meta-characters;
Another precaution from this hacking is to never store sensitive configuration files inside the web root;
If a suspect request to a file is made, the full file-path should be built up and all the characters in the path should be normalized (e.g. change %20 to spaces);
Careful programming on the web-server is important and you should make use of security software, patches and vulnerability scanners.

