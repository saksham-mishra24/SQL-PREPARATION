# Question - 8
 
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
create table students
(
student_id int,
student_name varchar(20)
);
insert into students values
(1,'Daniel'),(2,'Jade'),(3,'Stella'),(4,'Jonathan'),(5,'Will');

create table exams
(
exam_id int,
student_id int,
score int);

insert into exams values
(10,1,70),(10,2,80),(10,3,90),(20,1,80),(30,1,70),(30,3,80),(30,4,90),(40,1,60)
,(40,2,70),(40,4,80);
;``
  
  </details>
<br>

``
# Input should be like this
``
![image](https://user-images.githubusercontent.com/120908587/218140554-cd58d79e-520c-4b6e-b257-9c25cef6d816.png)



```sql 
with ct as
(select exam_id, min(score) as min_score,  max(score) as max_score from exams
group by exam_id)
select e.student_id from exams e
inner join ct c on  e.exam_id =  c.exam_id
group by student_id
having max(case when score = min_score or score = max_score then 1 else 0 end) = 0

```


* Another Solution

```sql 



with hig_low_score as ( Select *,
Row_number() over (Partition by exam_id order by score desc) as High_rank,
Row_number() over (Partition by exam_id order by score ) as low_rank from exams)
select Distinct e.Student_id from exams e
where  e.student_id not in (Select student_id from hig_low_score where High_rank=1 or low_rank=1)
order by e.Student_id asc
```


