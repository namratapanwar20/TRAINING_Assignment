**7.Fetch all the physical items ordered in the month of September 2023.**

```sql
select 
  oi.order_id, 
  oi.order_item_seq_id 
from 
  order_item oi 
  join product p on oi.product_id = p.product_id 
  join product_type pt on p.product_type_id = pt.product_type_id and pt.is_physical = "Y"
  join order_status os on oi.order_id = os.order_id 
  and oi.status_id = os.status_id and (oi.status_id = "ITEM_COMPLETED" or oi.status_id = "ITEM_CANCELLED")
  and oi.order_item_seq_id = os.order_item_seq_id  and  Month(os.status_datetime)= 9 
  and Year(os.status_datetime)= 2023 ;
```
