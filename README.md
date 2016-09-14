# PHP Security

Разработчики очень часто не уделяют достаточно времени вопросу безопасности веб-приложений. Особенно этим грешат начинающие. 
Конечно, на сто процентов гарантировать безопасность веб-приложения нельзя, но можно максимально усложнить жизнь потенциальному злоумышленнику. 
Это руководство предназначено для ознакомления читателя с видами уязвимостей, способами их предотвращения и методикой проверки безопасности веб-приложения.

> ... следует помнить, что вы не можете проверить все возможные варианты даже для простейшей страницы. Данные, которые вы ожидаете, могут совершенно не соответствовать тому, что введет раздраженный служащий, хакер со стажем или домашний кот, разгуливающий по клавиатуре. Поэтому лучше логически подумать над вопросом: в каком месте могут быть введены неожиданные данные, как их можно модифицировать, усечь, либо, наоборот, дополнить. // [php.net](http://php.net)