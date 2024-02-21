**15. Shipping Revenue last month:**
```sql
select 
  sum(amount) as shipping_revenue 
from 
  order_adjustment 
where 
  created_date >= date_sub(
    CURDATE(), 
    INTERVAL 1 MONTH
  ) 
  and order_adjustment_type_id = 'SHIPPING_CHARGES';
```
```sql
select 
  sum(oa.amount) as shipping_revenue 
from 
  order_adjustment oa 
  join order_header oh on oa.order_id = oh.order_id 
where 
  oa.created_date >= date_sub(
    CURDATE(), 
    INTERVAL 1 MONTH
  ) 
  and oa.order_adjustment_type_id = 'SHIPPING_CHARGES' 
  and oh.status_id = 'ORDER_COMPLETED';
```
