**16. Send sale orders shipped from the warehouse:**
```sql
select 
	oh.order_id 
from 
	order_header oh
	join order_item oi on oh.order_id = oi.order_id
		and SALES_CHANNEL_ENUM_ID = "POS_SALES_CHANNEL"
	join order_item_ship_group_assoc oisga on oisga.order_id = oi.ORDER_ID 
		and oisga.order_item_seq_id = oi.ORDER_ITEM_SEQ_ID 
	join order_item_ship_group oisg on oisg.order_id = oisga.order_id 
	 	and oisg.ship_group_seq_id = oisga.ship_group_seq_id 
	join facility f on f.facility_id = oisg.facility_id 
	join facility_type ft on f.facility_type_id = ft.facility_type_id 
		and ft.parent_type_id = "DISTRIBUTION_CENTER";
```
