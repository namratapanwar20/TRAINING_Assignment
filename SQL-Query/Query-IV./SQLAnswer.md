**4. Fetch the following columns for created orders. These should be sales orders.<br>
ORDER_ID<br>
TOTAL_AMOUNT<br>
PAYMENT_METHOD<br>
SHOPIFY_ORDER_NAME<br>
NOTE: <br>
The total amount represents the total amount of the order.<br>
The payment method is the method by which payment was made, like Cash, mastercard, visa, paypal,etc.**<br>

```sql
select 
  oh.order_id, 
  oh.grand_total as total_amount, 
  pay.description as payment_method, 
  od.id_value
from 
  order_header oh 
  join order_payment_preference opp on oh.order_id = opp.order_id 
  join payment_method_type pay on pay.payment_method_type_id = opp.payment_method_type_id 
  join order_identification od on oh.order_id = od.order_id 
where 
  oh.status_id = "ORDER_CREATED" 
  and oh.order_type_id = "SALES_ORDER" 
  and od.order_identification_type_id = "SHOPIFY_ORD_NAME";
```
