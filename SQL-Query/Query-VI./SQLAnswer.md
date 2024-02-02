**6. Fetch all the physical items completed from Warehouse in September of 2023.**

```sql
select 
  oi.order_id, 
  oi.order_item_seq_id 
from 
  order_item oi 
  join order_header oh on oh.order_id = oi.order_id 
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id 
  and oisga.order_item_seq_id = oi.order_item_seq_id 
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id 
  join product p on oi.product_id = p.product_id 
  join product_type pt on p.product_type_id = pt.product_type_id 
  join facility f on f.facility_id = oisg.facility_id 
  join order_status os on oi.order_id = os.order_id 
  and oi.status_id = os.status_id 
  and oi.order_item_seq_id = os.order_item_seq_id 
where 
  pt.is_physical = "Y" 
  and f.facility_type_id = "WAREHOUSE" 
  and Month(os.status_datetime)= 8 
  and Year(os.status_datetime)= 2023 
  and os.status_id = "ITEM_COMPLETED";

```
