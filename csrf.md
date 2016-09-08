# CSRF

CSRF (Cross-Site Request Forgery, также XSRF) - атака, которая приводит к тому, что злоумышленник может выплнять на сторонних сайтах действия от имени других зарегистрированных и залогиненных пользователей. 

Единственная уважительная причина не использовать защиту от данного вида атак — сайт не хранит никакие пользовательские данные, а вы не используете панель администратора для редактирования материалов.

### Пример:
Один из типичных сценариев CSRF атаки:

* Гиви авторизируется на уязвимом сайте (bank.com) и в браузере сохраняются куки.
* Гиви попадает на страницу злоумышленника (через приглашение в емейле или каким-то другим способом), на которой находится html форма:

```html
<form action="http://bank.com/send-money" method="POST">
  <input type="hidden" name="amount" value="1000">
  <input type="hidden" name="for" value="John">
  ...
  <input type="submit" name="submit" value="Click and win a prize!">
</form>
```

* Гиви по незнанию сабмитит форму (либо форма сабимитится автоматически из JS), cайт bank.com проверяет куки, видит, что посетитель авторизован и обрабатывает форму, profit!


### Защита:
https://habrahabr.ru/post/235247/


Use re-authentication for critical operations (change password, recovery email, etc.)
If you're not sure whether your operation is CSRF proof, consider adding CAPTCHAs (however CAPTCHAs are inconvenience for users)
If you're performing operations based on other parts of a request (neither GET nor POST) e.g Cookies or HTTP Headers, you might need to add CSRF tokens there as well.
AJAX powered forms need to re-create their CSRF tokens. Use the function provided above (in code snippet) for that and never rely on Javascript.
CSRF on GET or Cookies will lead to inconvenience, consider your design and architecture for best practices.

How To Protect Against It
The first step is to ensure no data-altering actions are per-
formed by GET requests. Anything that performs an action
on data should require a POST, PUT, or DELETE request. If
the user clicks a delete button, they should then be taken to a
form used to confirm the action. If data-altering actions need
to be performed over GET (maybe for a RESTful API), you can
require a unique token in the query string. In the following
examples we will be using POST data but the exact same
concepts apply when dealing with GET requests; just set the
token in the query string instead of in the POST parameters.