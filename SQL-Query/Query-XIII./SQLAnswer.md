**13. Facility wise Revenue for (SM Store):**
```sql
select 
  sum(oi.unit_price * oi.quantity) as total_unit, 
  f.facility_id 
from 
  order_item oi 
  join order_header oh on oh.order_id = oi.order_id 
  join order_status os ON oh.order_id = os.order_id
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id 
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id
  join facility f on f.facility_id = oisg.facility_id 
  join facility_type ft on ft.facility_type_id = f.facility_type_id
where 
  ft.parent_type_id = "PHYSICAL_STORE"
group by 
  f.facility_id;
```
