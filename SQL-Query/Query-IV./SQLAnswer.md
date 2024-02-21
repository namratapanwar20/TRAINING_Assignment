**4. Shipped units By Location:**
```sql
select 
  count(FACILITY_ID) facilities, 
  FACILITY_TYPE_ID 
from 
  facility 
where 
  FACILITY_ID in (
    select 
      DESTINATION_FACILITY_ID 
    from 
      shipment
  ) 
group by 
  FACILITY_TYPE_ID;
```
