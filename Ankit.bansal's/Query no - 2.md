# Question - 2
 
</details>
<br>
<details>
  <summary>Click here to check the question !</summary>
<br>
Write a sql query to find users who purchased different products on different dates 
ie: products purchased on any given day are not repeated on any other day
</details>
<br>

</details>
<br>
<details>
  <summary>Here is the script !</summary>
<br>
  
``
  create table purchase_history
(userid int
,productid int
,purchasedate date
);
SET DATEFORMAT dmy;
insert into purchase_history values
(1,1,'23-01-2012')
,(1,2,'23-01-2012')
,(1,3,'25-01-2012')
,(2,1,'23-01-2012')
,(2,2,'23-01-2012')
,(2,2,'25-01-2012')
,(2,4,'25-01-2012')
,(3,4,'23-01-2012')
,(3,1,'23-01-2012')
,(4,1,'23-01-2012')
,(4,2,'25-01-2012')
;``
  
  </details>
<br>

``
# Input should be like this
``

![image](https://user-images.githubusercontent.com/120908587/217746613-ad8aabe9-b4cb-4cc6-b482-d907172b01a0.png)




```sql 
-- lead 
select id, count(1) as total_rides,
sum(case when end_loc = next_strt_loc then 1 else 0 end) as profit_rides from
(select * ,
lead(start_loc, 1) over( partition by id order by start_time) as next_strt_loc from drivers) a 
group by id 
```


* Another Solution

```sql 

with rides as 
(select *, ROW_NUMBER() over(partition by id order by start_time asc) as rn from drivers)
select r1.id, count(1) as total_rides , count(r2.id) as profit_rides
from rides r1
left join rides r2
on r1.id= r2.id and r1.end_loc = r2.start_loc and r1.rn+1 = r2.rn
group by r1.id
```
