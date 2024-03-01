**8. Orders that have more than one item in a single ship group:**
```sql
select 
  ORDER_ID, 
  count(ORDER_ID) 
from 
  order_item_ship_group_assoc 
where 
  ORDER_ID in (
    select 
      ORDER_ID 
    from 
      order_item_ship_group_assoc 
    group by 
      ORDER_ID, 
      SHIP_GROUP_SEQ_ID 
    having 
      count(ORDER_ITEM_SEQ_ID)> 1
  ) 
group by 
  ORDER_ID;
```
