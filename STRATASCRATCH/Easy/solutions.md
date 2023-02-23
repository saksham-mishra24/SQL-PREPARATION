### Question No. 1
### 📌 Airbnb | 
[Question : ](https://platform.stratascratch.com/coding/9622-number-of-bathrooms-and-bedrooms?code_type=5)

Find the average number of bathrooms and bedrooms for each city’s property types. Output the result along with the city name and the property type.


* INPUT


![image](https://user-images.githubusercontent.com/120908587/220550230-a57363b5-eca3-400b-9c54-1061296bae41.png)


* QUERY 


```sql
SELECT 
  city_name, 
  property_type, 
  AVG(bedrooms) AS avg_bedrooms, 
  AVG(bathrooms) AS avg_bathrooms 
FROM 
  airbnb_search_details 
GROUP BY 
  city_name, 
  property_type
order by city
```
* OUTPUT

<img width="597" alt="image" src="https://user-images.githubusercontent.com/81607668/172528878-b77567f6-9890-40c5-9040-23caf7a70204.png">
