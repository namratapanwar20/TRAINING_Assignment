**10. Orders brokered but not shipped:**
```sql
select 
select 
  count(oh.ORDER_ID) 
from 
  order_header oh 
  join order_item oi on oh.order_id = oi.order_id 
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id
  and oisga.order_item_seq_id = oi.order_item_seq_id
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id
  join facility f on f.facility_id = oisg.facility_id 
where 
  f.FACILITY_ID != '_NA_' 
  and oh.STATUS_ID != 'ORDER_COMPLETED' 
  and oh.STATUS_ID != 'ORDER_CANCELLED';
```
