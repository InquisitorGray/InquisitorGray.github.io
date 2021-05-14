---
layout: default
title: DTM : ALTER VIEW
nav_order: 1
parent: Запросы SQL\+
grand_parent: 5. Справочная информация
has_children: false
---

Руководство пользователя
[5. Справочная информация](5_Справочная_информация.md)
[Запросы SQL+](./5_Справочная_информация/Запросы_SQLplus.md)

DTM : ALTER VIEW
================

Запрос позволяет изменить вид [логического представления](361070885.html) в [логической базе данных](354945300.html).

В ответе возвращается:

*   пустой объект ResultSet при успешном выполнении запроса;
    
*   исключение при неуспешном выполнении запроса.
    

**Примечание:** логическое представление можно также изменить с помощью запроса `CREATE OR REPLACE VIEW` (см. [CREATE VIEW](CREATE-VIEW_544965567.html)).

#### Синтаксис

ALTER VIEW \[db\_name.\]view\_name AS SELECT query

#### Параметры

*   `db_name` — имя логической базы данных, в которой находится логическое представление. Указывается опционально, если выбрана логическая БД, [используемая по умолчанию](401279070.html);
    
*   `view_name` — имя изменяемого логического представления;
    
*   `query` — [SELECT](SELECT_509509945.html)\-подзапрос, на основе которого строится новый вид логического представления.
    

#### Ограничения

В подзапросе `query` не допускается использование:

*   логических представлений,
    
*   [системных представлений](544899575.html) INFORMATION\_SCHEMA,
    
*   директивы [FOR SYSTEM\_TIME](https://arenadata.atlassian.net/wiki/spaces/DTM/pages/509509945/SELECT#select_for_system_time),
    
*   секции `DATASOURCE_TYPE`.
    

#### Пример
```SQL
ALTER VIEW sales.stores\_by\_sold\_products AS
  SELECT store\_id, SUM(product\_units) AS product\_amount
  FROM sales.sales
  GROUP BY store\_id
  ORDER BY product\_amount ASC
LIMIT 20
```
