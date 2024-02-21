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
      DATEDIFF(
        CURDATE(), 
        ENTRY_DATE
      )<= 7
  );
```
