**2. Leading up to the New Year, what is the count of orders shipped from stores in the 25 days preceding the New Year?**

```sql
select 
  count(order_id) 
from 
  order_header 
where 
  order_id in (
    select 
      order_id 
    from 
      order_status 
    where 
      status_id = "ORDER_COMPLETED" 
      and STATUS_DATETIME >= '2024-01-01' - INTERVAL 25 DAY 
      AND STATUS_DATETIME < '2024-01-01'
  ) 
  and origin_facility_id in (
    select 
      facility_id 
    from 
      facility 
    where 
      facility_type_id = "RETAIL_STORE" 
      or facility_type_id = "OUTLET_STORE"
  );

```
