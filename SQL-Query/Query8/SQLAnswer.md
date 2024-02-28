**8. How many orders with a single return were recorded in the last month?**

```sql
select 
  order_id as orders_with_single_return 
from 
  order_header 
where 
  order_id in (
    select 
      order_id 
    from 
      return_item 
    where 
      return_id in (
        select 
          return_id 
        from 
          return_header 
        where 
          entry_date >= date_sub(
            CURDATE(), 
            INTERVAL 1 MONTH
          )
      ) 
    group by 
      order_id 
    having 
      count(return_id)= 1
  );
```
