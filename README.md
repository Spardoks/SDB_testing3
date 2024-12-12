# Домашнее задание к занятию "`SQL. Часть 1`" - `Виталий Коряко`

https://github.com/netology-code/sdb-homeworks/blob/main/12-03.md


### Задание 1

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a” и не содержат пробелов.

### Решение 1

```
SELECT DISTINCT district
FROM address
WHERE district LIKE 'K%a' AND district NOT LIKE '% %';
```

```
+-----------+
| district  |
+-----------+
| Kanagawa  |
| Kalmykia  |
| Kaduna    |
| Karnataka |
| K�tahya   |
| Kerala    |
| Kitaa     |
+-----------+
```

### Задание 2

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно** и стоимость которых превышает 10.00.

### Решение 2

```
SELECT *
FROM payment
WHERE CAST(payment_date AS date) BETWEEN '2005-06-15' AND '2005-06-18'
AND amount  > 10.00;
```
```
+------------+-------------+----------+-----------+--------+---------------------+---------------------+
| payment_id | customer_id | staff_id | rental_id | amount | payment_date        | last_update         |
+------------+-------------+----------+-----------+--------+---------------------+---------------------+
|        908 |          33 |        1 |      1301 |  10.99 | 2005-06-15 09:46:33 | 2006-02-15 22:12:36 |
|       7017 |         260 |        1 |      2091 |  10.99 | 2005-06-17 18:09:04 | 2006-02-15 22:14:58 |
|       8272 |         305 |        1 |      2166 |  11.99 | 2005-06-17 23:51:21 | 2006-02-15 22:15:47 |
|      12888 |         477 |        1 |      2306 |  10.99 | 2005-06-18 08:33:23 | 2006-02-15 22:19:46 |
|      13892 |         516 |        1 |      1718 |  10.99 | 2005-06-16 14:52:02 | 2006-02-15 22:20:47 |
|      14620 |         544 |        2 |      1434 |  10.99 | 2005-06-15 18:30:46 | 2006-02-15 22:21:35 |
|      15313 |         572 |        2 |      1889 |  10.99 | 2005-06-17 04:05:12 | 2006-02-15 22:22:22 |
+------------+-------------+----------+-----------+--------+---------------------+---------------------+
```

### Задание 3

Получите последние пять аренд фильмов.

### Решение 3

```
SELECT *
FROM rental
ORDER BY rental_date DESC
LIMIT 5;
```
```
+-----------+---------------------+--------------+-------------+-------------+----------+---------------------+
| rental_id | rental_date         | inventory_id | customer_id | return_date | staff_id | last_update         |
+-----------+---------------------+--------------+-------------+-------------+----------+---------------------+
|     11739 | 2006-02-14 15:16:03 |         4568 |         373 | NULL        |        2 | 2006-02-15 21:30:53 |
|     14616 | 2006-02-14 15:16:03 |         4537 |         532 | NULL        |        1 | 2006-02-15 21:30:53 |
|     11676 | 2006-02-14 15:16:03 |         4496 |         216 | NULL        |        2 | 2006-02-15 21:30:53 |
|     15966 | 2006-02-14 15:16:03 |         4472 |         374 | NULL        |        1 | 2006-02-15 21:30:53 |
|     13486 | 2006-02-14 15:16:03 |         4460 |         274 | NULL        |        1 | 2006-02-15 21:30:53 |
+-----------+---------------------+--------------+-------------+-------------+----------+---------------------+
```

### Задание 4

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'.

### Решение 4

```
SELECT 
    LOWER(REPLACE(first_name, 'll', 'pp')) AS adjusted_name,
    LOWER(last_name) AS adjusted_last_name
FROM 
    customer
WHERE 
    first_name IN ('Kelly', 'Willie')
    AND active = 1;
```

```
+---------------+--------------------+
| adjusted_name | adjusted_last_name |
+---------------+--------------------+
| kelly         | torres             |
| willie        | howell             |
| willie        | markham            |
| kelly         | knott              |
+---------------+--------------------+
```

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 5*

Выведите Email каждого покупателя, разделив значение Email на две отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй — значение, указанное после @.

### Задание 6*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные — строчными.