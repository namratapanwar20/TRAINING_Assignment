**12. Maximum units fulfilled by location:**
```sql
select 
  oh.ORIGIN_FACILITY_ID, 
  sum(oi.QUANTITY) as total 
from 
  order_header oh 
  join order_item oi on oh.ORDER_ID = oi.ORDER_ID 
where 
  oh.STATUS_ID = 'ORDER_COMPLETED' 
group by 
  oh.ORIGIN_FACILITY_ID 
order by 
  total desc 
limit 
  1;
```
