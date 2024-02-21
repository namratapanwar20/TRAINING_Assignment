**14. Shipping Refund in the last month:**
```sql
select 
  sum(amount) as refunded_amount 
from 
  return_adjustment 
where 
  created_date >= date_sub(
    CURDATE(), 
    INTERVAL 1 MONTH
  ) 
  and return_adjustment_type_id = 'RET_SHIPPING_ADJ';
```
