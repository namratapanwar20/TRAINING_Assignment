**4. Shipped units By Location:**
```sql
select 
  s.origin_facility_id,
  sum(si.quantity)
from 
  shipment s 
  join shipment_item si on s.shipment_id = si.shipment_id 
where 
  s.status_id = "SHIPMENT_SHIPPED" 
group by 
  s.origin_facility_id;
```
