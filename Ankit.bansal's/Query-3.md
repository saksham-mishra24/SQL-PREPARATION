# Question - 3
 
</details>
<br>
<details>
  <summary>Click here to check the question !</summary>
<br>
write a query to print total rides and profit rides for each driver 
profit ride is when the end location of current ride is same as start location on next ride

</details>
<br>

</details>
<br>
<details>
  <summary>Here is the script !</summary>
<br>
  
``
 create table drivers(id varchar(10), start_time time, end_time time, start_loc varchar(10), end_loc varchar(10));
insert into drivers values('dri_1', '09:00', '09:30', 'a','b'),('dri_1', '09:30', '10:30', 'b','c'),('dri_1','11:00','11:30', 'd','e');
insert into drivers values('dri_1', '12:00', '12:30', 'f','g'),('dri_1', '13:30', '14:30', 'c','h');
insert into drivers values('dri_2', '12:15', '12:30', 'f','g'),('dri_2', '13:30', '14:30', 'c','h');
;``
  
  </details>
<br>

``
# Input should be like this
``

![image](https://user-images.githubusercontent.com/120908587/217745647-f4bdb17e-f3b4-4cac-a29b-cb033a852506.png)




```sql 
with cte as 
(select userid, count(distinct purchasedate) as dates_purchsed_by,count( productid) as product_purchased,
count(distinct productid) as distinct_product_purchased from purchase_history
group by userid)

select userid from cte where  dates_purchsed_by  > 1 and product_purchased = distinct_product_purchased
```


* Another Solution

```sql 
with cte1 as
(select a.* from purchase_history as a left join
(select userid , productid , count(1) as product_count from purchase_history group by userid , productid having count(1) > 1)
as b on a.userid = b.userid where b.userid is null) 

select userid from cte1 group by userid
having count(distinct purchasedate) > 1;
```
