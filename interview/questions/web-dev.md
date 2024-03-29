# Веб-разработка

## Что такое CGI. Плюсы, минусы

Common Gateway Interface. Соглашение о том, как веб-сервер взаимодействует с программой, написанной на каком-то языке. Веб-сервер запускает программу как исполняемый файл. Параметры запроса, например, метод, путь, заголовки и т.д. передаются через переменные окружения.

Программа должна прочитать эти переменные и записать в стандартный поток вывода HTTP-ответ.

Плюсы:

- Протокол не накладывает условия на язык, на котором написана программа. Это     может быть и скрипт, и бинарный файл.
- Протокол экстремально прост.
- Программа не хранит состояние, что удобно для отладки.

Минусы:

- Запуск процесса ОС на каждый запрос отрабатывает очень медленно.
- Передача данных через `stdout` медленней юникс-сокетов.

## Как защитить куки от воровства и от подделки

Зависит от того, насколько строгие критерии безопасности на сайте. Если в куках хранятся вспомогательные данные, например, индекс последнего выбранного в дропдауне элемента, правилами ниже можно пренебречь.

Для платежных систем, сайтов с приватными данными приведенные правила обязательны.

- Выставлять кукам флаг `httponly`. Браузер не даст прочесть и изменить такие куки на клиенте Джаваскриптом.
- Использовать флаг `secure`. Куки будут переданы только по безопасному соединению.
- Устанавливать короткий срок жизни куки.
- Устанавливать короткий срок сессии на сервере.
- Добавлять в ключ сессии заголовок `User-Agent`. Тогда если украсть куки и установить на другой машине, ключ сессии будет другим.
- Аналогично пункту выше, но добавлять `IP` пользователя.
- Подписывать куки секретным ключом. Добавлять поле `sig`, которое равно `HMAC-SHA1(cookie-body, secret_key)`. На сервере проверять, что подпись совпадает.

## Какая разница между аутентификацией и авторизацией

**Идентификация** (от латинского identifico — отождествлять): присвоение субъектам и объектам идентификатора и / или сравнение идентификатора с перечнем присвоенных идентификаторов. Например, представление человека по имени отчеству - это идентификация.

**Аутентификация** (от греческого: αυθεντικός ; реальный или подлинный): проверка соответствия субъекта и того, за кого он пытается себя выдать, с помощью некой уникальной информации (отпечатки пальцев, цвет радужки, голос и тд.), в простейшем случае - с помощью имени входа и пароля.

**Авторизация** - это проверка и определение полномочий на выполнение некоторых действий (например, чтение файла /var/mail/eltsin) в соответствии с ранее выполненной аутентификацией.

Все три процедуры взаимосвязаны:

1. Сначала определяют имя (логин или номер) – идентификация
2. Затем проверяют пароль (ключ или отпечаток пальца) – аутентификация
3. И в конце предоставляют доступ – авторизация

## Что такое XSS. Примеры. Как защитить приложение

XSS – межсайтовые запросы. Страница, подверженная уязвимости, вынуждает пользователя выполнить запрос к другой странице, либо запустить нежелательный js-код.

Например, пользователь отправил комментарий, в котором был код:

```html
<script>alert('foo');</script>
```

Движок сайта не фильтрует текст комментария, поэтому тег `<script>` становится частью страницы и исполняется браузером. Каждый, кто зайдет на страницу с опасным комментарием, увидит всплывающее окно с тестом `foo`.

Другой пример. Страница поиска принимает поисковой терм `q`. В заголовке фраза “Результат поиска по запросу” + текст параметра. Если не экранировать параметр, то запрос `/search?q=<script>alert('foo');</script>` приведет к аналогичному результату.

Зная, что страница выполняет js-код, хакер может подгрузить на страницу контекстную рекламу, баннеры, заставить браузей перейти на любую страницу, похитить куки.

Уязвимость устраняется экранированием небезопасных символов, чисткой (санацией) HTML-тегов.

## REST & SOAP

