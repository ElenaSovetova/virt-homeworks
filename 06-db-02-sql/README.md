# Домашнее задание к занятию "6.2. SQL"

## Введение

Перед выполнением задания вы можете ознакомиться с 
[дополнительными материалами](https://github.com/netology-code/virt-homeworks/tree/master/additional/README.md).

## Задача 1

Используя docker поднимите инстанс PostgreSQL (версию 12) c 2 volume, 
в который будут складываться данные БД и бэкапы.

Приведите получившуюся команду или docker-compose манифест.
---

docker pull postgres:12

docker volume create vol1

docker volume create vol2

sudo docker run --rm --name vagrant-netology -e POSTGRES_PASSWORD=vagrant -e POSTGRES_USER=vagrant -e POSTGRES_DB=vagrant -d -ti -p 2222:2222 -v vol1:/var/lib/postgresql/data -v vol2:/var/lib/postgresql postgres:12

root@7c2aa13a3dcc:/#  psql -U postgres

![img_1.png](img_1.png)
## Задача 2

В БД из задачи 1: 
- создайте пользователя test-admin-user и БД test_db
Создаем БД test_db:
![img_2.png](img_2.png)
пользователя test-admin-user:
![img_3.png](img_3.png)
![img_4.png](img_4.png)
- в БД test_db создайте таблицу orders и clients (спeцификация таблиц ниже)
![img_5.png](img_5.png)
![img_6.png](img_6.png)
- предоставьте привилегии на все операции пользователю test-admin-user на таблицы БД test_db
![img_7.png](img_7.png)
- создайте пользователя test-simple-user 
![img_8.png](img_8.png)
- предоставьте пользователю test-simple-user права на SELECT/INSERT/UPDATE/DELETE данных таблиц БД test_db
![img_9.png](img_9.png)
Таблица orders:
- id (serial primary key)
- наименование (string)
- цена (integer)

Таблица clients:
- id (serial primary key)
- фамилия (string)
- страна проживания (string, index)
- заказ (foreign key orders)

Приведите:
- итоговый список БД после выполнения пунктов выше,
![img_10.png](img_10.png)
- описание таблиц (describe)
![img_11.png](img_11.png)
![img_15.png](img_15.png)
![img_16.png](img_16.png)
- SQL-запрос для выдачи списка пользователей с правами над таблицами test_db
![img_12.png](img_12.png)
- список пользователей с правами над таблицами test_db
![img_13.png](img_13.png)

## Задача 3

Используя SQL синтаксис - наполните таблицы следующими тестовыми данными:

Таблица orders

|Наименование|цена|
|------------|----|
|Шоколад| 10 |
|Принтер| 3000 |
|Книга| 500 |
|Монитор| 7000|
|Гитара| 4000|
![img_17.png](img_17.png)
Таблица clients

|ФИО|Страна проживания|
|------------|----|
|Иванов Иван Иванович| USA |
|Петров Петр Петрович| Canada |
|Иоганн Себастьян Бах| Japan |
|Ронни Джеймс Дио| Russia|
|Ritchie Blackmore| Russia|
![img_18.png](img_18.png)
Используя SQL синтаксис:
- вычислите количество записей для каждой таблицы 
- приведите в ответе:
    - запросы 
    - результаты их выполнения.
![img_19.png](img_19.png)
    - 
## Задача 4

Часть пользователей из таблицы clients решили оформить заказы из таблицы orders.

Используя foreign keys свяжите записи из таблиц, согласно таблице:

|ФИО|Заказ|
|------------|----|
|Иванов Иван Иванович| Книга |
|Петров Петр Петрович| Монитор |
|Иоганн Себастьян Бах| Гитара |

Приведите SQL-запросы для выполнения данных операций.
![img_20.png](img_20.png)
Приведите SQL-запрос для выдачи всех пользователей, которые совершили заказ, а также вывод данного запроса.
 ![img_21.png](img_21.png)
Подсказк - используйте директиву `UPDATE`.

## Задача 5

Получите полную информацию по выполнению запроса выдачи всех пользователей из задачи 4 
(используя директиву EXPLAIN).

Приведите получившийся результат и объясните что значат полученные значения.

![img_23.png](img_23.png)

cost - затратность операции

0.00 — затраты на получение первой строки.

18.10 — затраты на получение всех строк.

rows — приблизительное количество возвращаемых строк при выполнении операции Seq Scan. 

width — средний размер одной строки в байтах.
## Задача 6

Создайте бэкап БД test_db и поместите его в volume, предназначенный для бэкапов (см. Задачу 1).

vagrant@vagrant:~$ sudo docker exec -i vagrant-netology pg_dump -U vagrant test_db -f /var/lib/postgresql/data/dump_test.sql

![img_24.png](img_24.png)
Остановите контейнер с PostgreSQL (но не удаляйте volumes).
![img_25.png](img_25.png)

Поднимите новый пустой контейнер с PostgreSQL.

 sudo docker run --rm --name vagrant-netology2 -e POSTGRES_PASSWORD=vagrant -e POSTGRES_USER=vagrant -e POSTGRES_DB=vagrant -d -ti -p 5432:5432 -v vol1:/var/lib/postgresql/data -v vol2:/var/lib/postgresql postgres:12
![img_26.png](img_26.png)


Восстановите БД test_db в новом контейнере.
При создании нового окнтейнера волюмы подключились атвоматически


Приведите список операций, который вы применяли для бэкапа данных и восстановления. 

---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
