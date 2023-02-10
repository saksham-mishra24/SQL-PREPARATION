# Question - 4

</details>
<br>
<details>
  <summary>Click here to check the question !</summary>
<br>
Scenario:

There is a live production system with a table ("ORDERS") that captures order information in real-time.
We wish to capture "deltas" from this table (inserts and deletes) by leveraging a nightly copy of the table. 
There are no timestamps that can be used for delta processing.

ORDER

ORDER_ID (Primary Key)

This table processes 10,000 transactions per day, including INSERTS, UPDATES, and DELETES. The DELETEs are physical, so the records will no longer exist in the table.

Every day at 12:00AM, a snapshot (copy) of this table created and is an exact copy of the table at that time.

ORDER_COPY

ORDER_ID (Primary Key)

Requirement:

Write a query that (as efficiently as possible) will return only new INSERTS into ORDER since the snapshot was taken (record is in ORDER, but not ORDER_COPY) OR
only new DELETES from ORDER since the snapshot was taken (record is in ORDER_COPY, but not ORDER).

The query should return the Primary Key ( ORDE R \ ID) and a single character ("INSERT_OR_DELETE_FLAG") of "I" if it is an INSERT, or u D^ prime prime if it is a DELETE. 
 For example, consider the Ven Diagram below depicting Inserts and Deletes and the desired result set:
  
</details>
<br>

</details>
<br>
<details>
  <summary>Here is the script !</summary>
<br>

``create table tbl_orders (
order_id integer,
order_date date
);
insert into tbl_orders
values (1,'2022-10-21'),(2,'2022-10-22'),
(3,'2022-10-25'),(4,'2022-10-25');

select * into tbl_orders_copy from  tbl_orders;

select * from tbl_orders;
insert into tbl_orders
values (5,'2022-10-26'),(6,'2022-10-26');
delete from tbl_orders where order_id=1;
``
  
  </details>
<br>

``
# Input should be like this
``

![image](https://user-images.githubusercontent.com/120908587/218005759-9b1298d9-15d1-424b-b24f-668f5bfbc927.png)




```sql 
select coalesce(o.order_id, c.order_id) as details,
case 
when c.order_id is NULL then 'I' 
 when o.order_id is NULL then 'D' end as flag
from tbl_orders o
full  outer join  tbl_orders_copy c
on o.order_date = c.order_date 
where c.order_id is null or o.order_id is null
```










