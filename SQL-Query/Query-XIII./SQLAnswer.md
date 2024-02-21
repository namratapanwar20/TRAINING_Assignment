**13. Facility wise Revenue for (SM Store):**
```sql
select 
  sum(oi.unit_price * oi.quantity) as total_unit, 
  f.facility_id 
from 
  order_item oi 
  join order_header oh on oh.order_id = oi.order_id 
  join facility f on oh.origin_facility_id = f.facility_id 
where 
  f.facility_type_id = 'RETAIL_STORE' 
  or f.facility_type_id = 'OUTLET_STORE' 
group by 
  f.facility_id;
```
