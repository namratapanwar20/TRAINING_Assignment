**2. Fetch the following columns for completed return items of SM_STORE for ecom return channel.<br>
RETURN_ID <br>
ORDER_ID<br>
PRODUCT_STORE_ID<br> 
STATUS_DATETIME<br>
ORDER_NAME <br>
FROM_PARTY_ID <br>
RETURN_DATE <br>
ENTRY_DATE<br>
RETURN_CHANNEL_ENUM_ID** <br>

```sql
SELECT 
  rh.return_id, 
  oh.order_id, 
  oh.product_store_id, 
  rs.status_datetime, 
  oh.order_name, 
  rh.from_party_id, 
  rh.return_date, 
  rh.entry_date, 
  rh.return_channel_enum_id 
FROM 
  return_header rh 
  JOIN return_item ri ON ri.return_id = rh.return_id 
  JOIN order_item oi ON ri.order_id = oi.order_id 
  and oi.order_item_seq_id = ri.order_item_seq_id 
  JOIN order_header oh ON oi.order_id = oh.order_id 
  JOIN return_status rs ON rs.return_item_seq_id = ri.return_item_seq_id 
  and ri.status_id = rs.status_id 
  and ri.return_id = rs.return_id 
where 
  oh.product_store_id = "SM_STORE" 
  and rs.status_id = "RETURN_COMPLETED" 
  and rh.return_channel_enum_id = "ECOM_RTN_CHANNEL";
```
