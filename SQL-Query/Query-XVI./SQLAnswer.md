**16. Send sale orders shipped from the warehouse:**
```sql
select 
  order_id 
from 
  order_header 
where 
  sales_channel_enum_id = 'POS_SALES_CHANNEL' 
  and origin_facility_id in (
    select 
      facility_id 
    from 
      facility 
    where 
      facility_type_id = 'WAREHOUSE'
  );
```
