**1. How many single-item orders were fulfilled from warehouses in the last month?**

```sql
select 
  count(*) 
from 
  order_header oh 
  join order_item oi on oh.order_id = oi.order_id 
  join order_status os ON oi.order_item_seq_id = os.order_item_seq_id 
  and oh.order_id = os.order_id 
  join facility f on f.facility_id = oh.origin_facility_id 
where 
  f.facility_type_id = "WAREHOUSE" 
  and oi.status_id = "ORDER_COMPLETED" 
  and os.status_datetime >= date_sub(
    CURDATE(), 
    INTERVAL 1 MONTH
  ) 
group by 
  oi.order_id 
having 
  count(oi.order_item_seq_id)= 1;
```
