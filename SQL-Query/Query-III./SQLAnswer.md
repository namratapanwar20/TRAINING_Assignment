**3. Average number of shipments per month:**
```sql
select 
  count(SHIPMENT_ID)/ count(
    distinct extract(
      YEAR_MONTH 
      from 
        STATUS_DATE
    )
  ) as AVERAGE 
from 
  shipment_status 
where 
  status_id = 'SHIPMENT_SHIPPED';
```
