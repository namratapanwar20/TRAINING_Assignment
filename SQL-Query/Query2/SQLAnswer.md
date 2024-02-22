**2. Leading up to the New Year, what is the count of orders shipped from stores in the 25 days preceding the New Year?**

```sql
select 
  count(oh.order_id)
from 
  order_header oh 
  join order_item oi on oh.order_id = oi.order_id 
  join order_status os on os.order_id = oh.order_id  and oh.status_id=os.status_id
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id 
  and oisga.order_item_seq_id = oi.order_item_seq_id 
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id 
  join facility f on f.facility_id = oisg.facility_id 
where 
  oh.status_id = "ORDER_COMPLETED" 
  and os.STATUS_DATETIME >= '2024-01-01' - INTERVAL 25 DAY 
  and os.STATUS_DATETIME < '2024-01-01' 
  and (
    facility_type_id = "RETAIL_STORE" 
    or facility_type_id = "OUTLET_STORE"
  );
```
