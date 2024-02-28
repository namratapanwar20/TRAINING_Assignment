**17. BOPIS orders Revenue in the last year:**
```sql
select 
  sum(oi.quantity * oi.unit_price) 
from 
  order_item oi 
  join order_header oh on oi.order_id = oh.order_id
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id  
    and oisga.order_item_seq_id = oi.order_item_seq_id 
  join order_item_ship_group oisg on oisg.order_id = oh.order_id 
  	and oisg.ship_group_seq_id = oisga.ship_group_seq_id
where 
  oisg.shipment_method_type_id = 'STOREPICKUP' 
  and oh.order_date >= date_sub(
    CURDATE(), 
    INTERVAL 1 YEAR
  );
```
