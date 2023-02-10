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






