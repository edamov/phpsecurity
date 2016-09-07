# Security misconfiguration

In my experience, web servers and applications that have been misconfigured are way more common than those that have been configured properly. Perhaps this because there is no shortage of ways to screw up. Some examples:

Running the application with debug enabled in production.
Having directory listing enabled on the server, which leaks valuable information.
Running outdated software (think WordPress plugins, old PhpMyAdmin).
Having unnecessary services running on the machine.
Not changing default keys and passwords. (Happens way more frequently than you’d believe!)
Revealing error handling information to the attackers, such as stack traces.
Prevention: Have a good (preferably automated) “build and deploy” process, which can run tests on deploy. The poor man’s security misconfiguration solution is post-commit hooks, to prevent the code from going out with default passwords and/or development stuff built in.