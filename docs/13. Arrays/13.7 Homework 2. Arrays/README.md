# Домашняя работа 2. Массивы

Написать функцию, которая фильтрует телефонные номера по коду оператора.

Принимает 3-х значный код мобильного оператора и список телефонных номеров в формате +1(234)5678901 (variadic)

Функция возвращает только те номера, код оператора которых соответствует значению соответствующего аргумента.

Проверить функцию передав следующие аргументы:

`903`, `+7(903)1901235`, `+7(926)8567589`, `+7(903)1532476`

Попробовать передать аргументы с созданием массива и без.

Подсказка: чтобы передать массив в VARIADIC-аргумент, надо перед массивом прописать, собственно, ключевое слово variadic.

## Решение 
```sql
CREATE OR REPLACE FUNCTION get_phone_operator_from_list(phone_code char(3), VARIADIC phones char(14)[]) RETURNS SETOF char(14) AS $$
SELECT phone
FROM UNNEST(phones) AS phone
WHERE phone LIKE CONCAT('%(', phone_code, ')%');
$$ LANGUAGE sql;

SELECT get_phone_operator_from_list('903', VARIADIC ARRAY['+7(903)1901235', '+7(926)8567589', '+7(903)1532476']);
```