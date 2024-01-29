**1.Fetch the following columns for completed order items for sales orders of SM_STORE product store and those are physical items.<br>
ORDER_ID<br>
ORDER_ITEM_SEQ_ID<br>
PRODUCT_ID<br>
PRODUCT_TYPE_ID<br>
IS_PHYSICAL<br>
IS_DIGITAL<br>
SALES_CHANNEL_ENUM_ID<br>
ORDER_DATE<br>
ENTRY_DATE<br>
STATUS_ID<br>
STATUS_DATETIME<br>
ORDER_TYPE_ID<br>
PRODUCT_STORE_ID** 

```sql
SELECT 
  oh.order_id, 
  oi.order_item_seq_id, 
  p.product_id, 
  pt.is_physical, 
  pt.is_digital, 
  oh.sales_channel_enum_id, 
  oh.order_date, 
  oh.entry_date, 
  os.status_datetime, 
  oh.order_type_id, 
  oh.product_store_id 
FROM 
  order_item oi 
  JOIN order_header oh ON oi.order_id = oh.order_id 
  JOIN product p ON oi.product_id = p.product_id 
  JOIN product_type pt ON p.product_type_id = pt.product_type_id 
  JOIN order_status os ON oi.order_item_seq_id = os.order_item_seq_id 
  and oi.status_id = os.status_id 
  and oi.order_id = os.order_id 
where 
  pt.is_physical = "Y" 
  and os.status_id = "ITEM_COMPLETED" 
  and oh.product_store_id = "SM_STORE" 
  and oh.order_type_id = "SALES_ORDER";

```
