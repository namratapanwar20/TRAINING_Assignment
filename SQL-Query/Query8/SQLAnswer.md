**8. How many orders with a single return were recorded in the last month?**

```sql
select 
	oh.order_id orders_with_single_return 
from 
	order_header oh 
	join return_item ri on oh.order_id = ri.order_id 
	join return_header rh on rh.return_id = ri.return_id 
where 
	rh.entry_date >= date_format(curdate() - interval 1 month, '%y-%m-01')
    and rh.entry_date < date_format(curdate(), '%y-%m-01')
group by 
	oh.order_id
having 
	count(ri.return_id)=1;
```
