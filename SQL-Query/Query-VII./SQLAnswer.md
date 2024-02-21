**7. Payment captured but not shipped order items:**
```sql
select 
  oh.ORDER_ID, 
  opp.STATUS_ID, 
  oh.STATUS_ID 
from 
  order_header oh 
  join order_payment_preference opp on oh.ORDER_ID = opp.ORDER_ID 
where 
  opp.STATUS_ID = 'PAYMENT_SETTLED' 
  and (
    oh.STATUS_ID != 'ORDER_CANCELLED' 
    and oh.STATUS_ID != 'ORDER_COMPLETED'
  );
```
