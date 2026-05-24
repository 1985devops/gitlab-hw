# Домашнее задание к занятию «SQL. Часть 2» -  Нугаев Алексей


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
---

### Задание 1.

1. `Одним запросом получил информацию о магазине, в котором обслуживается более 300 покупателей, и вывел в результат следующую информацию:` 

* фамилия и имя сотрудника из этого магазина;
* город нахождения магазина;
* количество пользователей, закреплённых в этом магазине.

```
SELECT 
    CONCAT(st.first_name, ' ', st.last_name) AS manager_name,
    c.city,
    COUNT(cu.customer_id) AS customer_count
FROM store s
JOIN staff st ON s.manager_staff_id = st.staff_id
JOIN address a ON s.address_id = a.address_id
JOIN city c ON a.city_id = c.city_id
JOIN customer cu ON s.store_id = cu.store_id
GROUP BY s.store_id, st.first_name, st.last_name, c.city
HAVING COUNT(cu.customer_id) > 300;

```

`При необходимости прикрепитe сюда скриншоты`
![установка 1](https://github.com/1985devops/gitlab-hw/blob/main/nnn1.png)


### Задание 2.

1. `Получил количество фильмов, продолжительность которых больше средней продолжительности всех фильмов.`


```
SELECT COUNT(*) AS long_films_count
FROM film
WHERE length > (SELECT AVG(length) FROM film);

```

`При необходимости прикрепитe сюда скриншоты`
![установка 2](https://github.com/1985devops/gitlab-hw/blob/main/nnn2.png)


### Задание 3.

1. `Получил информацию, за какой месяц была получена наибольшая сумма платежей, и добавил информацию по количеству аренд за этот месяц.` 

```
SELECT 
    DATE_FORMAT(payment_date, '%Y-%m') AS payment_month,
    SUM(amount) AS total_amount,
    COUNT(rental_id) AS rental_count
FROM payment
GROUP BY payment_month
ORDER BY total_amount DESC
LIMIT 1;

```

`При необходимости прикрепитe сюда скриншоты`
![установка 3](https://github.com/1985devops/gitlab-hw/blob/main/nnn3.png)
