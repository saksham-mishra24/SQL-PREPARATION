# Question - 6

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

``create table candidates (
emp_id int,
experience varchar(20),
salary int
);
delete from candidates;
insert into candidates values
(1,'Junior',10000),(2,'Junior',15000),(3,'Junior',40000),(4,'Senior',16000),(5,'Senior',20000),(6,'Senior',50000);
``
  
  </details>
<br>

``
# Input should be like this
``

![image](https://user-images.githubusercontent.com/120908587/218094459-066eca34-7f8c-41cd-9a96-77cada3bee1f.png)




```sql 

with ct1 as 
  (select *, sum(salary) over(partition by experience order by salary ) as running_slry from candidates)
 , senior as ( select * from ct1 where running_slry <= 70000 and experience = 'Senior')

 select * from ct1 where  experience = 'Junior' and salary <=  70000-(select sum(salary) from senior)
 union all
 select * from senior
```










