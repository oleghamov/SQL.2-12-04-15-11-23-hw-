# Домашнее задание к занятию "SQL. Часть 2" - `Хамов Олег`

### Задание 1

    select concat(sf.first_name , ' ', sf.last_name) as 'LFMname Employee',

	 cy.city,

	 COUNT(cr.customer_id) as 'Count Buyers'
		
    from sakila.store s

    join sakila.staff sf on sf.store_id = s.store_id

    join sakila.customercr on cr.store_id = s.store_id

    join sakila.address a on a.address_id = s.address_id

    join sakila.city cy on cy.city_id = a.city_id

    group by sf.staff_id, cy.city_id

    having COUNT(cr.customer_id) > 300;

### Задание 2

    select COUNT(f.title)

    from sakila.film f
 
    where f.`length` > (select AVG(`length`)
 
        from sakila.film);

### Задание 3

    select t.amount_of_payments,

	 t.month_of_payments,

	 (select count(r.rental_id)

	 from sakila.rental r

	 where DATE_FORMAT(r.rental_date, '%M %Y') = t.month_of_payments) 'count_of_rent'

    from (

       select SUM(p.amount) 'amount_of_payments', DATE_FORMAT(p.payment_date, '%M %Y') 'month_of_payments'
 
       from sakila.payment p
 
       group by DATE_FORMAT(p.payment_date, '%M %Y')) t

    order by t.amount_of_payments desc

    limit 1;
