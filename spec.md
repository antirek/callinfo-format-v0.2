

JSON

level-0 - условный уровень, совместимый с CDR 

level-1 - условный уровень, расширяющий level-0, дополнительные данные в data


## level-0

поля: явные, скрытые

скрытые поля необходимы для работы внутри приложений, не предназначены для экспорта во внешние пользовательские системы, возможна реализация фильтра контроля для проверки и очистки этих полей при экспорте

* version, обязательное, определяет версию данного формата

* server, необязательное, требуется в мульти серверных системах, скрытое

* account, необязательное, требуется в мульти аккаунтовых системах, скрытое

* time	- unixtimestamp звонка, обязательное

* timezone - таймзона, необязательное

* uuid - uuid звонка, обязательное, уникальное для сервиса в целом

* direction, необязательное, набор вариантов определяется архитектором системы, например: входящие, исходящие, внутренние, транзитные

* from - номер А

* fromChannel - идентификация входного канала, необязательное, скрытое

* to - номер Б

* toChannel - идентификация исходящего канала, необязательное, скрытое

* duration - длительность звонка, от поступления в систему до завершения

* billsec - длительность звонка в ответном состоянии, может использоваться как расчетное для длительности вызова

* record - бинарный флаг наличия записи разговора 

* recordUrl - при флаге наличия записи указывается url, необязательное

* answered - бинарный флаг успешного вызова, необязательно, успешность определяется архитектором системы, например, может быть успешным в результате ответа оператора (не путать с ответным состоянием канала)

* cause - причина завершения вызова, необязательно, определяется по состоянию каналов

* data - данные для level-1




## level-1

* badges - беджи, архитектором системы могут быть определены разные дополнительные флаги для различных характеристик вызова, например, api - для вызовов, соверешенных посредством api, transfered - для переведенных вызовов, declined_by_limit - для отклоненных по лимиту линий, advertise - вызовы, пришедшие на рекламные номера коллтрекинга, pickuped - для перехваченных вызовов и т.д., данное поле предназначено только для формирования списка беджей, чтобы а) можно было визульно промаркировать в журнале звонков, б) произвести быстрый подсчет звонков с разными характеристиками

* badgesData - список данных, расширяющих данные беджей



* caller - секция данных для звонящего номера from

** operator - оператор связи для номера А

** region - регион происхождения номера А

** name - имя, определенное по интегрированным системам CRM, белых списков и т.д.

** 


* callee - секция данных для набранного номера to 

** operator

** region

** name

* recordFile - при флаге наличия записи указывается относительный системный путь хранения файла записи, скрытое


* route - маршрут прохождения вызова

содержит список объектов, через которые прошла маршрутизация вызова при его обслуживании, например, для входящих вызовов это используемый черный список, проверка временного интервала, используемая очередь, для исходящих список проверенных вариантов исходящих шаблонов для выбора транка, с временными метками

* dialstatus - статус канала



* subs - данные по сабканалам прохождения вызова, смотри секцию subs

содержит список наборов данных для каждого сабканала, который был задействован для обслуживания вызова

** содержит route, аналогично level-1

** содержит recordFile, скрытое, аналогично level-1

** dialstatus - статус канала, аналогично level-1

