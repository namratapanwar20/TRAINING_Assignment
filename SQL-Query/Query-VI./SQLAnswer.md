**6. Total $ value of shipments shipped from facility 904/906 to first quarter:**
```sql
select 
  sum(oi.unit_price * oi.quantity) TOTALMONETARYVALUE 
from 
  order_item oi 
  join order_header oh on oh.order_id = oi.order_id 
  and oh.currency_uom = 'USD' 
  join order_shipment os on os.order_id = oh.order_id 
  join shipment s on s.shipment_id = os.shipment_id 
  and s.status_id = 'SHIPMENT_SHIPPED' 
  and s.origin_facility_id in ('904', '906') 
  join shipment_status ss on s.shipment_id = ss.shipment_id 
  and month(ss.status_date) in (1, 3) 
  and year(ss.status_date) = 2022;

```
