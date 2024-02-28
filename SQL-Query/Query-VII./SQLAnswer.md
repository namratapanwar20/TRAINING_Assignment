**7. Payment captured but not shipped order items:**
Using "not in" :

```sql
select 
  oi.ORDER_ID, 
  opp.STATUS_ID, 
  oi.STATUS_ID 
from 
  order_item oi 
  join order_payment_preference opp on oi.ORDER_ID = opp.ORDER_ID 
where 
  opp.STATUS_ID = 'PAYMENT_SETTLED' 
  and (
  	oi.STATUS_ID not in ('ITEM_CANCELLED','ITEM_COMPLETED')
  );
```
Using "and" :

```sql
select 
  oi.ORDER_ID, 
  opp.STATUS_ID, 
  oi.STATUS_ID 
from 
  order_item oi 
  join order_payment_preference opp on oi.ORDER_ID = opp.ORDER_ID 
where 
  opp.STATUS_ID = 'PAYMENT_SETTLED' 
  and (
    oi.STATUS_ID != 'ITEM_CANCELLED' 
    and oi.STATUS_ID != 'ITEM_COMPLETED'
  );
```
