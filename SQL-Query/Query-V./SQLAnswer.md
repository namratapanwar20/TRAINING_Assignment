**5. Last week imported orders & items count:**
```sql
Select 
  count(ORDER_ID), 
  sum(QUANTITY) 
from 
  order_item 
where 
  ORDER_ID in (
    select 
      ORDER_ID 
    from 
      order_header 
    where 
      entry_date >= date_sub(curdate(), interval dayofweek(curdate())+7 day)
      and entry_date < date_sub(curdate(), interval dayofweek(curdate()) day)
  );
```
