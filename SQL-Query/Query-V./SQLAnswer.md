**5.Fetch the following data for completed order items in July of 2023.<br>
ORDER_ID<br>
ORDER_ITEM_SEQ_ID<br>
SHOPIFY_ORDER_ID<br>
SHOPIFY_PRODUCT_ID**<br>


```sql
select 
  oi.order_id, 
  oi.order_item_seq_id, 
  od.id_value as SHOPIFY_ORDER_ID, 
  gd.id_value as SHOPIFY_PRODUCT_ID 
from 
  order_item oi 
  join order_status os on oi.order_id = os.order_id 
  and oi.status_id = os.status_id 
  and oi.order_item_seq_id = os.order_item_seq_id 
  join order_identification od on oi.order_id = od.order_id 
  join good_identification gd on gd.product_id = oi.product_id 
where 
  Month(os.status_datetime)= 7 
  and Year(os.status_datetime)= 2023 
  and od.order_identification_type_id = "SHOPIFY_ORD_ID" 
  and os.status_id = "ITEM_COMPLETED" 
  and gd.good_identification_type_id = "SHOPIFY_PROD_ID";

```
