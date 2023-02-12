# Question - 10
 
</details>
<br>
<details>
  <summary>Click here to check the question !</summary>
<br>
how many new and repaeted customers are coming day to day
</details>
<br>

</details>
<br>
<details>
  <summary>Here is the script !</summary>
<br>
  
``
create table customer_orders (
order_id integer,
customer_id integer,
order_date date,
order_amount integer
);
select * from customer_orders
insert into customer_orders values(1,100,cast('2022-01-01' as date),2000),(2,200,cast('2022-01-01' as date),2500),(3,300,cast('2022-01-01' as date),2100)
,(4,100,cast('2022-01-02' as date),2000),(5,400,cast('2022-01-02' as date),2200),(6,500,cast('2022-01-02' as date),2700)
,(7,100,cast('2022-01-03' as date),3000),(8,400,cast('2022-01-03' as date),1000),(9,600,cast('2022-01-03' as date),3000)
;
;``
  
  </details>
<br>

``
# Input should be like this
``
![image](https://user-images.githubusercontent.com/120908587/218327137-d42007b7-7e74-44b2-90b6-8f621ee8d6f8.png)


```sql 
with cte as(
select  order_date, row_number() over(partition by customer_id order by 
order_date asc) as rn from customer_orders)
select order_date, 
sum(case when rn=1 then 1 else 0 end) as new_customers,
sum(case when rn>1 then 1 else 0 end) as repeat_customers from cte
group by order_date;

```


* Another Solution

```sql 



with first_visit as (select customer_id, min(order_date) as first_visit_date
from customer_orders
group by customer_id)
select c.order_date,
sum(case when c.order_date = fv.first_visit_date then 1 else 0 end) as new,
sum(case when c.order_date != fv.first_visit_date then 1 else 0 end) as repeat
from customer_orders c
join first_visit fv
on c.customer_id = fv.customer_id
group by c.order_date
```


