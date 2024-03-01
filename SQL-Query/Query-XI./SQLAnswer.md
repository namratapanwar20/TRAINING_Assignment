**11. Orders completed hourly:**
```sql
select 
  hour(STATUS_DATETIME) as hours, 
  count(*) 
from 
  order_status 
where 
  STATUS_ID = 'ORDER_COMPLETED' 
group by 
  hours;
```
