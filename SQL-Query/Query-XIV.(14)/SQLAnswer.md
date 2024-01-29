**14.Fetch the inventory variances of the products where the reason is ‘VAR_LOST’ or VAR_DAMAGED.**
```sql
select 
  ii.product_id 
from 
  inventory_item ii 
  join inventory_item_variance iiv on iiv.inventory_item_id = ii.inventory_item_id 
where 
  iiv.variance_reason_id = "VAR_DAMAGED" 
  or iiv.variance_reason_id = "VAR_LOST";
```
