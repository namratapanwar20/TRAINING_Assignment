**1. Total number of shipments in January 2022 first quarter:**
```sql
select 
  count(SHIPMENT_ID) 
from 
  shipment_status 
where 
  STATUS_ID = ’SHIPMENT_SHIPPED’ 
  and Month(STATUS_DATE) in (1, 3) 
  and Year(STATUS_DATE)= 2022;
```
