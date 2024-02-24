**13. Fetch the following details with their orders completed in August 2023.<br>
PRODUCT_ID <br>
PRODUCT_TYPE_ID<br>
PRODUCT_STORE_ID <br>
TOTAL_QUANTITY<br>
INTERNAL_NAME <br>
FACILITY_ID<br>
EXTERNAL_ID <br>
FACILITY_TYPE_ID<br> 
ORDER_HISTORY_ID <br>
ORDER_ID<br>
ORDER_ITEM_SEQ_ID<br>
SHIP_GROUP_SEQ_ID**

```sql
select 
  p.product_id, 
  p.product_type_id, 
  oh.product_store_id, 
  sum(oi.quantity) as TOTAL_QUANTITY, 
  p.internal_name, 
  p.facility_id, 
  oi.external_id, 
  f.facility_type_id, 
  ohist.order_history_id, 
  oi.order_id, 
  oi.order_item_seq_id, 
  oi.ship_group_seq_id 
from 
  order_header oh 
  join order_item oi on oh.order_id = oi.order_id 
  join product p on p.product_id = oi.product_id 
  join order_history ohist on oi.order_id = ohist.order_id 
  and oi.order_item_seq_id = ohist.order_item_seq_id 
  join order_item_ship_group_assoc oisga on oisga.order_id = oi.order_id 
  and oisga.order_item_seq_id = oi.order_item_seq_id 
  join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
  and oisg.ship_group_seq_id = oisga.ship_group_seq_id 
  join facility f on f.facility_id = oisg.facility_id 
  join order_status os on os.order_id = oh.order_id and oh.status_id=os.status_id
where 
  MONTH(os.status_datetime)= 8 
  and YEAR(os.status_datetime)= 2023 
  and oh.status_id = "ORDER_COMPLETED" 
group by oh.order_id;
```
