**12.Get all the appeasements in July month.<br>
a.How do we differentiate between returns and appeasements?<br>
b.Get all the below fields <br>
(Appeasements in return_adjustment_type)<br>
RETURN_ID<br>
ENTRY_DATE <br>
RETURN_ADJUSTMENT_TYPE_ID <br>
AMOUNT <br>
COMMENTS <br>
ORDER_ID <br>
ORDER_DATE <br>
RETURN_DATE, <br>
PRODUCT_STORE_ID**

```sql
select 
  rh.return_id, 
  rh.entry_date, 
  ra.return_adjustment_type_id, 
  ra.amount, 
  ra.comments, 
  ra.order_id, 
  oh.order_date, 
  rh.return_date, 
  oh.product_store_id 
from 
  return_header rh 
  join return_adjustment ra on rh.return_id = ra.return_id 
  join order_header oh on oh.order_id = ra.order_id 
where 
  ra.return_adjustment_type_id = "APPEASEMENT" 
  and MONTH(rh.return_date)= 7 
  and YEAR(rh.return_date)= 2023;
```
