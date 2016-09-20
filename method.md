# Методика

В этом разделе приведены ключевые пункты, на которые следует обратить внимание в разрезе безопасности приложения. Соблюдая ниже приведенные правила вы значительно обезопасите себя и свое приложение от сторонних посягательств.

http://www.phptherightway.com/#security

Главное правило - никогда нельзя доверять входящим данным.
Всегда фильтруйте получаемые данные (формы, файлы, HTTP заголовки...) и экранируйте ответ.
Предпочитайте белые списки - входящие данные не валидны, пока не доказано обратное. Это основа основ.

##### AUTHENTICATION SYSTEMS (Signup/Signin/Password reset) 
- Используйте HTTPS.
- Для хеширования паролей используйте `bcrypt` (нет необходимости отдельно генерировать соль - `bcrypt` сделает это за вас).
- Удаляйте идентификатор сессии после логаута.
- Удаляйте все активные сессии при сбросе пароля.
- Используйте `session_regenerate_id()` после успешного логина.
- Избегайте открытых редиректов после успешного логина(????).
- При использовании протокола OAuth2 обязательно наличие `state` параметра.
- Обрабатывайте входящие данные во время Signup/Login на случай наличия конструкций `javascript://`, `data://`, CRLF символов. 
- Используйте безопасные httpOnly куки.
- Ограничивайте количество неудачных попыток при логине пользователей. Используйте капчу или метод `повторите вашу попытку через N минут`.
- Генерирутей для каждого восставновления пароля свой уникальный токен.
- Срок действия токена для восстановления пароля устанавливайте на адекватный период (до 10 минут будет достаточно).
- Экспайрите токен для восстановления пароля после его использования.


##### USER DATA & AUTHORIZATION
- Any resource access like, `my cart`, `my history` should check the logged in user's ownership of the resource using session id.
- В качестве идентификаторов пользователей и других сущностей используйте `UUID` вместо автоинкрементных чисел.
- Фича `Edit email/phone number` всегда должна верифицироваться владельцем аккаунта. 
- Any upload feature should sanitize the filename provided by the user. Also, for generally reasons apart from security, upload to something like S3 (and post-process using lambda) and not your own server capable of executing code.  
- При реализации функционала `Profile photo upload` нужно фильтровать все `EXIF` теги кроме случаев, когда они необходимы.
- Используйте JWT-токены, если вы разрабатываете API.

##### SECURITY HEADERS & CONFIGURATIONS
- `Add` [CSP](https://en.wikipedia.org/wiki/Content_Security_Policy) header to mitigate XSS and data injection attacks. This is important.
- `Add` [CSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery) header to prevent cross site request forgery. Also add [SameSite](https://tools.ietf.org/html/draft-ietf-httpbis-cookie-same-site-00) attributes on cookies.
- `Add` [HSTS](https://en.wikipedia.org/wiki/HTTP_Strict_Transport_Security) header to prevent SSL stripping attack.
- `Add` your domain to the [HSTS Preload List](https://hstspreload.appspot.com/)
- `Add` [X-Frame-Options](https://en.wikipedia.org/wiki/Clickjacking#X-Frame-Options) to protect against Clickjacking.
- `Add` [X-XSS-Protection](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project#X-XSS-Protection) header to mitigate XSS attacks.
- Update DNS records to add [SPF](https://en.wikipedia.org/wiki/Sender_Policy_Framework) record to mitigate spam and phishing attacks.
- Add [subresource integrity checks](https://en.wikipedia.org/wiki/Subresource_Integrity) if loading your JavaScript libraries from a third party CDN. For extra security, add the [require-sri-for](https://w3c.github.io/webappsec-subresource-integrity/#parse-require-sri-for) CSP-directive so you don't load resources that don't have an SRI sat.  
- Use random CSRF tokens and expose business logic APIs as HTTP POST requests. Do not expose CSRF tokens over HTTP for example in an initial request upgrade phase.
- Do not use critical data or tokens in GET request parameters. Exposure of server logs or a machine/stack processing them would expose user data in turn.  
- Не используйте метод GET для изменения состояния приложения.
  
  
##### SANITIZATION OF INPUT
- `Sanitize` all user inputs or any input parameters exposed to user to prevent [XSS](https://en.wikipedia.org/wiki/Cross-site_scripting).
- Always use parameterized queries to prevent [SQL Injection](https://en.wikipedia.org/wiki/SQL_injection).  
- Sanitize user input if using it directly for functionalities like CSV import.
- `Sanitize` user input for special cases like robots.txt as profile names in case you are using a url pattern like coolcorp.io/username. 
- Do not hand code or build JSON by string concatenation ever, no matter how small the object is. Use your language defined libraries or framework.
- [ ] Sanitize inputs that take some sort of URLs to prevent [SSRF](https://docs.google.com/document/d/1v1TkWZtrhzRLy0bYXBcdLUedXGb9njTNIJXa3u9akHM/edit#heading=h.t4tsk5ixehdd).
- [ ] Sanitize Outputs before displaying to users.

##### OPERATIONS
- Проверяйте, что у вас на сервере нет "случайно" открытых портов наружу.
- Проверяйте вашу БД на "не дефолтные" пароли, особенно в MongoDB & Redis.
- Используйте SSH для доступа на сервер; забудьте про доступ к SSH по паролю, используйте аутентификацию по SSH-ключам.
- [ ] Modify server config to use TLS 1.2 for HTTPS and disable all other schemes. (The tradeoff is good.)
- Не оставляйте DEBUG-режим включенным. В некоторых фреймворках включенный DEBUG-режим может привести к утечке критически важной для безопасности вашего приложения информации.
- Будьте готовы к DDOS-атакам, используйте хостинг, который помогает обезопасить или смягчить атаки подобного рода.
- Установите систему мониторинга за вашим приложением, логируйте **(что логировать?????)**.

##### PEOPLE
- Set up an email (e.g. security@coolcorp.io) and a page for security researchers to report vulnerabilities.
- Depending on what you are making, limit access to your user databases.
- Be polite to bug reporters.
- Have your code review done by a fellow developer from a secure coding perspective. (More eyes)
-  In case of a hack or data breach, check previous logs for data access, ask people to change passwords. You might require an audit by external agencies depending on where you are incorporated.  


И последнее, всегда используйте [актуальные версии PHP](https://secure.php.net/supported-versions.php) и библиотек в вашем приложении. Рекомендуется регулярно обновлять PHP и быть в курсе изменений, сделанных в последних версиях.

Наличие известных уязвимостей можно проверить используя следующие инструменты:
  - [Security Advisories Checker](https://security.sensiolabs.org) - проверяет composer зависимости на наличие известных уязвимостей;
  - [PHP Security Advisories Database](https://github.com/FriendsOfPHP/security-advisories) - база данных известных уязвимостей в различных PHP проектах и библиотеках;
  - [Scanner for php.ini](https://github.com/psecio/iniscan) - утилита для проверки php.ini файла на наличие небезопасных конфигов.