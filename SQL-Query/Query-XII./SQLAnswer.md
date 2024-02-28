**12. Maximum units fulfilled by location:**
```sql
select 
  f.facility_id, 
  sum(oi.QUANTITY) as total 
from 
  order_header oh 
  join order_item oi on oh.ORDER_ID = oi.ORDER_ID 
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id 
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id
  join facility f on f.facility_id = oisg.facility_id 
where 
  oh.STATUS_ID = 'ORDER_COMPLETED' 
group by 
  f.facility_id
order by 
  total desc 
limit 
  1;
```
