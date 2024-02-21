**17. BOPIS orders Revenue in the last year:**
```sql
select 
  sum(oi.quantity * oi.unit_price) 
from 
  order_item oi 
  join order_header oh on oi.order_id = oh.order_id 
  join order_item_ship_group oisg on oisg.order_id = oh.order_id 
where 
  oisg.shipment_method_type_id = 'STOREPICKUP' 
  and oh.order_date >= date_sub(
    CURDATE(), 
    INTERVAL 1 YEAR
  );
```
