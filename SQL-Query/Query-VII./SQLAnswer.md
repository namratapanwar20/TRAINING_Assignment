**7. Payment captured but not shipped order items:** <br>

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

Query Cost --> 

![Screenshot from 2024-02-28 17-51-25](https://github.com/namratapanwar20/TRAINING_Assignment/assets/116093745/3b928d55-7dfd-492a-830b-d495b3452536)


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

Query Cost --> 

![Screenshot from 2024-02-28 17-55-06](https://github.com/namratapanwar20/TRAINING_Assignment/assets/116093745/c88446ab-d9a4-4ff4-92e9-3fb96a9e7482)



