**10. Orders brokered but not shipped:**
```sql
select 
  ORDER_ID 
from 
  order_header 
where 
  ORIGIN_FACILITY_ID != '_NA_' 
  and STATUS_ID != 'ORDER_COMPLETED' 
  and STATUS_ID != 'ORDER_CANCELLED';
```
