# Question - 7

</details>
<br>
<details>
  <summary>Click here to check the question !</summary>
<br>

</details>
<br>

</details>
<br>
<details>
  <summary>Here is the script !</summary>
<br>

``
  create table phonelog(
    Callerid int, 
    Recipientid int,
    Datecalled datetime
);

insert into phonelog(Callerid, Recipientid, Datecalled)
values(1, 2, '2019-01-01 09:00:00.000'),
       (1, 3, '2019-01-01 17:00:00.000'),
       (1, 4, '2019-01-01 23:00:00.000'),
       (2, 5, '2019-07-05 09:00:00.000'),
       (2, 3, '2019-07-05 17:00:00.000'),
       (2, 3, '2019-07-05 17:20:00.000'),
       (2, 5, '2019-07-05 23:00:00.000'),
       (2, 3, '2019-08-01 09:00:00.000'),
       (2, 3, '2019-08-01 17:00:00.000'),
       (2, 5, '2019-08-01 19:30:00.000'),
       (2, 4, '2019-08-02 09:00:00.000'),
       (2, 5, '2019-08-02 10:00:00.000'),
       (2, 5, '2019-08-02 10:45:00.000'),
       (2, 4, '2019-08-02 11:00:00.000');
  ``
  
  </details>
<br>

``
# Input should be like this
``

![image](https://user-images.githubusercontent.com/120908587/218095113-ce933433-edf0-45cc-a6ac-e27abde055c3.png)




```sql 
with ct as (select callerid,cast(datecalled as date) as called_date ,min(datecalled) as first_day,max(datecalled) as last_day
from phonelog
group by callerid,cast(datecalled as date))

select c.*,p1.Recipientid from ct c
inner join phonelog p1 on c.callerid = p1.callerid and c.first_day = p1.Datecalled
inner join phonelog p2 on c.callerid = p2.callerid and c.last_day = p2.Datecalled
where p1.Recipientid = p2.Recipientid
```
