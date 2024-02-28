**12. Maximum units fulfilled by location:**
```sql
select 
  f.facility_id, 
  sum(oi.QUANTITY) as total 
from 
  order_item oi
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id 
  and oisga.order_item_seq_id = oi.order_item_seq_id
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id
  join facility f on f.facility_id = oisg.facility_id and f.facility_id is not null
where 
  oi.STATUS_ID = 'ITEM_COMPLETED'
group by 
  oisg.facility_id
order by 
  total desc 
limit 
  1;
```
