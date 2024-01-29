**9.Find all the orders whose two or more items are canceled but the orders are still in the approved status.**

```sql
select 
  order_id 
from 
  order_header 
where 
  order_id in (
    select 
      order_id 
    from 
      order_item 
    where 
      status_id = "ITEM_CANCELLED" 
    group by 
      order_id 
    having 
      count(order_item_seq_id)>= 2
  ) 
  and status_id = "ORDER_APPROVED";

```
