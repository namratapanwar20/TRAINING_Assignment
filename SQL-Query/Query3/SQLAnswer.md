**3. In the period following the New Year, what is the number of orders shipped from stores in the first 25 days?**

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
      and STATUS_DATETIME >= '2024-01-01' 
      AND STATUS_DATETIME < '2024-01-01' + INTERVAL 25 DAY
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
