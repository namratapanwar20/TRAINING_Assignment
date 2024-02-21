**9. Find orders where multiple items are grouped and shipped together in a single shipment:**
```sql
select 
  ORDER_ID, 
  count(ORDER_ID), 
  STATUS_ID 
from 
  order_item 
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
  and STATUS_ID = 'ITEM_COMPLETED' 
group by 
  ORDER_ID;
```