### Что такое REST

- [REST Principles and Architectural Constraints](https://restfulapi.net/rest-architectural-constraints/)

REST (Representational state transfer «передача состояния представления») – соглашение о том, как выстраивать сервисы. Под REST часто имеют в виду т.н HTTP REST API. Как правило, это веб-приложение с набором урлов – конечных точек. Урлы принимают и возвращают данные в формате JSON. Тип операции задают методом HTTP-запроса, например:

- `GET` – получить объект или список объектов
- `POST` – создать объект
- `PUT` – обновить существующий объект
- `PATCH` – частично обновить существующий объект
- `DELETE` – удалить объект
- `HEAD` – получить метаданные объекта

REST-архитектура активно использует возможности протокола HTTP, чтобы избежать т.н. “велосипедов” – собственных решений. Например, параметры кеширования передаются стандартными заголовками `Cache`, `If-Modified-Since`, `ETag`. Авторизациция – заголовком `Authentication`.

REST это архитектурный стиль для проектирования слабо связанных HTTP приложений, что часто используется при разработке веб-сервисов. REST не диктует правил как это должно быть имплементировано на low уровне, он лишь дает высокоуровненые гайдлайны и оставляет тебе свободу для того чтобы воплотить собственную реализацию.

Для веб-служб, построенных с учётом REST (то есть не нарушающих накладываемых им ограничений), применяют термин «RESTful».

В отличие от веб-сервисов (веб-служб) на основе SOAP, не существует «официального» стандарта для RESTful веб-API. Дело в том, что REST является архитектурным стилем, в то время как SOAP является протоколом.

REST определяет 6 архитектурных ограничений, соблюдение которых позволит создать настоящий RESTful API:

1. Единообразие интерфейса
2. Клиент-сервер
3. Отсутствие состояния
4. Кэширование
5. Слои
6. Код по требованию (необязательное ограничение)

**Единообразие интерфейса**
Вы должны придумать API интерфейс для ресурсов системы, доступный для пользователей системы и следовать ему во что бы то ни стало. Ресурс в системе должен иметь только один логичный URI, который должен обеспечивать способ получения связанных или дополнительных данных. Всегда лучше ассоциировать (синонимизировать) ресурс с веб страницей.

Любой ресурс не должен быть слишком большим и содержать все и вся в своем представлении. Когда это уместно, ресурс должен содержать ссылки (HATEOAS: Hypermedia as the Engine of Application State), указывающие на относительные URI для получения связанной информации.

Кроме того, представления ресурсов в системе должны следовать определенным рекомендациям, таким как соглашения об именах, форматы ссылок или формат данных (xml или / и json).

>Как только разработчик ознакомится с одним из ваших API, он сможет следовать аналогичному подходу для других API.

**Клиент-сервер**
По сути, это означает, что клиентское приложение и серверное приложение ДОЛЖНЫ иметь возможность развиваться по отдельности без какой-либо зависимости друг от друга. Клиент должен знать только URI ресурса и больше ничего. Сегодня это нормальная практика в веб-разработке, поэтому с вашей стороны ничего особенного не требуется. Будь проще.

>Серверы и клиенты также могут заменяться и разрабатываться независимо, если интерфейс между ними не изменяется.

**Отсутствие состояния**
Рой Филдинг черпал вдохновение из HTTP, и это отражается в этом ограничении. Сделайте все клиент-серверное взаимодействие без состояний. Сервер не будет хранить информацию о последних  HTTP-запросах клиента. Он будет рассматривать каждый запрос как новый. Нет сессии, нет истории.

Если клиентское приложение должно быть приложением с отслеживанием состояния для конечного пользователя, когда пользователь входит в систему один раз и после этого выполняет другие авторизованные операции, то каждый запрос от клиента должен содержать всю информацию, необходимую для обслуживания запроса, включая сведения об аутентификации и авторизации.

>Клиентский контекст не должен храниться на сервере между запросами. Клиент отвечает за управление состоянием приложения.

**Кэширование**
В современном мире кэширование данных и ответов имеет первостепенное значение везде, где это применимо/возможно. Кэширование повышает производительность на стороне клиента и расширяет возможности масштабирования для сервера, поскольку нагрузка уменьшается.

В REST кэширование должно применяться к ресурсам, когда это применимо, и тогда эти ресурсы ДОЛЖНЫ быть объявлены кешируемыми. Кэширование может быть реализовано на стороне сервера или клиента.

>Хорошо настроенное кэширование частично или полностью исключает некоторые взаимодействия клиент-сервер, что еще больше повышает масштабируемость и производительность.

**Слои**
REST позволяет вам использовать многоуровневую архитектуру системы, в которой вы развертываете API-интерфейсы на сервере A, храните данные на сервере B, a запросы аутентифицируете, например, на сервере C. Клиент обычно не может сказать, подключен ли он напрямую к конечному серверу или к посреднику.

**Код по требованию (необязательное ограничение)**
Это опциональное ограничение. Большую часть времени вы будете отправлять статические представления ресурсов в форме XML или JSON. Но когда вам нужно, вы можете вернуть исполняемый код для поддержки части вашего приложения, например, клиенты могут вызывать ваш API для получения кода визуализации виджета интерфейса пользователя. Это разрешено

Все вышеперечисленные ограничения помогают вам создать действительно RESTful API, и вы должны следовать им. Тем не менее, иногда вы можете столкнуться с нарушением одного или двух ограничений. Не беспокойтесь, вы все еще создаете API RESTful, но не «труЪ RESTful».

### Что такое SOAP

SOAP (от англ. Simple Object Access Protocol - простой протокол доступа к объектам; вплоть до спецификации 1.2) - протокол обмена структурированными сообщениями в распределённой вычислительной среде. Первоначально SOAP предназначался в основном для реализации удалённого вызова процедур (RPC). Сейчас протокол используется для обмена произвольными сообщениями в формате XML, а не только для вызова процедур. Официальная спецификация последней версии 1.2 протокола никак не расшифровывает название SOAP. SOAP является расширением протокола XML-RPC.
SOAP может использоваться с любым протоколом прикладного уровня: SMTP, FTP, HTTP, HTTPS и др. Однако его взаимодействие с каждым из этих протоколов имеет свои особенности, которые должны быть определены отдельно. Чаще всего SOAP используется поверх HTTP.

### В чем разница между REST и SOAP веб сервисами

Некоторые отличия:

- REST поддерживает различные форматы: text, JSON, XML; SOAP - только XML,
- REST работает только по HTTP(S), а SOAP может работать с различными протоколами,
- REST может работать с ресурсами. Каждый URL это представление какого-либо ресурса. SOAP работает с операциями, которые реализуют какую-либо бизнес логику с помощью нескольких интерфейсов,
- SOAP на основе чтения не может быть помещена в кэш, а REST в этом случае может быть закэширован,
- SOAP поддерживает SSL и WS-security, в то время как REST - только SSL, SOAP поддерживает ACID (Atomicity, Consistency, Isolation, Durability). REST поддерживает транзакции, но не один из ACID не совместим с двух фазовым коммитом.

### Можем ли мы посылать SOAP сообщения с вложением

Да, это возможно. Можно посылать вложением различные форматы: PDF, изображения или другие двоичные данные. Сообщения SOAP работают вместе с расширением MIME, в котором предусмотрено multipart/related

### Как бы вы решили какой из REST или SOAP веб сервисов использовать

REST против SOAP можно перефразировать как "Простота против Стандарта". В случае REST (простота) у вас будет скорость, расширяемость и поддержка многих форматов. В случае с SOAP у вас будет больше возможностей по безопасности (WS-security) и транзакционная безопасность (ACID).

## Какие способы для мониторинга веб-приложений в production вы использовали или знаете

- [51 инструмент для APM и мониторинга серверов](https://habr.com/ru/company/pc-administrator/blog/304356/)