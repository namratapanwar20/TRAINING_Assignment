**14. Shipping Refund in the last month:**
```sql
select 
  sum(amount) as refunded_amount 
from 
  return_adjustment 
where 
  created_date >= date_format(curdate() - interval 1 month, '%y-%m-01')
  and created_date < date_format(curdate(), '%y-%m-01')
  and return_adjustment_type_id = 'RET_SHIPPING_ADJ';
```
