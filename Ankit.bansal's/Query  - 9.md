# Question - 9
 
</details>
<br>
<details>
  <summary>Click here to check the question !</summary>
<br>
write a query to print total number of wins and losses and match played by each teams.

</details>
<br>

</details>
<br>
<details>
  <summary>Here is the script !</summary>
<br>
  
``
create table icc_world_cup
(
Team_1 Varchar(20),
Team_2 Varchar(20),
Winner Varchar(20)
);
INSERT INTO icc_world_cup values('India','SL','India');
INSERT INTO icc_world_cup values('SL','Aus','Aus');
INSERT INTO icc_world_cup values('SA','Eng','Eng');
INSERT INTO icc_world_cup values('Eng','NZ','NZ');
INSERT INTO icc_world_cup values('Aus','India','India');
;``
  
  </details>
<br>

``
# Input should be like this
``
![image](https://user-images.githubusercontent.com/120908587/218326938-25516406-b96b-4ae7-8d81-5395704038f7.png)



```sql 
select team_name,count(1) as total_machtes, sum(win_flag) as total_wins, count(1) - sum(win_flag) as total_loss
from(
select team_1 as team_name, case when team_1 = winner then 1 else 0 end as win_flag
from icc_world_cup
union all
select team_2 as team_name , case when team_2 = winner then 1 else 0 end as win_flag
from icc_world_cup) as a
group by team_name
order by total_wins desc
```



