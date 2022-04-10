# Домашнее задание к занятию "6.6. Troubleshooting"

## Задача 1
Пользователь (разработчик) написал в канал поддержки, что у него уже 3 минуты происходит CRUD операция в MongoDB и её нужно прервать.
Вы как инженер поддержки решили произвести данную операцию:

•	напишите список операций, которые вы будете производить для остановки запроса пользователя
```bash
docker run --name my-mongo -p 3000:3000 -d mongo
docker exec -it my-mongo bash
зайти в консоль  mongo
> show dbs
admin   0.000GB
config  0.000GB
local   0.000GB
Поиск запроса который выполняется более 3 минут > db.currentOp(
... {
... "active" : true,
... "secs_running" : { "$gt" : 180 },
... "ns" : /^test\./
... }
... )
{ "inprog" : [ ], "ok" : 1 }

Остановить зависший запрос db.killOp(параметр полученный в запросе выше inprog)
```
•	предложите вариант решения проблемы с долгими (зависающими) запросами в MongoDB
```bash
1. Попробовать метод maxTimeMS() для установки предела исполнения по времени операций 
2. Используя Database Profiler, отловить медленные операции и произвести оптимизацию.

```
## Задача 2
Вы запустили инстанс Redis для использования совместно с сервисом, который использует механизм TTL. Причем отношение количества записанных key-value значений к количеству истёкших значений есть величина постоянная и увеличивается пропорционально количеству реплик сервиса.

При масштабировании сервиса до N реплик вы увидели, что:
•	сначала рост отношения записанных значений к истекшим
•	Redis блокирует операции записи
```bash
Возможнo вся память занята истекшими ключами, но еще не удаленными. Redis заблокировался (ACTIVE_EXPIRE_CYCLE_LOOKUPS_PER_LOOP),
чтобы вывести из DB удаленные ключи и снизить их количество менее 25%. Т.к. Redis - однопоточное приложение, то все операции блокируются,
пока он не выполнит очистку. Имеет смысл поиграть со значением hz в redis.conf

```
## Задача 3
Вы подняли базу данных MySQL для использования в гис-системе. При росте количества записей, в таблицах базы, пользователи начали жаловаться на ошибки вида:
InterfaceError: (InterfaceError) 2013: Lost connection to MySQL server during query u'SELECT..... '

Как вы думаете, почему это начало происходить и как локализовать проблему?
```bash
https://dev.mysql.com/doc/refman/8.0/en/error-lost-connection.html возможны три причины:
1. Слишком объемные запросы, рекомендуется увеличение параметра net_read_timeout
2. Малое значение параметра connect_timeout, клиент не успевает установить соединение.
3. Размер сообщения/запроса превышает размер буфера max_allowed_packet на сервере или max_allowed_packet на строне клиента.
```

Какие пути решения данной проблемы вы можете предложить?
```bash
1. Увеличить на сервере MySQL wait_timeout, max_allowed_packet, net_write_timeout и net_read_timeout
2. Уменьшить pool_recycle, wait_timeout. 
```
## Задача 4
Вы решили перевести гис-систему из задачи 3 на PostgreSQL, так как прочитали в документации, что эта СУБД работает с большим объемом данных лучше, чем MySQL.
После запуска пользователи начали жаловаться, что СУБД время от времени становится недоступной. В dmesg вы видите, что:

postmaster invoked oom-killer

Как вы думаете, что происходит?
```bash
Postgres недостаточно памяти.      
```

Как бы вы решили данную проблему?
```bash
Произвести настройку параметров, затрагивающих память в Postgres:
max_connections
shared_buffer
work_mem
effective_cache_size
maintenance_work_mem
```
