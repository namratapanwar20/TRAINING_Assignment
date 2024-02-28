**16. Send sale orders shipped from the warehouse:**
```sql
select 
  oh.order_id 
from 
  order_header oh 
  join order_item oi on oh.order_id = oi.order_id 
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id 
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id
  join facility f on f.facility_id = oisg.facility_id 
  join facility_type ft on ft.facility_type_id = f.facility_type_id
where 
  oh.sales_channel_enum_id = "POS_SALES_CHANNEL" 
  and ft.parent_type_id = "DISTRIBUTION_CENTRE"; 
```
