**1. How many single-item orders were fulfilled from warehouses in the last month?**

```sql
select 
  count(*) 
from 
  order_header oh 
  join order_item oi on oh.order_id = oi.order_id 
  join order_status os ON oh.order_id = os.order_id
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id 
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id
  join facility f on f.facility_id = oisg.facility_id
  join facility_type ft on f.facility_type_id = ft.facility_type_id
where 
  ft.parent_type_id = "DISTRIBUTION_CENTER" 
  and oh.status_id = "ORDER_COMPLETED" 
  and os.status_datetime >= date_sub(
    CURDATE(), 
    INTERVAL 1 MONTH
  ) 
group by 
  oi.order_id 
having 
  count(oi.order_item_seq_id)= 1;
```
