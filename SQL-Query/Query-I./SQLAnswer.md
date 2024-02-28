**1. Total number of shipments in January 2022 first quarter:**
```sql
select 
  count(SHIPMENT_ID) 
from 
  shipment_status 
where 
  STATUS_ID = "SHIPMENT_SHIPPED"
  and STATUS_DATE between '2022-01-01' and '2022-01-31';
```
