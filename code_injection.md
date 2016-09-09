# Code Injection (Remote file inclusion, Local file inclusion)

В PHP есть четыре функции, через которые можно заинклудить файл: `require`, `require_once`, `include` и `include_once`.


### Remote File Inclusion and Remote Code 

This security breach allows a malicious or unknown party to run code on your web server or client side and it can lead to several further types of hacking. Remote file inclusion is caused by a site vulnerability which allows hackers to deploy a malicious file onto the web server. This can be caused by improper use of require() and include() functions when the register_globals directive, a setting which controls the availability of superglobal variables, is ON (allowing the user to initialize variables remotely). If this directive is ON, an uninitialized variable can be used to include malicious or unwanted files from remote locations, and if the allow_url_fopen is enabled in php.ini, then remote files can be uploaded to the site’s server via FTP or HTTP from a remote location.


### Защита


You should make OFF The register_globals directive, in later versions of PHP, it is OFF by default, but one should always check that. If the directive has to be set to ON for some reason, all variables must be properly initialized.
There are other PHP directives can be used to prevent this security breach, which include:
allow_url_fopen (set to on by default) that controls whether remote files should be includable and should be turned to OFF
allow_url_include (set to off by default) that controls whether include_once(), include(), require() and require_once() commands are able to include remote files into the code
Enabling safe_mode which forces PHP to test of user ID permissions before opening any file
Always validate user input and be very careful with any data retrieved from remote servers or locations. In order to stop it, you can ensure that all include files are locally hosted and never accept files from anywhere else unless absolutely necessary
Restrict user privileges to an absolute minimum can also help in prevention from this security threat